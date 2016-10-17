---
title: "Modifier la configuration ATA - Adresse IP de la console ATA | Microsoft Advanced Threat Analytics"
description: "Décrit comment modifier l’adresse IP de la console ATA, utilisée pour créer un raccourci vers la console ATA sur les passerelles ATA."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 08/24/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 050f1ef0b39d69b64ede53243a7fa2d33d0e4813
ms.openlocfilehash: b3d11a87f1909c1fd964fa990e5d36a91691a844


---

*S’applique à : Advanced Threat Analytics version 1.7*



# Modifier la configuration ATA - URL de la console ATA

>[!div class="step-by-step"]
[« Certificat du centre ATA](modifying-ata-config-centercert.md)
[Mot de passe de connectivité de domaine »](modifying-ata-config-dcpassword.md)

## Modifier l’URL de la console ATA
Par défaut, l’URL de la console ATA est l’adresse IP sélectionnée pour l’adresse IP de la console ATA lors de l’installation du centre ATA.

L’URL est utilisée dans les scénarios suivants :

-   Installation de passerelles ATA : quand une passerelle ATA est installée, elle s’inscrit auprès du centre ATA. Ce processus d’inscription est effectué par la connexion à la console ATA. Si vous entrez un nom de domaine complet pour l’URL de la console ATA, vous devez vérifier que la passerelle ATA peut résoudre le nom de domaine complet en adresse IP à laquelle la console ATA est liée.

-   Alertes : quand ATA envoie une alerte par courrier électronique ou SIEM, il inclut un lien vers l’activité suspecte. La partie hôte du lien est le paramètre URL de la console ATA.

-   Si vous avez installé un certificat de votre autorité de certification interne, vous souhaiterez probablement faire correspondre l’URL au nom d’objet du certificat pour que les utilisateurs ne reçoivent pas de message d’avertissement lors de la connexion à la console ATA.

-   L’utilisation d’un nom de domaine complet pour l’URL de la console ATA vous permet de modifier l’adresse IP utilisée par la console ATA sans annuler les alertes qui ont été envoyées précédemment ni avoir à retélécharger le package de la passerelle ATA. Vous devez uniquement mettre à jour le DNS avec la nouvelle adresse IP.

> [!NOTE]
> Après avoir modifié l’URL de la console ATA, vous devez télécharger le package d’installation de la passerelle ATA avant d’installer de nouvelles passerelles ATA.

Si vous devez modifier l’URL de la console ATA, procédez comme suit sur le serveur du centre ATA.

1.  Ouvrez la console ATA.

2.  Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône des paramètres de configuration ATA](media/ATA-config-icon.JPG)

3.  Sélectionnez **Centre**.

4.  Sous **Adresse IP de la console**, sélectionnez l’une des adresses IP existantes.

5.  Sous **URL de la console**, modifiez l’URL en fonction des besoins :

    ![URL de la console ATA](media/ATA-chge-center-URL.png)
6.  Cliquez sur **Enregistrer**.

>[!div class="step-by-step"]
[« Certificat du centre ATA](modifying-ata-config-centercert.md)
[Mot de passe de connectivité de domaine »](modifying-ata-config-dcpassword.md)


## Voir aussi
- [Utilisation de la console ATA](working-with-ata-console.md)
- [Installer ATA](install-ata.md)
- [Consultez le forum ATA !](https://aka.ms/ata-forum)



<!--HONumber=Aug16_HO5-->

