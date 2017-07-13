---
title: "Surveiller l’intégrité et les événements système d’Advanced Threat Analytics | Microsoft Docs"
description: "Le centre d’intégrité ATA vous permet de vérifier le bon fonctionnement du service ATA, d’être alerté en cas de problèmes potentiels et de voir les événements système dans l’observateur d’événements."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7e396cddb818c0e80f8b7d78764a58d6abd560e5
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2017
---
*S’applique à : Advanced Threat Analytics version 1.8*


# Utilisation de l’intégrité et des événements système d’ATA
<a id="working-with-ata-system-health-and-events" class="xliff"></a>

## Centre d’intégrité ATA
<a id="ata-health-center" class="xliff"></a>
Le centre d’intégrité ATA vous permet d’évaluer les performances de votre service ATA et vous prévient en cas de problèmes.

## Utilisation du centre d’intégrité ATA
<a id="working-with-the-ata-health-center" class="xliff"></a>
Si un problème se produit, le centre d’intégrité ATA déclenche une alerte en affichant un point rouge au-dessus de l’icône du centre d’intégrité dans la barre de menus.

![Barre d’outils du point rouge dans le centre d’intégrité ATA](media/ATA-Health-Center-Alert-red-dot.png)

### Gestion de l’intégrité d’ATA
<a id="managing-ata-health" class="xliff"></a>
Pour vérifier l’intégrité globale de votre système, cliquez sur l’icône du centre d’intégrité dans la barre de menus. ![Icône du centre d’intégrité ATA](media/ATA-red-dot.png)

-   Pour gérer les alertes actives, vous pouvez leur affecter l’état **Résolue(s)** ou **Rejetée(s)**. Dans l’alerte, cliquez sur **Ouvrir**, puis faites défiler la liste jusqu’à **Résolue(s)** ou **Rejetée(s)**.

-   Si vous résolvez un problème et qu’ATA détecte qu’il existe encore, le problème retourne automatiquement dans la liste **Ouvert**. Si ATA détecte qu’un problème ouvert est résolu, le problème passe automatiquement à la liste **Résolu**.

-   Les alertes **Rejetée(s)** vous permettent d’indiquer à ATA que vous ne souhaitez plus vérifier un problème particulier. Par exemple, si vous recevez une alerte concernant un problème dont vous connaissez l’existence et que vous n’envisagez pas de le résoudre, vous pouvez lui affecter l’état **Rejetée(s)**. Ainsi, vous ne recevrez plus de notifications et il n’apparaîtra plus dans la liste **Ouvert**.

![Image de problèmes dans le centre d’intégrité ATA](media/ATA-Health-Issue.JPG)






## Voir aussi
<a id="see-also" class="xliff"></a>
- [Gestion des paramètres de la détection ATA](working-with-detection-settings.md)
- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
