---
title: "Dépannage des problèmes connus d’ATA | Microsoft Docs"
description: "Décrit comment résoudre les problèmes connus dans Advanced Threat Analytics"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 8/20/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 2362f6bf64147b972e9c45e3b97bab4280c6eeac
ms.sourcegitcommit: 46dd0e695f16a0dd23bbfa140eba15ea6a34d7af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
*S’applique à : Advanced Threat Analytics version 1.8*



# <a name="troubleshooting-ata-known-issues"></a>Résolution des problèmes connus d’ATA

Cette section détaille les erreurs possibles dans les déploiements d’ATA et les étapes requises pour les corriger.

## <a name="ata-gateway-and-lightweight-gateway-errors"></a>Erreurs de la passerelle ATA et de la passerelle légère ATA

> [!div class="mx-tableFixed"]
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
|System.InvalidOperationException : L’instance 'Microsoft.Tri.Gateway' n’existe pas dans la catégorie spécifiée.|Les PID ont été activés pour traiter les noms dans la passerelle ATA|Utilisez [KB281884](https://support.microsoft.com/kb/281884) pour désactiver les PID dans les noms de processus.|
|System.InvalidOperationException : La catégorie n’existe pas.|Il est possible que les compteurs soient désactivés dans le Registre.|Utilisez [KB2554336](https://support.microsoft.com/kb/2554336) pour reconstruire les compteurs de performance.|
|System.ApplicationException : Impossible de démarrer la session de suivi ETW MMA-ETW-Livecapture-a4f595bd-f567-49a7-b963-20fa4e370329|Il existe une entrée d’hôte dans le fichier HOSTS qui pointe vers le nom court de l’ordinateur.|Supprimez l’entrée d’hôte du fichier C:\Windows\System32\drivers\etc\HOSTS ou remplacez-la par un nom de domaine complet.|
|System.IO.IOException : échec de l’authentification, car la partie distante a fermé le flux de transport.|TLS 1.0 est désactivé sur la passerelle ATA, tandis que .Net est configuré pour utiliser TLS 1.2|Utilisez l’une des options suivantes : </br> Activer TLS 1.0 sur la passerelle ATA </br>Activer TLS 1.2 sur .Net en définissant les clés de Registre pour utiliser les valeurs par défaut du système d’exploitation pour SSL et TLS, comme suit : </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001 `</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] " SchUseStrongCrypto"=dword:00000001`|
|System.TypeLoadException : Impossible de charger le type 'Microsoft.Opn.Runtime.Values.BinaryValueBufferManager' à partir de l’assembly 'Microsoft.Opn.Runtime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'|Échec du chargement par la passerelle ATA des fichiers d’analyse nécessaires.|Vérifiez si Microsoft Message Analyzer est installé. L’installation de Message Analyzer avec la passerelle / passerelle légère ATA n’est pas prise en charge. Désinstallez Message Analyzer et redémarrez le service de passerelle.|
|Alertes « Trafic avec mise en miroir de ports ignoré » lors de l’utilisation de la passerelle légère sur VMware|Si vous utilisez des contrôleurs de domaine sur des machines virtuelles VMware, vous recevrez peut-être des alertes concernant le **trafic réseau avec mise en miroir de ports ignoré**. Cela peut être dû à une incompatibilité de configuration dans VMware. |Pour éviter ces alertes, vous pouvez vérifier que les paramètres suivants sont définis sur 0 ou sont désactivés : TsoEnable, LargeSendOffload, IPv4, TSO Offload. Pensez aussi à désactiver IPv4 Giant TSO Offload. Pour plus d’informations, voir la documentation de VMware.|
|System.Net.WebException : le serveur distant a retourné une erreur : (407) Authentification proxy requise|La communication de la passerelle ATA avec le centre ATA est interrompue par un serveur proxy.|Désactivez le proxy sur l’ordinateur de la passerelle ATA. <br></br>Notez que les paramètres de proxy sont peut-être définis par compte.|
|System.IO.DirectoryNotFoundException : Le système n’arrive pas à trouver le chemin spécifié. (Exception de HRESULT : 0x80070003)|Un ou plusieurs services nécessaires pour exécuter ATA n’ont pas démarré.|Démarrez les services suivants : <br></br>Journaux et alertes de performance (PLA), Planificateur de tâches (Schedule).|
|System.Net.WebException : le serveur distant a retourné une erreur : (403) Interdit|Il a été interdit à la passerelle ATA ou la passerelle légère d’établir une connexion HTTP, car le centre ATA n’est pas approuvé.|Ajoutez le nom NetBIOS et le nom de domaine complet du centre ATA à la liste des sites web approuvés et effacez le cache Interne Explorer (ou le nom du centre ATA tel qu’il est spécifié dans la configuration si le nom configuré est différent du nom de domaine complet/NetBIOS).|
|System.Net.Http.HttpRequestException: PostAsync failed [requestTypeName=StopNetEventSessionRequest]|La passerelle ATA ou la passerelle légère ATA ne peuvent pas arrêter et démarrer la session ETW qui collecte le trafic réseau en raison d’un problème WMI|Suivez les instructions de la rubrique [WMI : reconstruction du référentiel WMI](https://blogs.technet.microsoft.com/askperf/2009/04/13/wmi-rebuilding-the-wmi-repository/) pour résoudre le problème WMI|

 
## <a name="deployment-errors"></a>Erreurs liées au déploiement
> [!div class="mx-tableFixed"]
|Erreur|Description|Résolution|
|-------------|----------|---------|
|L’installation de .Net Framework 4.6.1 échoue avec l’erreur 0x800713ec.|Les composants requis pour .Net Framework 4.6.1 ne sont pas installés sur le serveur. |Avant d’installer ATA, vérifiez que les mises à jour Windows [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) et [KB2919355](https://support.microsoft.com/kb/2919355) sont installées sur le serveur.|
|System.Threading.Tasks.TaskCanceledException : une tâche a été annulée|Le processus de déploiement a dépassé le délai d’expiration, car il n’a pas pu accéder au centre ATA.|1.    Vérifiez la connectivité réseau au centre ATA en y accédant avec son adresse IP. <br></br>2.    Vérifiez la configuration du proxy ou du pare-feu.|
|System.Net.Http.HttpRequestException : une erreur s’est produite lors de l’envoi de la demande. ---> System.Net.WebException : le serveur distant a retourné une erreur : (407) Authentification proxy requise.|Le processus de déploiement a dépassé le délai d’expiration, car il n’a pas pu atteindre le centre ATA en raison d’une configuration incorrecte du proxy.|Désactivez la configuration du proxy avant le déploiement puis réactivez la configuration du proxy. Vous pouvez aussi configurer une exception dans le proxy.|
|System.Net.Sockets.SocketException : Une connexion existante a dû être fermée par l’hôte distant||Utilisez l’une des options suivantes : </br>Activer TLS 1.0 sur la passerelle ATA </br>Activer TLS 1.2 sur .Net en définissant les clés de Registre pour utiliser les valeurs par défaut du système d’exploitation pour SSL et TLS, comme suit :</br> `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br> `[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] " SchUseStrongCrypto"=dword:00000001`|
|Error [\[]DeploymentModel[\]] Failed management authentication [\[]CurrentlyLoggedOnUser=<domain>\<username>Status=FailedAuthentication Exception=[\]]|Le processus de déploiement de la passerelle ATA ou de la passerelle légère ATA n’a pas réussi à s’authentifier auprès du centre ATA.|Ouvrez un navigateur sur l’ordinateur où s’est produit l’échec du processus de déploiement et essayez d’accéder à la console ATA. </br>Si ce n’est pas possible, cherchez à identifier le problème qui se trouve à l’origine de l’échec d’authentification du navigateur auprès du centre ATA. </br>Points à vérifier :</br>configuration du proxy ;</br>problèmes de mise en réseau ;</br>paramètres de stratégie de groupe pour l’authentification sur cet ordinateur différents du centre ATA.|





## <a name="ata-gateway-and-lightweight-gateway-issues"></a>Problèmes de la passerelle ATA et de la passerelle légère

> [!div class="mx-tableFixed"]
|Problème|Description|Résolution|
|-------------|----------|---------|
|Aucun trafic reçu du contrôleur de domaine, mais des alertes de surveillance sont observées|    Aucun trafic n’a été reçu d’un contrôleur de domaine utilisant la mise en miroir de ports via une passerelle ATA|Sur la carte réseau de capture de la passerelle ATA, désactivez ces fonctionnalités dans **Paramètres avancés** :<br></br>RSC (Receive Segment Coalescing) (IPv4)<br></br>RSC (Receive Segment Coalescing) (IPv6)|
|Cette alerte de surveillance s’affiche : **Une partie du trafic réseau n'est pas analysée**|Si vous avez une passerelle ATA ou une passerelle légère sur les machines virtuelles VMware, vous pouvez recevoir cette alerte de surveillance. Ce scénario se produit à cause d’une différence de configuration dans VMware.|Définissez les paramètres suivants avec les valeurs **0** ou **Désactivé** dans la configuration de carte réseau des machines virtuelles : TsoEnable, LargeSendOffload, TSO Offload, Giant TSO Offload|TLS 1.0 est désactivé sur la passerelle ATA, tandis que .Net est configuré pour utiliser TLS 1.2|




## <a name="see-also"></a>Voir aussi
- [Prérequis au déploiement d’ATA](ata-prerequisites.md)
- [Planification de la capacité d’ATA](ata-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
