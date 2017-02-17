---
title: "Installer Advanced Threat Analytics - Étape 2 | Microsoft Docs"
description: "La deuxième étape de la procédure d’installation d’ATA vous aide à configurer les paramètres de connectivité du domaine sur le serveur de votre centre ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 23ea3185e0d3556f524d8131a715a6057988f04c


---

*S’applique à : Advanced Threat Analytics version 1.7*



# <a name="install-ata---step-2"></a>Installer ATA - Étape 2

>[!div class="step-by-step"]
[« Étape 1](install-ata-step1.md)
[Étape 3 »](install-ata-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Étape 2. Fournir un nom d’utilisateur et un mot de passe pour se connecter à votre forêt Active Directory

La première fois que vous ouvrez la console ATA, l’écran suivant apparaît :

![ATA welcome stage 1 (Accueil ATA - phase 1)](media/ATA_1.7-welcome-provide-username.png)

1.  Entrez les informations suivantes, puis cliquez sur **Enregistrer** :

    |Champ|Commentaires|
    |---------|------------|
    |**Nom d’utilisateur** (obligatoire)|Entrez le nom de l’utilisateur en lecture seule, par exemple : **ATAuser**.|
    |**Mot de passe** (obligatoire)|Entrez le mot de passe de l’utilisateur en lecture seule, par exemple : **Pencil1**.|
    |**Domaine** (obligatoire)|Entrez le domaine de l’utilisateur en lecture seule, par exemple : **contoso.com**. **Remarque :** il est important d’entrer le nom complet du domaine où se trouve l’utilisateur. Par exemple, si le compte de l’utilisateur se trouve dans le domaine corp.contoso.com, vous devez entrer `corp.contoso.com`, et non contoso.com.|

2. Si vous le souhaitez, vous pouvez cliquer sur **Tester la connexion** pour tester la connectivité au domaine et vérifier que les informations d’identification fournies donnent accès au domaine. Cela ne fonctionne que si le centre ATA dispose d’une connectivité au domaine.   

    Après l’enregistrement, le message d’accueil dans la console devient : ![ATA welcome stage 1 finished](media/ATA_1.7-welcome-provide-username-finished.png)

3. Dans la console, cliquez sur **Download Gateway setup and install the first Gateway** (Télécharger le programme d’installation de passerelle et installer la première passerelle) pour continuer.


>[!div class="step-by-step"]
[« Étape 1](install-ata-step1.md)
[Étape 3 »](install-ata-step3.md)


## <a name="see-also"></a>Voir aussi

- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration requise pour ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Feb17_HO1-->


