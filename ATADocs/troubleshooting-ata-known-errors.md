---
title: "Dépannage des problèmes connus d’ATA | Microsoft Docs"
description: "Décrit comment résoudre les problèmes connus dans Advanced Threat Analytics"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/3/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 0ded0dd064f0327f6e52f15081e2b9dce14f982b
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2017
---
*S’applique à : Advanced Threat Analytics version 1.8*



# <a name="troubleshooting-ata-known-issues"></a>Résolution des problèmes connus d’ATA

Cette section détaille les erreurs possibles dans les déploiements d’ATA et les étapes requises pour les corriger.

## <a name="ata-gateway-and-lightweight-gateway-errors"></a>Erreurs de la passerelle ATA et de la passerelle légère ATA

|Erreur|Description|Résolution|
|-------------|----------|---------|
|System.DirectoryServices.Protocols.LdapException : Une erreur locale s’est produite.|La passerelle ATA n’a pas pu s’authentifier auprès du contrôleur de domaine.|1. Vérifiez que l’enregistrement DNS du contrôleur de domaine est correctement configuré sur le serveur DNS. <br>2. Vérifiez que l’heure de la passerelle ATA est synchronisée avec l’heure du contrôleur de domaine.|
|System.IdentityModel.Tokens.SecurityTokenValidationException : Impossible de valider la chaîne de certificats|La passerelle ATA n’a pas pu valider le certificat du centre ATA.|1. Vérifiez que le certificat de l’autorité de certification racine est installé dans le magasin de certificats d’autorité de certification de confiance sur la passerelle ATA. <br>2. Vérifiez que la liste de révocation de certificats est disponible et que la validation de la révocation de certificats peut être effectuée.|
|Microsoft.Common.ExtendedException : Échec de l’analyse de l’heure de génération|La passerelle ATA n’a pas pu analyser les messages syslog transférés à partir du serveur SIEM.|Vérifiez que le serveur SIEM est configuré pour transférer les messages dans un des formats pris en charge par ATA.|
|System.ServiceModel.FaultException : Une erreur s’est produite lors de la vérification de la sécurité du message.|La passerelle ATA n’a pas pu s’authentifier auprès du centre ATA.|Vérifiez que l’heure de la passerelle ATA est synchronisée avec l’heure du centre ATA.|
|System.ServiceModel.EndpointNotFoundException : Connexion impossible à net.tcp://center.ip.addr:443/IEntityReceiver|La passerelle ATA n’a pas pu établir de connexion au centre ATA.|Vérifiez que les paramètres réseau sont corrects et que la connexion réseau entre la passerelle ATA et le centre ATA est active.|
|System.DirectoryServices.Protocols.LdapException : Le serveur LDAP n’est pas disponible.|La passerelle ATA n’a pas pu interroger le contrôleur de domaine à l’aide du protocole LDAP.|1. Vérifiez que le compte d’utilisateur utilisé par ATA pour se connecter au domaine Active Directory a un accès en lecture à tous les objets de l’arborescence Active Directory. <br>2. Vérifiez que le contrôleur de domaine n’est pas renforcé pour empêcher les requêtes LDAP à partir du compte d’utilisateur utilisé par ATA.|
|Microsoft.Tri.Infrastructure.ContractException : Exception de contrat|La passerelle ATA n’a pas pu synchroniser la configuration à partir du centre ATA.|Terminez la configuration de la passerelle ATA dans la console ATA.|
|System.Reflection.ReflectionTypeLoadException : Impossible de charger un ou plusieurs des types demandés. Récupérez la propriété LoaderExceptions pour obtenir plus d’informations.|L’Analyseur de message est installé sur la passerelle ATA.| Désinstallez l’Analyseur de message.|
|Erreur [Layout] System.OutOfMemoryException : une exception de type « System.OutOfMemoryException » a été levée.|La passerelle ATA ne dispose pas de suffisamment de mémoire.|Augmentez la quantité de mémoire disponible sur le contrôleur de domaine.|
|Échec du démarrage du consommateur dynamique ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException : le fournisseur d’événements PEFNDIS n’est pas prêt|L’Analyseur de message (PEF) n’a pas été installé correctement.|Si vous utilisez Hyper-V, essayez de mettre à niveau les services d’intégration Hyper-V. Sinon, contactez le support technique pour obtenir une solution de contournement.|
|Échec de l’installation avec l’erreur : 0x80070652|Il y a d’autres installations en attente sur votre machine.|Attendez la fin des autres installations, puis redémarrez l’ordinateur, si nécessaire.|
|System.InvalidOperationException : L’instance 'Microsoft.Tri.Gateway' n’existe pas dans la catégorie spécifiée.|Les PID ont été activés pour traiter les noms dans la passerelle ATA|Utilisez [KB281884](https://support.microsoft.com/en-us/kb/281884) pour désactiver les PID dans les noms de processus.|
|System.InvalidOperationException : La catégorie n’existe pas.|Il est possible que les compteurs soient désactivés dans le Registre.|Utilisez [KB2554336](https://support.microsoft.com/en-us/kb/2554336) pour reconstruire les compteurs de performance.|
|System.ApplicationException : Impossible de démarrer la session de suivi ETW MMA-ETW-Livecapture-a4f595bd-f567-49a7-b963-20fa4e370329|Il existe une entrée d’hôte dans le fichier HOSTS qui pointe vers le nom court de l’ordinateur.|Supprimez l’entrée d’hôte du fichier C:\Windows\System32\drivers\etc\HOSTS ou remplacez-la par un nom de domaine complet.|
|System.IO.IOException : échec de l’authentification, car la partie distante a fermé le flux de transport.|TLS 1.0 est désactivé sur la passerelle ATA, mais .Net est configuré pour utiliser TLS 1.2|Utilisez l’une des options suivantes : </br> Activer TLS 1.0 sur la passerelle ATA </br>Activer TLS 1.2 sur .Net en définissant les clés de Registre pour utiliser les valeurs par défaut du système d’exploitation pour LLS et TLS, comme suit : `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`|
|System.TypeLoadException : Impossible de charger le type 'Microsoft.Opn.Runtime.Values.BinaryValueBufferManager' à partir de l’assembly 'Microsoft.Opn.Runtime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'|Échec du chargement par la passerelle ATA des fichiers d’analyse nécessaires.|Vérifiez si Microsoft Message Analyzer est installé. L’installation de Message Analyzer avec la passerelle / passerelle légère ATA n’est pas prise en charge. Désinstallez Message Analyzer et redémarrez le service de passerelle.|
|Alertes « Trafic avec mise en miroir de ports ignoré » lors de l’utilisation de la passerelle légère sur VMware|Si vous utilisez des contrôleurs de domaine sur des machines virtuelles VMware, vous recevrez peut-être des alertes concernant le **trafic réseau avec mise en miroir de ports ignoré**. Cela peut être dû à une incompatibilité de configuration dans VMware. |Pour éviter ces alertes, vous pouvez vérifier que les paramètres suivants sont définis sur 0 ou sont désactivés : TsoEnable, LargeSendOffload, IPv4, TSO Offload. Pensez aussi à désactiver IPv4 Giant TSO Offload. Pour plus d’informations, voir la documentation de VMware.|


## <a name="deployment-errors"></a>Erreurs liées au déploiement
|Erreur|Description|Résolution|
|-------------|----------|---------|
|L’installation de .Net Framework 4.6.1 échoue avec l’erreur 0x800713ec.|Les composants requis pour .Net Framework 4.6.1 ne sont pas installés sur le serveur. |Avant d’installer ATA, vérifiez que les mises à jour Windows [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) et [KB2919355](https://support.microsoft.com/kb/2919355) sont installées sur le serveur.|
|System.Threading.Tasks.TaskCanceledException : une tâche a été annulée|Le processus de déploiement a dépassé le délai d’expiration, car il n’a pas pu accéder au centre ATA.|1.    Vérifiez la connectivité réseau au centre ATA en y accédant avec son adresse IP. <br></br>2.    Vérifiez la configuration du proxy ou du pare-feu.|
|System.Net.Http.HttpRequestException : une erreur s’est produite lors de l’envoi de la demande. ---> System.Net.WebException : le serveur distant a retourné une erreur : (407) Authentification proxy requise.|Le processus de déploiement a dépassé le délai d’expiration, car il n’a pas pu atteindre le centre ATA en raison d’une configuration incorrecte du proxy.|Désactivez la configuration du proxy avant le déploiement puis réactivez la configuration du proxy. Vous pouvez aussi configurer une exception dans le proxy.|
|Aucun trafic reçu du contrôleur de domaine, mais des alertes de surveillance sont observées|    Aucun trafic n’a été reçu d’un contrôleur de domaine utilisant la mise en miroir de ports via une passerelle ATA|Sur la carte réseau de capture de la passerelle ATA, désactivez ces fonctionnalités dans **Paramètres avancés** :<br></br>RSC (Receive Segment Coalescing) (IPv4)<br></br>RSC (Receive Segment Coalescing) (IPv6)|





## <a name="see-also"></a>Voir aussi
- [Prérequis au déploiement d’ATA](ata-prerequisites.md)
- [Planification de la capacité d’ATA](ata-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
