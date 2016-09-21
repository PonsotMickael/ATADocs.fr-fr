---
title: "Nouveautés d’ATA version 1.7 | Microsoft ATA"
description: "Répertorie les nouveautés d’ATA version 1.7, ainsi que les problèmes connus"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 
ms.reviewer: 
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ae6a3295d2fffabdb8e5f713674379e4af499ac2
ms.openlocfilehash: af9101260b1a0d5d9da32398f638f76e0c8c40a7


---

# Nouveautés d’ATA version 1.7
Ces notes de publication fournissent des informations sur les problèmes connus de cette version d’Advanced Threat Analytics.

## Quelles sont les nouveautés d’ATA 1.7 ?
La mise à jour vers ATA 1.7 comprend des améliorations dans les domaines suivants :

-   Détections nouvelles et mises à jour

-   Contrôle d'accès en fonction du rôle

-   Prise en charge de Windows Server 2016 et Windows Server Core

-   Améliorations apportées à l’expérience utilisateur


### Détections nouvelles et mises à jour


- **Reconnaissance à l’aide d’une énumération de services d’annuaire** Dans le cadre de la phase de reconnaissance, les pirates collectent des informations sur les entités du réseau à l’aide de différentes méthodes. L’énumération des services d’annuaire à l’aide du protocole SAM-R permet aux pirates d’obtenir la liste des utilisateurs et des groupes dans un domaine et de comprendre l’interaction entre les différentes entités. 

- **Améliorations liées à Pass-the-Hash** Pour améliorer la détection Pass-the-Hash, nous avons ajouté des modèles de comportement supplémentaires pour les modèles d’authentification d’entités. Ces modèles permettent à ATA de mettre en corrélation le comportement d’entité avec les authentifications NTLM suspectes, et de différencier les attaques Pass-the-Hash réelles du comportement de scénarios de type « faux positif ».

- **Améliorations liées à Pass-the-Ticket** Pour détecter les attaques avancées en général et les attaques Pass-the-Ticket en particulier, la corrélation entre une adresse IP et le compte d’ordinateur doit être exacte. Il s’agit d’un véritable défi dans les environnements où les adresses IP changent rapidement par conception (par exemple sur les réseaux Wi-Fi et quand plusieurs machines virtuelles partagent le même hôte). Pour relever ce défi et améliorer la précision de la détection de Pass-the-Ticket, le mécanisme de résolution de nom de réseau d’ATA a été amélioré considérablement afin de réduire les faux positifs.

- **Améliorations liées aux comportements anormaux** Dans ATA 1.7, les données d’authentification NTLM ont été ajoutées comme source de données pour les détections de comportements anormaux, fournissant aux algorithmes une couverture plus étendue du comportement d’entité sur le réseau. 

- **Améliorations liées à l’implémentation de protocoles inhabituels** ATA détecte désormais l’implémentation de protocoles inhabituels dans le protocole Kerberos, ainsi que d’autres anomalies dans le protocole NTLM. Plus spécifiquement, ces nouvelles anomalies pour Kerberos sont couramment utilisées dans les attaques de type « Over-pass-the-Hash ».


### Infrastructure

- **Contrôle d’accès en fonction du rôle ** Fonctionnalité de contrôle d’accès en fonction du rôle (RBAC). ATA 1.7 inclut trois rôles : ATA Administrator, ATA Analyst et ATA Executive.

- **Prise en charge de Windows Server 2016 et Windows Server Core** ATA 1.7 prend en charge le déploiement de passerelles légères sur les contrôleurs de domaine exécutant Server Core pour Windows Server 2012 et Server Core pour Windows Server 2012 R2. De plus, cette version prend en charge Windows Server 2016 pour les composants Centre ATA et Passerelle ATA.

### Expérience de l'utilisateur
- **Expérience de configuration** Dans cette version, l’expérience de configuration d’ATA a été repensée pour une meilleure expérience utilisateur et pour mieux prendre en charge les environnements à plusieurs passerelles ATA. Cette version introduit également la page de mise à jour de la passerelle ATA pour une gestion plus simple et plus performante des mises à jour automatiques pour les différentes passerelles.

## Problèmes connus
Les problèmes connus de cette version sont les suivants :

### Risque d’échec de mise à jour automatique de passerelle
**Symptômes :** Dans les environnements avec des liaisons WAN lentes, la mise à jour de la passerelle ATA peut atteindre le délai d’expiration de mise à jour (100 secondes) et échouer.
Dans la console ATA, la passerelle ATA a l’état « Mise à jour (téléchargement du package) » pendant un laps de temps prolongé et l’opération finit par échouer.

**Solution de contournement :** Pour contourner ce problème, téléchargez le package de passerelle ATA le plus récent à partir de la console ATA et mettez à jour la passerelle ATA manuellement.

### Échec de la migration en cas de mise à jour à partir d’ATA 1.6
Quand vous effectuez la mise à jour vers ATA 1.7, le processus peut échouer avec le code d’erreur suivant : *0x80070643*:

