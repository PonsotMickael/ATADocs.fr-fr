---
title: "Fichier de configuration d’ATA | Microsoft ATA"
description: "Sauvegarde de la configuration d’ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 10/31/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f334f9c8440e4bb0202579de220f6530d0aabad8
ms.openlocfilehash: 542bdf983e26fa98c036de55860b482d0b1d734d


---

*S’applique à : Advanced Threat Analytics version 1.7*



# <a name="ata-configuration-file"></a>Fichier de configuration d’ATA
La configuration d’ATA est stockée dans la collection « SystemProfile » dans la base de données.
Cette collection est sauvegardée toutes les heures par le service du centre ATA dans des fichiers nommés « SystemProfile_*horodatage*.json ». Les 10 dernières versions sont stockées.
Celui-ci se trouve dans un sous-dossier appelé « Backup ». À l’emplacement de l’installation d’ATA par défaut, il se trouve ici : *C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*horodatage*.json*. 

**Remarque** : Il est recommandé de sauvegarder ce fichier quelque part quand vous apportez des modifications importantes à ATA.

Il est possible de restaurer tous les paramètres en exécutant la commande suivante :

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Voir aussi
- [Architecture d’ATA](/advanced-threat-analytics/plan-design/ata-architecture)
- [Prérequis au déploiement d’ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Oct16_HO5-->


