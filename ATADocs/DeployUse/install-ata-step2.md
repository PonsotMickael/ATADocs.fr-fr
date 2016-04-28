---
# required metadata

title: Installer ATA - Étape 2 | Microsoft Advanced Threat Analytics
description: La deuxième étape de la procédure d’installation d’ATA vous aide à configurer les paramètres de connectivité du domaine sur le serveur de votre centre ATA.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Installer ATA - Étape 2

>[!div class="step-by-step"]
[« Étape 1](install-ata-step1.md)
[Étape 3 »](install-ata-step3.md)

## Étape 2. Configurer les paramètres de connectivité du domaine de la passerelle ATA
Les paramètres de la section Paramètres de connectivité du domaine s’appliquent à toutes les passerelles ATA gérées par le centre ATA.

Pour configurer les paramètres de connectivité du domaine, procédez comme suit sur le serveur du centre ATA.

1.  Ouvrez la console ATA et connectez-vous. Pour obtenir des instructions, consultez [Utilisation de la console ATA](/advanced-threat-analytics/understand/working-with-ata-console).

2.  Quand vous vous connectez à la console ATA pour la première fois après l’installation du centre ATA, vous êtes automatiquement redirigé vers la page de configuration des passerelles ATA. Si vous souhaitez modifier l’un de ces paramètres par la suite, cliquez sur l’icône Paramètres et sélectionnez **Configuration**.

    ![Paramètres de configuration de la passerelle ATA](media/ATA-config-icon.JPG)

3.  Dans la page **Passerelles**, cliquez sur **Paramètres de connectivité du domaine**, entrez les informations suivantes, puis cliquez sur **Enregistrer**.

    |Champ|Commentaires|
    |---------|------------|
    |**Nom d’utilisateur** (obligatoire)|Entrez le nom de l’utilisateur en lecture seule, par exemple : **user1**.|
    |**Mot de passe** (obligatoire)|Entrez le mot de passe de l’utilisateur en lecture seule, par exemple : **Pencil1**. **Remarque :** vérifiez que ce mot de passe est correct. Si vous enregistrez le mauvais mot de passe, le service ATA cesse de fonctionner sur les serveurs de passerelle ATA.|
    |**Domaine** (obligatoire)|Entrez le domaine de l’utilisateur en lecture seule, par exemple : **contoso.com**. **Remarque :** il est important d’entrer le nom complet du domaine où se trouve l’utilisateur. Par exemple, si le compte de l’utilisateur se trouve dans le domaine corp.contoso.com, vous devez entrer `corp.contoso.com`, et non contoso.com.|
    ![Images les paramètres de connectivité du domaine ATA](media/ATA-Domain-Connectivity-User.JPG)


>[!div class="step-by-step"]
[« Étape 1](install-ata-step1.md)
[Étape 3 »](install-ata-step3.md)


## Voir aussi

- [Pour obtenir de l’aide, consultez notre forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurer la collecte d’événements](/advanced-threat-analytics/plandesign/configure-event-collection)
- [Conditions préalables au déploiement d’ATA](/advanced-threat-analytics/plandesign/ata-prerequisites)


<!--HONumber=Apr16_HO2-->


