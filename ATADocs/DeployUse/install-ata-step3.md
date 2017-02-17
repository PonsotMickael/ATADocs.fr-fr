---
title: "Installer Advanced Threat Analytics - Étape 3 | Microsoft Docs"
description: "La troisième étape de la procédure d’installation d’ATA vous aide à télécharger le package d’installation de la passerelle ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 40a7e5344ca3e8b99d70d1ef63a1cd5a2f0ce09c


---

*S’applique à : Advanced Threat Analytics version 1.7*



# <a name="install-ata---step-3"></a>Installer ATA - Étape 3

>[!div class="step-by-step"]
[« Étape 2](install-ata-step2.md)
[Étape 4 »](install-ata-step4.md)

## <a name="step-3-download-the-ata-gateway-setup-package"></a>Étape 3. Télécharger le package d’installation de la passerelle ATA
Après avoir configuré les paramètres de connectivité du domaine, vous pouvez télécharger le package d’installation de la passerelle ATA. Elle peut être installée sur un serveur dédié ou sur un contrôleur de domaine. Si vous l’installez sur un contrôleur de domaine, elle est installée en tant que passerelle légère ATA. Pour plus d’informations sur la passerelle légère ATA, consultez [Architecture ATA](/advanced-threat-analytics/plan-design/ata-architecture). 

S’il s’agit de la première fois que vous téléchargez une passerelle ATA, l’écran suivant s’affiche :

![Paramètres de configuration de la passerelle ATA](media/ATA_1.7-welcome-download-gateway.PNG)

Si ce n’est pas la première fois que vous téléchargez une passerelle ATA, ce message de bienvenue n’apparaît pas.

> [!NOTE] 
> Pour accéder ultérieurement à l’écran de configuration, cliquez sur l’**icône de paramètres** (en haut à droite) et sélectionnez **Configuration**, puis sous **Système**, cliquez sur **Passerelles**.  

1.  Cliquez sur **« Télécharger l’installation de la passerelle »**.
2.  Enregistrez le package localement.
3.  Copiez le package sur le serveur dédié ou sur le contrôleur de domaine sur lequel vous installez la passerelle ATA. Vous pouvez également ouvrir la console ATA à partir du serveur dédié ou du contrôleur de domaine et ignorer cette étape.

Le fichier zip comprend les éléments suivants :

-   Programme d’installation de la passerelle ATA

-   Fichier de paramètres de configuration avec les informations requises pour se connecter au centre ATA


>[!div class="step-by-step"]
[« Étape 2](install-ata-step2.md)
[Étape 4 »](install-ata-step4.md)

## <a name="see-also"></a>Voir aussi

- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration requise pour ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Feb17_HO1-->


