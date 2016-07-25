---
title: "Installer ATA - Étape 3 | Microsoft ATA"
description: "La troisième étape de la procédure d’installation d’ATA vous aide à télécharger le package d’installation de la passerelle ATA."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 3645f4688667158f673c6456aeb7ed5da01c2ddb


---

# Installer ATA - Étape 3

>[!div class="step-by-step"]
[« Étape 2](install-ata-step2.md)
[Étape 4 »](install-ata-step4.md)

## Étape 3. Télécharger le package d’installation de la passerelle ATA
Après avoir configuré les paramètres de connectivité du domaine, vous pouvez télécharger le package d’installation de la passerelle ATA. Elle peut être installée sur un serveur dédié ou sur un contrôleur de domaine. Si vous l’installez sur un contrôleur de domaine, elle est installée en tant que passerelle légère ATA. Pour plus d’informations sur la passerelle légère ATA, consultez [Architecture ATA](/advanced-threat-analytics/plan-design/ata-architecture). 

Pour télécharger le package d’installation de la passerelle ATA :

1.  À partir de la console ATA, cliquez sur l’icône des paramètres et sélectionnez **Configuration**.

    ![Paramètres de configuration de la passerelle ATA](media/ATA-config-icon.JPG)

2.  Sous l’onglet **Passerelles ATA**, cliquez sur **Télécharger l’installation de la passerelle ATA**.

3.  Enregistrez le package localement.
4.  Copiez le package sur le serveur dédié ou sur le contrôleur de domaine sur lequel vous installez la passerelle ATA. Vous pouvez également ouvrir la console ATA à partir du serveur dédié ou du contrôleur de domaine et ignorer cette étape.

Le fichier zip comprend les éléments suivants :

-   Programme d’installation de la passerelle ATA

-   Fichier de paramètres de configuration avec les informations requises pour se connecter au centre ATA


>[!div class="step-by-step"]
[« Étape 2](install-ata-step2.md)
[Étape 4 »](install-ata-step4.md)

## Voir aussi

- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Conditions préalables au déploiement d’ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Jul16_HO3-->


