---
title: "Modifier la configuration ATA - Adresse IP de la console ATA | Microsoft ATA"
description: "Décrit comment modifier l’adresse IP de la console ATA, utilisée pour créer un raccourci vers la console ATA sur les passerelles ATA."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 3c02459e6a0cde359e632bf966948cf3a72170a2


---

# Modifier la configuration ATA - Adresse IP de la console ATA

>[!div class="step-by-step"]
[« Certificat du centre ATA](modifying-ata-config-centercert.md)
[Certificat IIS »](modifying-ata-config-iiscert.md)

## Modifier l’adresse IP de la console ATA
Par défaut, l’URL de la console ATA est l’adresse IP sélectionnée pour l’adresse IP de la console ATA lors de l’installation du centre ATA.

L’URL est utilisée dans les scénarios suivants :

-   Installation de passerelles ATA : quand une passerelle ATA est installée, elle s’inscrit auprès du centre ATA. Ce processus d’inscription est effectué par la connexion à la console ATA. Si vous entrez un nom de domaine complet pour l’URL de la console ATA, vous devez vérifier que la passerelle ATA peut résoudre le nom de domaine complet en adresse IP à laquelle la console ATA est liée dans IIS. En outre, l’URL est utilisée pour créer le raccourci vers la console ATA sur les passerelles ATA.

-   Alertes : quand ATA envoie une alerte par courrier électronique ou SIEM, il inclut un lien vers l’activité suspecte. La partie hôte du lien est le paramètre URL de la console ATA.

-   Si vous avez installé un certificat de votre autorité de certification interne, vous souhaiterez probablement faire correspondre l’URL au nom d’objet du certificat pour que les utilisateurs ne reçoivent pas de message d’avertissement lors de la connexion à la console ATA.

-   L’utilisation d’un nom de domaine complet pour l’URL de la console ATA vous permet de modifier l’adresse IP utilisée par IIS pour la console ATA sans annuler les alertes qui ont été envoyées précédemment ni avoir à télécharger une nouvelle fois le package de la passerelle ATA. Vous devez uniquement mettre à jour le DNS avec la nouvelle adresse IP.

> [!NOTE]
> Après avoir modifié l’URL de la console ATA, vous devez télécharger le package d’installation de la passerelle ATA avant d’installer de nouvelles passerelles ATA.

Si vous devez modifier l’adresse IP utilisée par IIS pour la console ATA, procédez comme suit sur le serveur du centre ATA.

1.  Installez l’adresse IP sur le serveur du centre ATA.

2.  Ouvrez le Gestionnaire des services Internet.

3.  Développez le nom du serveur, puis **Sites**.

4.  Sélectionnez le site de la console ATA Microsoft et, dans le volet **Actions**, cliquez sur **Liaisons**.

    ![Image d’actions de liaisons de la console ATA](media/ATA-console-change-IP-bindings.jpg)

5.  Sélectionnez **HTTP** et cliquez sur **Modifier** pour sélectionner la nouvelle adresse IP. Faites de même pour **HTTPS** en sélectionnant la même adresse IP.

    ![Image de modification de la liaison de site](media/ATA-change-console-IP.jpg)

6.  Dans le volet **Actions**, cliquez sur **Redémarrer** sous **Gérer le site Web**.

7.  Ouvrez une invite de commandes administrateur et tapez les commandes suivantes pour mettre à jour le pilote HTTP.SYS :

    -   Pour ajouter la nouvelle adresse IP : `netsh http add iplisten ipaddress=newipaddress`

    -   Pour vérifier que la nouvelle adresse est utilisée : `netsh http show iplisten`

    -   Pour supprimer l’ancienne adresse IP : `netsh http delete iplisten ipaddress=oldipaddress`

8.  Si l’URL de la console ATA utilise toujours une adresse IP, mettez à jour l’URL de la console ATA vers la nouvelle adresse IP et téléchargez le package d’installation de la passerelle ATA avant de déployer de nouvelles passerelles ATA.

9. Si l’URL de la console ATA est un nom de domaine complet, mettez à jour le DNS avec la nouvelle adresse IP pour le nom de domaine complet.

>[!div class="step-by-step"]
[« Certificat du centre ATA](modifying-ata-config-centercert.md)
[Certificat IIS »](modifying-ata-config-iiscert.md)


## Voir aussi
- [Utilisation de la console ATA](working-with-ata-console.md)
- [Installer ATA](install-ata.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