![Erreur de la mise à jour d’ATA vers la version 1.7](media/ata-update-error.png)

Consultez le journal de déploiement pour déterminer la cause de l’échec. Le journal de déploiement se trouve à l’emplacement suivant, **%temp%\..\Microsoft Advanced Thread Analytics Center_{date_stamp}_MsiPackage.log**. 

Le tableau ci-dessous répertorie les erreurs à rechercher et le script Mongo correspondant permettant de corriger l’erreur. Consultez l’exemple en dessous du tableau pour savoir comment exécuter le script Mongo :

| Erreur dans le fichier journal de déploiement                                                                                                                  | Script Mongo                                                                                                                                                                         |
|---|---|
| System.FormatException: Size {size},is larger than MaxDocumentSize 16777216 <br>Plus bas dans le fichier :<br>  Microsoft.Tri.Center.Deployment.Package.Actions.DatabaseActions.MigrateUniqueEntityProfiles(Boolean isPartial)                                                                                        | db.UniqueEntityProfile.find().forEach(function(obj){if(Object.bsonsize(obj) > 12582912) {print(obj._id);print(Object.bsonsize(obj));db.UniqueEntityProfile.remove({_id:obj._id});}}) |
| System.OutOfMemoryException: Exception of type 'System.OutOfMemoryException' was thrown<br>Plus bas dans le fichier :<br>Microsoft.Tri.Center.Deployment.Package.Actions.DatabaseActions.ReduceSuspiciousActivityDetailsRecords(IMongoCollection`1 suspiciousActivityCollection, Int32 deletedDetailRecordMaxCount) | db.SuspiciousActivity.find().forEach(function(obj){if(Object.bsonsize(obj) > 500000),{print(obj._id);print(Object.bsonsize(obj));db.SuspiciousActivity.remove({_id:obj._id});}})     |
|System.Security.Cryptography.CryptographicException: Bad Length<br>Plus bas dans le fichier :<br> Microsoft.Tri.Center.Deployment.Package.Actions.DatabaseActions.MigrateCenterSystemProfile(IMongoCollection`1 systemProfileCollection)| CenterThumbprint=db.SystemProfile.find({_t:"CenterSystemProfile"}).toArray()[0].Configuration.SecretManagerConfiguration.CertificateThumbprint;db.SystemProfile.update({_t:"CenterSystemProfile"},{$set:{"Configuration.ManagementClientConfiguration.ServerCertificateThumbprint":CenterThumbprint}})|


Pour exécuter le script approprié, effectuez les étapes suivantes. 

1.  À partir d’une invite de commandes avec élévation de privilèges, accédez à l’emplacement suivant : **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**
2.  Tapez – **Mongo.exe ATA**   (*Remarque* : ATA doit être en majuscules.)
3.  Collez le script qui correspond à l’erreur dans le journal de déploiement à partir du tableau ci-dessus.

![Script Mongo ATA](media/ATA-mongoDB-script.png)

À ce stade, vous devez pouvoir redémarrer la mise à niveau.

### ATA signale un nombre important d’activités suspectes « *Reconnaissance à l’aide d’énumérations de services d’annuaire*» :
 
Il est fort probable que cela se produise quand un outil d’analyse de réseau s’exécute sur toutes les machines clientes de l’organisation ou une grande partie d’entre elles. Si vous rencontrez ce problème :

1. Si vous pouvez identifier la raison ou l’application spécifique qui s’exécute sur les machines clientes, envoyez un e-mail à ATAEval@microsoft.com avec les informations.
2. Utilisez le script mongo suivant pour ignorer tous ces événements (voir ci-dessus comment exécuter le script mongo) :

db.SuspiciousActivity.update({_t: "SamrReconnaissanceSuspiciousActivity"}, {$set: {Status: "Dismissed"}}, {multi: true})

### ATA envoie des notifications concernant les activités suspectes ignorées :
Si les notifications ont été configurées, ATA peut continuer à envoyer des notifications (e-mail, syslog et journaux des événements) pour les activités suspectes ignorées.
Pour le moment, il n'existe pas de solution de contournement pour ce problème. 

### La passerelle ATA n’arrivera peut-être pas à s’enregistrer auprès du centre ATA si TLS 1.0 et TLS 1.1 sont désactivés :
Si TLS 1.0 et TLS 1.1 sont désactivés sur la passerelle ATA (ou la passerelle légère), la passerelle n’arrivera peut-être pas à s’enregistrer auprès du centre ATA

### Le renouvellement automatique des certificats utilisés par ATA n’est pas pris en charge
L’utilisation du renouvellement automatique des certificats peut empêcher ATA de fonctionner quand le certificat est automatiquement renouvelé. 


## Voir aussi
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Mise à jour d’ATA vers la version 1.7 : guide de migration](ata-update-1.7-migration-guide.md)




<!--HONumber=Sep16_HO2-->


