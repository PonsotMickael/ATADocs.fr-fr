---
title: "Utilisation des journaux d’audit ATA | Microsoft Docs"
description: "Cet article décrit l’utilisation des journaux d’audit ATA dans le journal des événements Windows."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 54f17bc4775868e380586822456330dfc2d45c29
ms.sourcegitcommit: 53b56220fa761671442da273364bdb3d21269c9e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/05/2017
---
*S’applique à : Advanced Threat Analytics version 1.8*

# <a name="working-with-ata-audit-logs"></a>Utilisation des journaux d’audit ATA

Les journaux d’audit ATA sont conservés dans les journaux des événements Windows sous **Applications et services** et **Microsoft ATA** dans les ordinateurs du centre ATA et les passerelles ATA.

Le journal d’audit du centre ATA contient les éléments suivants :
-   Informations sur l’activité suspecte
-   Surveillance des alertes (page d’intégrité)
-   Connexions à de la console ATA
-   Tous les changements de configuration*

Le journal d’audit de la passerelle ATA contient les éléments suivants :
-   Les changements de configuration de la passerelle* 

(Tous les changements de configuration de la passerelle ATA sont configurés dans le centre ATA, mais ils sont toujours audités sur l’ordinateur de la passerelle.)

*Le journal d’audit des changements de configuration contient la configuration précédente et la nouvelle configuration.


## <a name="see-also"></a>Voir aussi
- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
