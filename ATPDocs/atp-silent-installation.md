---
title: "Installer sans assistance Azure - Protection avancée contre les menaces | Microsoft Docs"
description: "Cet article décrit comment installer sans assistance Azure ATP."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/11/2017
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 24eca4c6-c949-42ea-97b9-41ef0fb611f1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f27020f1b4a5fa7aa8fefbda28eac0c2ad6c64d0
ms.sourcegitcommit: 912e453753156902618ae6ebb8489c2320c06fc6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/12/2018
---
*S’applique à : Azure - Protection avancée contre les menaces*


# <a name="azure-atp-silent-installation"></a>Installation sans assistance d’Azure ATP
Cet article fournit des instructions pour installer sans assistance Azure ATP.

## <a name="prerequisites"></a>Prérequis

Azure ATP nécessite l’installation de Microsoft .NET Framework 4.7. 

Quand vous installez Azure ATP, le .Net Framework 4.7 est automatiquement installé dans le cadre du déploiement d’Azure ATP.

> [!IMPORTANT] 
> Vérifiez que la dernière version du .Net Framework est installée. Si une version antérieure du .Net est installée, votre installation sans assistance d’Azure ATP reste bloquée dans une boucle et échoue. 

> [!NOTE] 
> L’installation du .Net Framework 4.7 peut nécessiter le redémarrage du serveur. Quand vous installez le capteur Azure ATP sur des contrôleurs de domaine, pensez à planifier une fenêtre de maintenance pour ces derniers.
Quand vous utilisez la méthode d’installation sans assistance d’Azure ATP, le programme d’installation est configuré pour redémarrer automatiquement le serveur à la fin de l’installation (si nécessaire). En raison d’un bogue de Windows Installer, l’indicateur *norestart* ne peut pas être utilisé de façon fiable pour s’assurer que le serveur ne redémarre pas : veillez donc à exécuter seulement une installation sans assistance pendant une fenêtre de maintenance.

Pour suivre la progression du déploiement, surveillez les journaux d’installation d’Azure ATP, qui se trouvent dans **%AppData%\Local\Temp**.



## <a name="azure-atp-sensor-silent-installation"></a>Installation sans assistance du capteur Azure ATP

> [!NOTE]
> En cas de déploiement sans assistance du capteur Azure ATP avec System Center Configuration Manager ou un autre système de déploiement de logiciels, il est recommandé de créer deux packages de déploiement :</br>- .NET Framework 4.7, avec redémarrage du contrôleur de domaine</br>- Capteur Azure ATP </br>Rendez le package du capteur Azure ATP dépendant du déploiement du package .NET Framework. </br>Obtenez le [package de déploiement hors connexion .NET Framework 4.7](https://www.microsoft.com/download/details.aspx?id=49982). 


Utilisez la commande suivante pour installer sans assistance le capteur Azure ATP :

**Syntaxe** :

    Azure ATP sensor Setup.exe [/AccessKey=<Access Key>] [/quiet] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
   

> [!NOTE]
> Copiez la clé d’accès à partir du portail de l’espace de travail sous **Configuration**, puis **capteur**.


**Options d’installation** :

> [!div class="mx-tableFixed"]
|Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
|-------------|----------|---------|---------|
|Quiet|/quiet|Oui|Exécute le programme d’installation sans afficher d’interface utilisateur, ni d’invites.|
|Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Oui|Spécifie les paramètres d’installation de .Net Framework. Doit être définie de manière à effectuer l’installation sans assistance de .Net Framework.|

**Paramètres d’installation** :

> [!div class="mx-tableFixed"]
|Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
|-------------|----------|---------|---------|
|AccessKey|AccessKey="**"|Oui|Définit la clé d’accès servant à inscrire le capteur Azure ATP avec l’espace de travail Azure ATP.|

**Exemples**: Pour installer sans assistance le capteur Azure ATP, connectez-vous à l’ordinateur joint au domaine avec vos informations d’identification d’administrateur d’Azure ATP pour ne pas avoir à spécifier d’informations d’identification dans le cadre de l'installation. Sinon, inscrivez-le avec le service cloud Azure ATP en utilisant les informations d’identification spécifiées :

    "Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" 
    AccessKey="3WlO0uKW7lY6Lk0+dfkfkJQ0qZV6aSq5WxLf71+fuBhggCl/BMs9JxfAwi7oy9vYGviazUS1EPpzte7z8s4grw==" 
    

## <a name="update-the-azure-atp-sensor"></a>Mettre à jour le capteur Azure ATP

Utilisez la commande suivante pour mettre à jour sans assistance le capteur Azure ATP :

**Syntaxe** :

    Azure ATP  sensor Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Options d’installation** :

> [!div class="mx-tableFixed"]
|Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
|-------------|----------|---------|---------|
|Quiet|/quiet|Oui|Exécute le programme d’installation sans afficher d’interface utilisateur, ni d’invites.|
|Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Oui|Spécifie les paramètres d’installation de .Net Framework. Doit être définie de manière à effectuer l’installation sans assistance de .Net Framework.|


**Exemples** : Pour mettre à jour sans assistance le capteur Azure ATP :

        Azure ATP sensor Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-azure-atp-sensor-silently"></a>Désinstaller sans assistance le capteur Azure ATP

Utilisez la commande suivante pour effectuer une désinstallation sans assistance du capteur Azure ATP : **Syntaxe** :

    Azure ATP sensor Setup.exe [/quiet] [/Uninstall] [/Help]
    
**Options d’installation** :

> [!div class="mx-tableFixed"]
|Nom|Syntaxe|Obligatoire pour une désinstallation sans assistance ?|Description|
|-------------|----------|---------|---------|
|Quiet|/quiet|Oui|Exécute le programme de désinstallation sans afficher d’interface utilisateur, ni d’invites.|
|Désinstaller|/uninstall|Oui|Exécute la désinstallation sans assistance du capteur Azure ATP du serveur.|
|Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|

**Exemples** : Pour désinstaller sans assistance le capteur Azure ATP du serveur :


    Azure ATP sensor Setup.exe /quiet /uninstall
    



## <a name="see-also"></a>Voir aussi

- [Configurer le transfert d’événements](configure-event-forwarding.md)
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)