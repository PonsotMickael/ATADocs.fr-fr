---
title: "Prérequis pour Azure - Protection avancée contre les menaces | Microsoft Docs"
description: "Décrit la configuration requise pour réussir le déploiement d’Azure ATP dans votre environnement"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 62c99622-2fe9-4035-9839-38fec0a353da
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 819eeb73c57e7b1de5e7e5e837aa2d6db2e0848d
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2018
---
*S’applique à : Azure - Protection avancée contre les menaces*



# <a name="azure-atp-prerequisites"></a>Prérequis pour Azure ATP
Cet article décrit la configuration requise pour réussir le déploiement d’Azure ATP dans votre environnement.

>[!NOTE]
> Pour plus d’informations sur la façon de planifier les ressources et la capacité, consultez [Planification de la capacité Azure ATP](atp-capacity-planning.md).


Azure ATP se compose du service cloud Azure ATP, qui est constitué du portail de gestion de l’espace de travail et d’un portail d’espace de travail, du capteur autonome Azure ATP et/ou du capteur Azure ATP. Pour plus d’informations sur les composants Azure ATP, consultez [Architecture Azure ATP](atp-architecture.md).

Chaque espace de travail Azure ATP prend en charge une limite de forêt Active Directory et le niveau fonctionnel de forêt Windows 2003 et versions ultérieures. Pour les déploiements à plusieurs forêts, un espace de travail Azure ATP distinct est nécessaire pour chaque forêt.


