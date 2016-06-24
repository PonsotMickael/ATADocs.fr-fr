---
# required metadata

title: Résolution des problèmes liés au journal des erreurs ATA | Microsoft Advanced Threat Analytics
description: Décrit comment vous pouvez résoudre les erreurs courantes dans ATA. 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Résolution des problèmes liés au journal des erreurs ATA
Cette section détaille les erreurs possibles dans les déploiements d’ATA et les étapes requises pour les corriger.
## Erreurs liées à la passerelle ATA
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
|Échec du démarrage du consommateur dynamique ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException : le fournisseur d’événements PEFNDIS n’est pas prêt|L’Analyseur de message (PEF) n’a pas été installé correctement.|Contactez le support technique pour obtenir une solution de contournement.|
|Échec de l’installation avec l’erreur : 0x80070652|Il y a d’autres installations en attente sur votre machine.|Attendez la fin des autres installations, puis redémarrez l’ordinateur, si nécessaire.|

## Erreurs liées à la console ATA
|Erreur|Description|Résolution|
|-------------|----------|---------|
|Erreur HTTP 500.19 - Erreur interne du serveur|Le module de réécriture d’URL IIS n’a pas pu s’installer correctement.|Désinstallez et réinstallez le module de réécriture d’URL IIS.<br>[Téléchargez le module de réécriture d’URL IIS.](http://go.microsoft.com/fwlink/?LinkID=615137)|

## Erreurs liées au déploiement
|Erreur|Description|Résolution|
|-------------|----------|---------|
|L’installation de .Net Framework 4.6.1 échoue avec l’erreur 0x800713ec.|Les composants requis pour .Net Framework 4.6.1 ne sont pas installés sur le serveur. |Avant d’installer ATA, vérifiez que les mises à jour Windows [KB2919442](https://www.microsoft.com/en-us/download/details.aspx?id=42135) et [KB2919355](https://support.microsoft.com/en-us/kb/2919355) sont installées sur le serveur.|

![Image d’erreur ATA liée à l’installation de .NET](media/netinstallerror.png)


## Voir aussi
- [Configuration requise pour ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planification de la capacité ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurer la collecte d’événements](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configuration du transfert d’événements Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#ATA_event_WEF)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO4-->


