---
title: "Modifier la configuration ATA - Mot de passe de connectivité de domaine | Microsoft ATA"
description: "Décrit comment modifier le mot de passe de connectivité de domaine sur la passerelle ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 050f1ef0b39d69b64ede53243a7fa2d33d0e4813
ms.openlocfilehash: 7cee457a8959526b25a68c50efea2976bafbef75


---

*S’applique à : Advanced Threat Analytics version 1.7*



# Modifier la configuration ATA - Mot de passe de connectivité de domaine

>[!div class="step-by-step"]
[« URL de la console ATA](modifying-ata-config-consoleurl.md)


## Modifier le mot de passe de connectivité de domaine
Si vous modifiez le mot de passe de connectivité de domaine, assurez-vous que le mot de passe entré est correct. Dans le cas contraire, le service de passerelle ATA cesse de fonctionner sur les passerelles ATA.

Si vous pensez que cela s’est produit, recherchez la ligne suivante dans le fichier Microsoft.Tri.Gateway-Errors.log sur la passerelle ATA :
`The supplied credential is invalid.`

Pour corriger ce problème, procédez comme suit pour mettre à jour le mot de passe de connectivité de domaine dans le centre ATA :

1.  Ouvrez la console ATA dans le centre ATA.

2.  Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône des paramètres de configuration ATA](media/ATA-config-icon.JPG)

3.  Sélectionnez **Services d’annuaire**.

    ![Image de modification du mot de passe de la passerelle ATA](media/ATA-GW-change-DC-password.png)

4.  Sous **Mot de passe**, modifiez le mot de passe.

    Si le centre ATA dispose d’une connectivité au domaine, utilisez le bouton **Tester la connexion** pour valider les informations d’identification.

5.  Cliquez sur **Enregistrer**.

6.  Après avoir modifié le mot de passe, vérifiez manuellement que le service de la passerelle ATA fonctionne sur les serveurs de la passerelle ATA.

>[!div class="step-by-step"]
[« URL de la console ATA](modifying-ata-config-consoleurl.md)

## Voir aussi
- [Utilisation de la console ATA](working-with-ata-console.md)
- [Installer ATA](install-ata.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->


