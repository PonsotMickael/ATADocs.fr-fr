---
title: "Résolution des problèmes d’Advanced Threat Analytics en utilisant la base de données | Microsoft Docs"
description: "Décrit comment vous pouvez utiliser la base de données ATA pour résoudre les problèmes"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 377a3c81-5c1d-486f-8942-85249aacf560
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 671812b59ee00b27a329c72d09c00317a81d06be
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*S’applique à : Advanced Threat Analytics version 1.7*



# <a name="troubleshooting-ata-using-the-ata-database"></a>Résolution des problèmes liés à ATA à l’aide de la base de données ATA
ATA utilise MongoDB comme base de données.
Vous pouvez interagir avec la base de données à l’aide de la ligne de commande par défaut ou d’un outil d’interface utilisateur pour effectuer la résolution des problèmes et des tâches avancées.

## <a name="interacting-with-the-database"></a>Interaction avec la base de données
La procédure par défaut et la plus simple pour interroger la base de données consiste à utiliser l’interpréteur de commandes Mongo :

1.  Ouvrez une fenêtre de ligne de commande et modifiez le chemin au dossier bin MongoDB. Le chemin par défaut est : **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**.

2.  Exécutez `mongo.exe ATA`. Veillez à taper ATA tout en majuscules.

|Comment...|Syntaxe|Remarques|
|-------------|----------|---------|
|Rechercher des collections dans la base de données.|`show collections`|Utile en tant que test de bout en bout pour constater que le trafic est écrit dans la base de données et que l’événement 4776 est reçu par ATA.|
|Obtenir les détails d’un utilisateur/ordinateur/groupe (UniqueEntity), par exemple un ID d’utilisateur.|`db.UniqueEntity.find({SearchNames: "<name of entity in lower case>"})`||
|Rechercher le trafic d’authentification Kerberos provenant d’un ordinateur donné lors d’une journée spécifique.|`db.KerberosAs_<datetime>.find({SourceComputerId: "<Id of the source computer>"})`|Pour obtenir l’&lt;ID de l’ordinateur source&gt;, vous pouvez interroger les collections UniqueEntity, comme illustré dans l’exemple.<br /><br />Chaque type d’activité réseau, par exemple les authentifications Kerberos, possède sa propre collection par date UTC.|
|Rechercher le trafic NTLM provenant d’un ordinateur donné associé à un compte indiqué lors d’une journée spécifique.|`db.Ntlm_<datetime>.find({SourceComputerId: "<Id of the source computer>", SourceAccountId: "<Id of the account>"})`|Pour obtenir l’&lt;ID de l’ordinateur source&gt; et l’&lt;ID du compte&gt;, vous pouvez interroger les collections UniqueEntity, comme illustré dans l’exemple.<br /><br />Chaque type d’activité réseau, par exemple les authentifications NTLM, possède sa propre collection par date UTC.|
|Rechercher des propriétés avancées telles que les dates d’activation d’un compte. |`db.UniqueEntityProfile.find({UniqueEntityId: "<Id of the account>")`|Pour obtenir l’&lt;ID du compte&gt;, vous pouvez interroger les collections UniqueEntity, comme illustré dans l’exemple.<br>La propriété qui affiche les dates pendant lesquelles le compte a été actif s’appelle « ActiveDates ». Par exemple, vous voulez savoir si un compte a au moins 21 jours d’activité pour que l’algorithme d’apprentissage automatique de comportement inhabituel puisse être exécuté sur ce compte.|
|Apporter des modifications de configuration avancée. Dans cet exemple, nous affectons la valeur 10 000 à la taille de la file d’attente d’envoi pour toutes les passerelles ATA.|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

Voici un exemple de code qui utilise la syntaxe ci-dessus. Si vous étudiez une activité suspecte qui s’est produite le 20/10/2015 et que vous souhaitez en savoir plus sur les activités NTLM effectuées par « John Doe » ce jour-là :<br /><br />Tout d’abord, recherchez l’ID de « John Doe »

`db.UniqueEntity.find({Name: "John Doe"})`<br>Notez son ID comme indiqué par la valeur `_id`. Dans notre exemple, supposons que l’ID est `123bdd24-b269-h6e1-9c72-7737as875351`<br>Recherchez ensuite la collection avec la date la plus proche qui est antérieure à la date que vous recherchez, dans notre exemple 20/10/2015.<br>Recherchez ensuite les activités NTLM du compte de John Doe : 

`db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})`

## <a name="see-also"></a>Voir aussi
- [Prérequis au déploiement d’ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planification de la capacité d’ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurer la collecte d’événements](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configuration du transfert d’événements Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
