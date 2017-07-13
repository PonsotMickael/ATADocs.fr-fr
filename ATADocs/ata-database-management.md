---
title: "Gestion de la base de données Advanced Threat Analytics | Microsoft Docs"
description: "Procédures pour vous aider à déplacer, sauvegarder ou restaurer la base de données ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/12/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 05e49e23-6e0a-4ec0-9a63-a2093173c8a1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4fe667574ea011c032bacd8f5bce4b07c2c46602
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
*S’applique à : Advanced Threat Analytics version 1.8*



# Gestion de la base de données ATA
<a id="ata-database-management" class="xliff"></a>
Si vous voulez déplacer, sauvegarder ou restaurer la base de données ATA, suivez ces procédures pour MongoDB.

## Sauvegarde de la base de données ATA
<a id="backing-up-the-ata-database" class="xliff"></a>
Reportez-vous à la [documentation MongoDB correspondante](http://docs.mongodb.org/manual/administration/backup/).

## Restauration de la base de données ATA
<a id="restoring-the-ata-database" class="xliff"></a>
Reportez-vous à la [documentation MongoDB correspondante](http://docs.mongodb.org/manual/administration/backup/).

## Déplacement de la base de données ATA vers un autre lecteur
<a id="moving-the-ata-database-to-another-drive" class="xliff"></a>

1.  Arrêtez le service **Microsoft Advanced Threat Analytics Center**.
> [!Important] 
> Assurez-vous que le service ATA Center est arrêté avant de passer à l’étape suivante.

2.  Arrêtez le service **MongoDB**.

3.  Ouvrez le fichier de configuration Mongo situé par défaut à l’emplacement suivant : C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg.

    Trouvez le paramètre `storage: dbPath`.

4.  Déplacez le dossier indiqué dans le paramètre `dbPath` vers le nouvel emplacement.

5.  Remplacez le paramètre `dbPath` du fichier de configuration mongo par le nouveau chemin de dossier, puis enregistrez et fermez le fichier.

    ![Modifier l’image de configuration MongoDB](media/ATA-mongoDB-moveDB.png)

6.  Démarrez le service **MongoDB**.

7. Démarrez le service **Microsoft Advanced Threat Analytics Center**.

## Voir aussi
<a id="see-also" class="xliff"></a>
- [Architecture d’ATA](ata-architecture.md)
- [Prérequis au déploiement d’ATA](ata-prerequisites.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

