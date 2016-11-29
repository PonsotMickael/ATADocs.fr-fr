---
title: "Gestion de la base de données ATA | Microsoft Docs"
description: "Procédures pour vous aider à déplacer, sauvegarder ou restaurer la base de données ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/29/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 05e49e23-6e0a-4ec0-9a63-a2093173c8a1
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: fca7f1b2b8260cad6e0ce32aad1c9e1b53fc0ad5
ms.openlocfilehash: 9d7e2a03633acc97d6f918c97f9b67b553d5202e


---

*S’applique à : Advanced Threat Analytics version 1.7*



# <a name="ata-database-management"></a>Gestion de la base de données ATA
Si vous voulez déplacer, sauvegarder ou restaurer la base de données ATA, suivez ces procédures pour MongoDB.

## <a name="backing-up-the-ata-database"></a>Sauvegarde de la base de données ATA
Reportez-vous à la [documentation MongoDB correspondante](http://docs.mongodb.org/manual/administration/backup/).

## <a name="restoring-the-ata-database"></a>Restauration de la base de données ATA
Reportez-vous à la [documentation MongoDB correspondante](http://docs.mongodb.org/manual/administration/backup/).

## <a name="moving-the-ata-database-to-another-drive"></a>Déplacement de la base de données ATA vers un autre lecteur

1.  Arrêtez le service **Microsoft Advanced Threat Analytics Center**.
> [!Important] 
> Assurez-vous que le service ATA Center est arrêté avant de passer à l’étape suivante.

2.  Arrêtez le service **MongoDB**.

3.  Ouvrez le fichier de configuration Mongo situé par défaut à l’emplacement suivant : C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg.

    Trouvez le paramètre `storage: dbPath`.

4.  Déplacez le dossier indiqué dans le paramètre `dbPath` vers le nouvel emplacement.

5.  Remplacez le paramètre `dbPath` du fichier de configuration mongo par le nouveau chemin de dossier, puis enregistrez et fermez le fichier.

    ![Modifier l’image de configuration MongoDB](media/ATA-mongoDB-moveDB.png)

6.  Démarrez le service **MongoDB**.

7. Démarrez le service **Microsoft Advanced Threat Analytics Center**.

## <a name="see-also"></a>Voir aussi
- [Architecture d’ATA](/advanced-threat-analytics/plan-design/ata-architecture)
- [Prérequis au déploiement d’ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Nov16_HO3-->


