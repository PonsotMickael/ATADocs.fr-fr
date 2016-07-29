---
title: "Installer ATA - Étape 2 | Microsoft ATA"
description: "La deuxième étape de la procédure d’installation d’ATA vous aide à configurer les paramètres de connectivité du domaine sur le serveur de votre centre ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 65ec5c86478e9ded096b899d64eb257257095eaf


---

# Installer ATA - Étape 2

>[!div class="step-by-step"]
[« Étape 1](install-ata-step1.md)
[Étape 3 »](install-ata-step3.md)

## Étape 2. Configurer les paramètres généraux de la passerelle ATA
Les paramètres sous l’onglet **Général** s’appliquent à toutes les passerelles ATA gérées par le centre ATA.

Pour configurer les paramètres généraux de la passerelle ATA, procédez comme suit :

1.  Ouvrez la console ATA et connectez-vous. Pour obtenir des instructions, consultez [Utilisation de la console ATA](working-with-ata-console.md).

2.  Cliquez sur l’icône Paramètres et sélectionnez **Configuration**.

    ![Paramètres de configuration de la passerelle ATA](media/ATA-config-icon.JPG)

3.  Sous l’onglet **Général**, sous **Passerelles ATA**, entrez les informations suivantes et cliquez sur **Enregistrer**.

    |Champ|Commentaires|
    |---------|------------|
    |**Nom d’utilisateur** (obligatoire)|Entrez le nom de l’utilisateur en lecture seule, par exemple : **user1**.|
    |**Mot de passe** (obligatoire)|Entrez le mot de passe de l’utilisateur en lecture seule, par exemple : **Pencil1**. **Remarque :** vérifiez que ce mot de passe est correct. Si vous enregistrez le mauvais mot de passe, le service ATA cesse de fonctionner sur les serveurs de passerelle ATA.|
    |**Domaine** (obligatoire)|Entrez le domaine de l’utilisateur en lecture seule, par exemple : **contoso.com**. **Remarque :** il est important d’entrer le nom complet du domaine où se trouve l’utilisateur. Par exemple, si le compte de l’utilisateur se trouve dans le domaine corp.contoso.com, vous devez entrer `corp.contoso.com`, et non contoso.com.|
    |Mise à jour automatique de toutes les passerelles ATA |Si vous activez ce paramètre et que vous mettez à jour le centre ATA à l’occasion de futures publications de version, toutes les passerelles ATA sont automatiquement mises à jour.|

    ![Images les paramètres de connectivité du domaine ATA](media/ata-domain-connectivity-user.jpg)



>[!div class="step-by-step"]
[« Étape 1](install-ata-step1.md)
[Étape 3 »](install-ata-step3.md)


## Voir aussi

- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Conditions préalables au déploiement d’ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Jul16_HO4-->