[Avant de commencer](#before-you-start) : cette section répertorie les informations que vous devez rassembler ainsi que les comptes et entités réseau dont vous devez disposer avant de procéder à l’installation d’Azure ATP.

[Portail de gestion de l’espace de travail Azure ATP](#azure-atp-workspace-management-portal-and-workspace-portal-requirements) : cette section décrit la configuration requise du navigateur du portail de gestion de l’espace de travail.

[Portail de l’espace de travail Azure ATP](#azure-atp-workspace-management-portal-and-workspace-portal-requirements) : cette section décrit la configuration requise du navigateur pour l’exécution du portail de l’espace de travail Azure ATP.

[Capteur autonome Azure ATP](#azure-atp-sensor-requirements) : cette section répertorie le matériel du capteur autonome Azure ATP, la configuration logicielle requise ainsi que les paramètres que vous devez configurer sur vos serveurs de capteurs autonomes Azure ATP.

[Capteur Azure ATP](#azure-atp-lightweight-sensor-requirements) : cette section répertorie le matériel du capteur Azure ATP ainsi que la configuration logicielle requise.

![Diagramme d’architecture Azure ATP](media/ATP-architecture-topology.png)

## <a name="before-you-start"></a>Avant de commencer
Cette section répertorie les informations que vous devez rassembler ainsi que les comptes et entités réseau dont vous devez disposer avant de procéder à l’installation d’Azure ATP.


-   Compte d’utilisateur Azure AD **local** et mot de passe avec accès en lecture à tous les objets dans les domaines surveillés.

    > [!NOTE]
    > Si vous avez défini des listes de contrôle d’accès (ACL) personnalisées sur différentes unités d’organisation dans votre domaine, vérifiez que l’utilisateur sélectionné dispose d’autorisations d’accès en lecture à ces unités d’organisation.

-   Si vous exécutez Wireshark sur le capteur autonome Azure ATP, vous devez redémarrer le service de capteur Azure - Protection avancée contre les menaces après avoir arrêté la capture Wireshark. Sinon, le capteur arrête la capture du trafic.

- Si vous essayez d’installer le capteur ATP sur un ordinateur configuré avec une carte d’association de cartes réseau, vous recevez une erreur d’installation. Si vous souhaitez installer le capteur ATP sur un ordinateur configuré avec une association de cartes réseau, contactez votre représentant du support technique Azure ATP.

-    Recommandé : L’utilisateur doit disposer d’autorisations en lecture seule sur le conteneur Objets supprimés. Azure ATP peut ainsi détecter la suppression en bloc d’objets dans le domaine. Pour plus d’informations sur la configuration des autorisations en lecture seule sur le conteneur Objets supprimés, consultez la section **Modifier les autorisations sur un conteneur d’objets supprimés** dans l'article [Afficher ou définir des autorisations sur un objet d’annuaire](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

-   Facultatif : compte d’un utilisateur sans activité réseau. Ce compte est configuré comme l’utilisateur honeytoken Azure ATP. Pour plus d’informations, consultez [Configurer des exclusions et un utilisateur honeytoken](install-atp-step7.md).

-   Facultatif : quand vous déployez le capteur autonome, il est nécessaire de transférer les événements Windows 4776, 4732, 4733, 4728, 4729, 4756, 4757 et 7045 à ATP pour qu’Azure ATP puisse encore mieux détecter les attaques de type « Pass-The-Hash », par force brute et Honey Tokens, la modification de groupes sensibles ainsi que la création de service malveillant. Dans le capteur Azure ATP, ces événements sont reçus automatiquement. Dans le capteur autonome Azure ATP, vous pouvez recevoir ces événements de votre serveur SIEM ou en définissant les transferts d’événements Windows à partir de votre contrôleur de domaine. Les événements collectés fournissent à Azure ATP des informations supplémentaires qui ne sont pas accessibles par le biais du trafic réseau du contrôleur de domaine.


## <a name="azure-atp-workspace-management-portal-and-workspace-portal-requirements"></a>Configuration requise pour le portail de l’espace de travail et le portail de gestion de l’espace de travail Azure ATP
L’accès au portail de l’espace de travail Azure ATP et au portail de gestion de l’espace de travail Azure ATP s’effectue via un navigateur prenant en charge les navigateurs et les paramètres suivants :
-   Microsoft Edge
-   Internet Explorer 10 et versions ultérieures
-   Google Chrome 4.0 et versions ultérieures
-   Largeur d’écran d’une résolution minimale de 1 700 pixels
-   Pare-feu/proxy ouvert : pour communiquer avec le service cloud Azure ATP, vous devez ouvrir le port 443 dans votre pare-feu/proxy sur *.atp.azure.com. 

## <a name="azure-atp-standalone-sensor-requirements"></a>Configuration requise pour le capteur autonome Azure ATP
Cette section décrit la configuration requise pour le capteur autonome Azure ATP.
### <a name="general"></a>Général
L’installation du capteur autonome Azure ATP sur un serveur Windows Server 2012 R2 ou Windows Server 2016 (dont Server Core) est prise en charge.
Le capteur autonome Azure ATP peut être installé sur un serveur membre d’un domaine ou d’un groupe de travail.
Le capteur autonome Azure ATP peut servir à surveiller les contrôleurs de domaine avec le niveau fonctionnel de domaine Windows 2003 et versions ultérieures.

Pour que vos contrôleurs de domaine communiquent avec le service cloud, vous devez ouvrir le port 443 dans vos pare-feu et proxies sur *.atp.azure.com.


Pour plus d’informations sur l’utilisation de machines virtuelles avec le capteur autonome Azure ATP, consultez [Configurer la mise en miroir des ports](configure-port-mirroring.md).

> [!NOTE]
> Un minimum de 5 Go d’espace sont nécessaires et 10 Go sont recommandés. Cela inclut l’espace nécessaire pour les fichiers binaires Azure ATP, les journaux Azure ATP et les journaux de performance.

### <a name="server-specifications"></a>Spécifications du serveur
Pour bénéficier de performances optimales, choisissez **Hautes performances** comme **Option d’alimentation** pour le capteur autonome Azure ATP.<br>
Un capteur autonome Azure ATP peut prendre en charge la surveillance de plusieurs contrôleurs de domaine, en fonction du volume du trafic réseau à destination et en provenance des contrôleurs de domaine.

>[!NOTE] 
> En cas d’exécution en tant que machine virtuelle, la mémoire dynamique ou toute autre fonctionnalité d’augmentation de la mémoire n’est pas prise en charge.

Pour plus d’informations sur la configuration matérielle requise pour le capteur autonome Azure ATP, consultez [Planification de la capacité Azure ATP](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Synchronisation de l’heure

L’heure des serveurs et contrôleurs de domaine sur lesquels le capteur est installé doit être synchronisée pour que tout écart entre eux ne dépasse pas cinq minutes.


### <a name="network-adapters"></a>Cartes réseau
Le capteur autonome Azure ATP nécessite au moins une carte de gestion et au moins une carte de capture :

-   **Carte de gestion** : cette carte est utilisée pour les communications sur votre réseau d’entreprise. Elle doit être configurée avec les paramètres suivants :

    -   Adresse IP statique (capteur par défaut inclus)

    -   Serveurs DNS préféré et auxiliaire

    -   Le **Suffixe DNS pour cette connexion** doit être le nom DNS du domaine pour chaque domaine surveillé.

        ![Configurer le suffixe DNS dans les paramètres TCP/IP avancés](media/ATP-DNS-Suffix.png)

        > [!NOTE]
        > Si le capteur autonome Azure ATP est membre du domaine, le suffixe peut être configuré automatiquement.

-   **Carte de capture** : cette carte est utilisée pour capturer le trafic à destination et en provenance des contrôleurs de domaine.

    > [!IMPORTANT]
    > -   Configurez la mise en miroir des ports de la carte de capture comme la destination du trafic réseau des contrôleurs de domaine. Pour plus d’informations, consultez [Configurer la mise en miroir des ports](configure-port-mirroring.md). En règle générale, vous devez collaborer avec l’équipe de virtualisation ou de mise en réseau pour configurer la mise en miroir des ports.
    > -   Configurez une adresse IP statique non routable pour votre environnement, sans capteur par défaut ni adresse de serveur DNS. Par exemple : 1.1.1.1/32. Cela permet de garantir que la carte réseau de capture peut capturer le volume maximum de trafic et que la carte réseau de gestion est utilisée pour envoyer et recevoir le trafic réseau demandé.

### <a name="ports"></a>Ports
Le tableau suivant répertorie les ports qui, au minimum, doivent être configurés sur la carte de gestion pour satisfaire aux exigences du capteur autonome Azure ATP :

|Protocole|Transport|Port|Vers/À partir de|Direction|
|------------|-------------|--------|-----------|-------------|
|LDAP|TCP et UDP|389|Contrôleurs de domaine|Sortant|
|LDAP sécurisé (LDAPS)|TCP|636|Contrôleurs de domaine|Sortant|
|LDAP vers le catalogue global|TCP|3268|Contrôleurs de domaine|Sortant|
|LDAPS vers le catalogue global|TCP|3269|Contrôleurs de domaine|Sortant|
|SSL (*.atp.azure.com)|TCP|443|Service cloud Azure ATP|Sortant|
|Kerberos|TCP et UDP|88|Contrôleurs de domaine|Sortant|
|Netlogon (SMB, CIFS, SAM-R)|TCP et UDP|445|Contrôleurs de domaine|Sortant|
|Horloge Windows|UDP|123|Contrôleurs de domaine|Sortant|
|DNS|TCP et UDP|53|Serveurs DNS|Sortant|
|NTLM sur RPC|TCP|135|Tous les appareils sur le réseau|Sortant|
|NetBIOS|UDP|137|Tous les appareils sur le réseau|Sortant|
|Syslog (facultatif)|TCP/UDP|514, selon la configuration|Serveur SIEM|Entrant|
|RADIUS|UDDP|1813|RADIUS|Entrant|

> [!NOTE]
> - À l’aide du compte d’utilisateur du service d’annuaire, le capteur interroge les points de terminaison de votre organisation à la recherche des administrateurs locaux en utilisant SAM-R (ouverture de session réseau) pour générer le [graphe des chemins de mouvement latéral](use-case-lateral-movement-path.md). Pour plus d’informations, consultez [Configurer les autorisations requises SAM-R](install-atp-step8-samr.md).
> - Les ports suivants doivent être ouverts en entrée sur les appareils du réseau à partir des capteurs autonome Azure ATP :
>   -   NTLM sur RPC (port TCP 135) à des fins de résolution
>   -   NetBIOS (port UDP 137) à des fins de résolution
>   -   Requêtes SAM-R (port TCP/UDP 445) à des fins de détection


## <a name="azure-atp-sensor-requirements"></a>Configuration requise pour le capteur Azure ATP
Cette section décrit la configuration requise pour le capteur Azure ATP.
### <a name="general"></a>Général
Le capteur Azure ATP prend en charge l’installation sur un contrôleur de domaine exécutant Windows Server 2008 R2 SP1 (Server Core non inclus), Windows Server 2012, Windows Server 2012 R2 et Windows Server 2016 (Core inclus, mais pas Nano).

Le contrôleur de domaine peut être un contrôleur de domaine en lecture seule (RODC).

Pour que vos contrôleurs de domaine communiquent avec le service cloud, vous devez ouvrir le port 443 dans vos pare-feu et proxies sur *.atp.azure.com.

Pendant l’installation, .NET Framework 4.7 est installé et peut entraîner un redémarrage du contrôleur de domaine.


> [!NOTE]
> Un minimum de 5 Go d’espace sont nécessaires et 10 Go sont recommandés. Cela inclut l’espace nécessaire pour les fichiers binaires Azure ATP, les journaux Azure ATP et les journaux de performance.

### <a name="server-specifications"></a>Spécifications du serveur

Le capteur Azure ATP nécessite au minimum deux cœurs et 6 Go de RAM sur le contrôleur de domaine.
Pour bénéficier de performances optimales, choisissez **Hautes performances** comme **Option d’alimentation** pour le capteur Azure ATP.
Vous pouvez déployer le capteur Azure ATP sur des contrôleurs de domaine de différentes charges et tailles, en fonction de la quantité de trafic réseau vers et depuis les contrôleurs de domaine et de la quantité de ressources installées sur ce contrôleur de domaine.

>[!NOTE] 
> En cas d’exécution en tant que machine virtuelle, la mémoire dynamique ou toute autre fonctionnalité d’augmentation de la mémoire n’est pas prise en charge.

Pour plus d’informations sur la configuration matérielle requise pour le capteur Azure ATP, consultez [Planification de la capacité Azure ATP](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Synchronisation de l’heure

L’heure des serveurs et contrôleurs de domaine sur lesquels le capteur est installé doit être synchronisée pour que tout écart entre eux ne dépasse pas cinq minutes.

### <a name="network-adapters"></a>Cartes réseau

Le capteur Azure ATP surveille le trafic local sur toutes les cartes réseau du contrôleur de domaine. <br>
Après le déploiement, vous pouvez utiliser le portail de l’espace de travail Azure ATP si vous voulez changer les cartes réseau surveillées.

Le capteur n’est pas pris en charge sur les contrôleurs de domaine exécutant Windows 2008 R2 avec l’association de carte réseau Broadcom activée.

### <a name="ports"></a>Ports
Le tableau suivant répertorie les ports qui, au minimum, sont requis par le capteur Azure ATP :

|Protocole|Transport|Port|Vers/À partir de|Direction|
|------------|-------------|--------|-----------|-------------|
|SSL (*.atp.azure.com)|TCP|443|Service cloud Azure ATP|Sortant|
|DNS|TCP et UDP|53|Serveurs DNS|Sortant|
|NTLM sur RPC|TCP|135|Tous les appareils sur le réseau|Sortant|
|Netlogon (SMB, CIFS, SAM-R)|TCP/UDP|445|Contrôleurs de domaine|Sortant|
|NetBIOS|UDP|137|Tous les appareils sur le réseau|Sortant|
|Syslog (facultatif)|TCP/UDP|514, selon la configuration|Serveur SIEM|Entrant|
|RADIUS|UDDP|1813|RADIUS|Entrant|

> [!NOTE]
> - À l’aide du compte d’utilisateur du service d’annuaire, le capteur interroge les points de terminaison de votre organisation à la recherche des administrateurs locaux en utilisant SAM-R (ouverture de session réseau) pour générer le [graphe des chemins de mouvement latéral](use-case-lateral-movement-path.md).
> - Les ports suivants doivent être ouverts en entrée sur les appareils du réseau à partir des capteurs Azure ATP :
>   -   NTLM sur RPC (port TCP 135) à des fins de résolution
>   -   NetBIOS (port UDP 137) à des fins de résolution
>   -   Requêtes SAM-R (port TCP/UDP 445) à des fins de détection





## <a name="see-also"></a>Voir aussi
- [Outil de dimensionnement Azure ATP](http://aka.ms/aatpsizingtool)
- [Architecture Azure ATP](atp-architecture.md)
- [Installer ATP](install-atp-step1.md)
- [Consultez le forum ATP !](https://aka.ms/azureatpcommunity)

