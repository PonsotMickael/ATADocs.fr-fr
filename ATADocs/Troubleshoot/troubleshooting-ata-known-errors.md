--
# <a name="required-metadata"></a>métadonnées requises

titre : Résolution des problèmes liés au journal des erreurs Advanced Threat Analytics | Microsoft Docs description : Décrit comment résoudre les erreurs courantes dans ATA mots clés : auteur : rkarlin ms.author: rkarlin manager: mbaldwin ms.date: 14/03/2017 ms.topic: article ms.prod: ms.service: advanced-threat-analytics ms.technology: ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb

# <a name="optional-metadata"></a>métadonnées facultatives

#<a name="robots"></a>ROBOTS :
#<a name="audience"></a>audience:
#<a name="msdevlang"></a>ms.devlang :
ms.reviewer: arzinger

ms.suite: ems
#<a name="mstgtpltfrm"></a>ms.tgt_pltfrm :
#<a name="mscustom"></a>ms.custom :

---

*S’applique à : Advanced Threat Analytics version 1.7*



# <a name="troubleshooting-the-ata-error-log"></a>Résolution des problèmes liés au journal des erreurs ATA
Cette section détaille les erreurs possibles dans les déploiements d’ATA et les étapes requises pour les corriger.
## <a name="ata-gateway-errors"></a>Erreurs liées à la passerelle ATA
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
|System.IO.IOException : échec de l’authentification, car la partie distante a fermé le flux de transport.|TLS 1.0 est désactivé sur la passerelle ATA, mais .Net est configuré pour utiliser TLS 1.2|Utilisez l’une des options suivantes : </br> Activer TLS 1.0 sur la passerelle ATA </br>Activer TLS 1.2 sur .Net en définissant les clés de Registre pour utiliser les valeurs par défaut du système d’exploitation pour LLS et TLS, comme suit : `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"`|



## <a name="ata-lightweight-gateway-errors"></a>Erreurs liées à la passerelle légère ATA

**Erreur** : Alertes « Trafic avec mise en miroir de ports ignoré » en cas d’utilisation de la passerelle légère sur VMware

**Description** : Si vous utilisez des contrôleurs de domaine sur des machines virtuelles VMware, vous pouvez recevoir des alertes concernant le **trafic réseau avec mise en miroir de port ignoré**. Cela peut être dû à une incompatibilité de configuration dans VMware. 
**Résolution** : Pour éviter ces alertes, vous pouvez vérifier que les paramètres TsoEnable, LargeSendOffload, IPv4 et TSO Offload ont la valeur 0 ou qu’ils sont désactivés. Pensez aussi à désactiver IPv4 Giant TSO Offload. Pour plus d’informations, voir la documentation de VMware.


## <a name="ata-iis-errors-not-applicable-for-ata-v17-and-above"></a>Erreurs IIS ATA (non applicable pour ATA 1.7 et versions ultérieures)
|Erreur|Description|Résolution|
|-------------|----------|---------|
|Erreur HTTP 500.19 - Erreur interne du serveur|Le module de réécriture d’URL IIS n’a pas pu s’installer correctement.|Désinstallez et réinstallez le module de réécriture d’URL IIS.<br>[Télécharger le module de réécriture d’URL IIS](http://go.microsoft.com/fwlink/?LinkID=615137)|

## <a name="deployment-errors"></a>Erreurs liées au déploiement
|Erreur|Description|Résolution|
|-------------|----------|---------|
|L’installation de .Net Framework 4.6.1 échoue avec l’erreur 0x800713ec.|Les composants requis pour .Net Framework 4.6.1 ne sont pas installés sur le serveur. |Avant d’installer ATA, vérifiez que les mises à jour Windows [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) et [KB2919355](https://support.microsoft.com/kb/2919355) sont installées sur le serveur.|

![Image d’erreur ATA liée à l’installation de .NET](media/netinstallerror.png)


## <a name="see-also"></a>Voir aussi
- [Prérequis au déploiement d’ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planification de la capacité d’ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurer la collecte d’événements](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configuration du transfert d’événements Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
