---
title: "Exportation et importation d’une configuration ATA | Microsoft Docs"
description: Comment exporter et importer la configuration ATA.
keywords: 
author: rkarlin
ms.author: rkarlin
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
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: f0307ae2e8f222e7c58db234b0fb393072ac7444


---

*S’applique à : Advanced Threat Analytics version 1.7*



# <a name="export-and-import-the-ata-configuration"></a>Exportation et importation d’une configuration ATA
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




<!--HONumber=Jan17_HO1-->


