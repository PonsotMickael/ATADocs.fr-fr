---
title: "Installer ATA - Étape 2 | Microsoft ATA"
description: "La deuxième étape de la procédure d’installation d’ATA vous aide à configurer les paramètres de connectivité du domaine sur le serveur de votre centre ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 050f1ef0b39d69b64ede53243a7fa2d33d0e4813
ms.openlocfilehash: fc268bcb2e3d027b09fa3349427934f60783b971


---

*S’applique à : Advanced Threat Analytics version 1.7*



# Installer ATA - Étape 2

>[!div class="step-by-step"]
[« Étape 1](install-ata-step1.md)
[Étape 3 »](install-ata-step3.md)

## Étape 2. Fournir un nom d’utilisateur et un mot de passe pour se connecter à votre forêt Active Directory

La première fois que vous ouvrez la console ATA, l’écran suivant apparaît :

![ATA welcome stage 1 (Accueil ATA - phase 1)](media/ATA_1.7-welcome-provide-username.png)

1.  Entrez les informations suivantes, puis cliquez sur **Enregistrer** :

    |Champ|Commentaires|
    |---------|------------|
    |**Nom d’utilisateur** (obligatoire)|Entrez le nom de l’utilisateur en lecture seule, par exemple : **ATAuser**.|
    |**Mot de passe** (obligatoire)|Entrez le mot de passe de l’utilisateur en lecture seule, par exemple : **Pencil1**.|
    |**Domaine** (obligatoire)|Entrez le domaine de l’utilisateur en lecture seule, par exemple : **contoso.com**. **Remarque :** il est important d’entrer le nom complet du domaine où se trouve l’utilisateur. Par exemple, si le compte de l’utilisateur se trouve dans le domaine corp.contoso.com, vous devez entrer `corp.contoso.com`, et non contoso.com.|
    |Mise à jour automatique de toutes les passerelles ATA |Si vous activez ce paramètre et que vous mettez à jour le centre ATA à l’occasion de futures publications de version, toutes les passerelles ATA sont automatiquement mises à jour.|

    Après l’enregistrement, le message d’accueil dans la console devient : ![ATA welcome stage 1 finished (Accueil ATA - fin de la phase 1)](media/ATA_1.7-welcome-provide-username-finished.png)

2. Dans la console, cliquez sur **Download Gateway setup and install the first Gateway** (Télécharger le programme d’installation de passerelle et installer la première passerelle) pour continuer.


>[!div class="step-by-step"]
[« Étape 1](install-ata-step1.md)
[Étape 3 »](install-ata-step3.md)


## Voir aussi

- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Conditions préalables au déploiement d’ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Aug16_HO5-->


