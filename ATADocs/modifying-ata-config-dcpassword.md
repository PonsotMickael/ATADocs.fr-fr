---
title: "Modifier la configuration Advanced Threat Analytics - Mot de passe de connectivité de domaine | Microsoft Docs"
description: "Décrit comment modifier le mot de passe de connectivité de domaine sur la passerelle ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 652d3a9e20737d26e8776035690a180f6bd84593
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/07/2017
---
*S’applique à : Advanced Threat Analytics version 1.8*



# <a name="change-ata-configuration---domain-connectivity-password"></a>Modifier la configuration ATA - Mot de passe de connectivité de domaine



## <a name="change-the-domain-connectivity-password"></a>Modifier le mot de passe de connectivité de domaine
Si vous modifiez le mot de passe de connectivité de domaine, assurez-vous que le mot de passe entré est correct. Dans le cas contraire, le service de passerelle ATA cesse de fonctionner sur les passerelles ATA.

Si vous pensez que cela s’est produit, recherchez les erreurs suivantes dans le fichier Microsoft.Tri.Gateway-Errors.log sur la passerelle ATA : `The supplied credential is invalid.`

Pour corriger ce problème, procédez comme suit pour mettre à jour le mot de passe de connectivité de domaine dans le centre ATA :

1.  Ouvrez la console ATA dans le centre ATA.

2.  Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône des paramètres de configuration ATA](media/ATA-config-icon.png)

3.  Sélectionnez **Services d’annuaire**.

    ![Image de modification du mot de passe de la passerelle ATA](media/ATA-GW-change-DC-password.png)

4.  Sous **Mot de passe**, modifiez le mot de passe.

    Si le centre ATA dispose d’une connectivité au domaine, utilisez le bouton **Tester la connexion** pour valider les informations d’identification

5.  Cliquez sur **Enregistrer**.

6.  Après avoir modifié le mot de passe, vérifiez manuellement que le service de la passerelle ATA fonctionne sur les serveurs de la passerelle ATA.



## <a name="see-also"></a>Voir aussi
- [Utilisation de la console ATA](working-with-ata-console.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
