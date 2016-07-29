---
title: "Modifier la configuration ATA - Certificat IIS | Microsoft ATA"
description: "Décrit comment modifier le certificat utilisé par IIS pour le centre ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e58a0390-57ef-4c68-a987-2e75e5f3d6b3
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 18d3dfdc2262765d71d82f395273e2972118cbfb


---

# Modifier la configuration ATA - Certificat IIS

>[!div class="step-by-step"]
[« Adresse IP de la console ATA](modifying-ata-config-consoleip.md)
[Mot de passe de connectivité de domaine »](modifying-ata-config-dcpassword.md)

## Modifier le certificat IIS
Dans la console, vous pouvez sélectionner et modifier le certificat pour le service du centre ATA, mais vous ne pouvez pas modifier le certificat utilisé par IIS.

Si vous souhaitez le modifier, procédez comme suit :

> [!NOTE]
> Après avoir modifié le certificat IIS, vous devez télécharger le package d’installation de la passerelle ATA avant d’installer de nouvelles passerelles ATA.

Si vous devez modifier le certificat utilisé par IIS pour le centre ATA, procédez comme suit sur le serveur du centre ATA.

1.  Installez le nouveau certificat sur le serveur du centre ATA.

2.  Ouvrez le Gestionnaire des services Internet (IIS).

3.  Développez le nom du serveur, puis **Sites**.

4.  Sélectionnez le site de la console ATA Microsoft et, dans le volet **Actions**, cliquez sur **Liaisons**.

    ![Actions de liaisons de la console ATA](media/ATA-console-change-IP-bindings.jpg)

5.  Sélectionnez **HTTPS** et cliquez sur **Modifier**.

6.  Sous **Certificat SSL**, sélectionnez le nouveau certificat.

7.  Téléchargez le package d’installation de la passerelle ATA avant d’installer une nouvelle passerelle ATA.

>[!div class="step-by-step"]
[« Adresse IP de la console ATA](modifying-ata-config-consoleip.md)
[Mot de passe de connectivité de domaine »](modifying-ata-config-dcpassword.md)

## Voir aussi
- [Utilisation de la console ATA](working-with-ata-console.md)
- [Installer ATA](install-ata.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->


