---
title: Installer ATA sans assistance | Microsoft ATA
description: "Cet article décrit comment installer ATA sans assistance."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: dce4cbaf894d383851a7039b6457a98c1d5ba5d4


---

# Installation d’ATA sans assistance
Cet article fournit des instructions pour installer ATA sans assistance.
## Conditions préalables

Microsoft ATA v1.6 requiert l’installation de Microsoft .NET Framework 4.6.1. 

Quand vous installez ou mettez à jour ATA, .Net Framework 4.6.1 est automatiquement installé dans le cadre du déploiement de Microsoft ATA.

> [!Note] 
> L’installation de .Net Framework 4.6.1 peut nécessiter le redémarrage du serveur. Quand vous installez la passerelle ATA sur des contrôleurs de domaine, pensez à planifier une fenêtre de maintenance pour ces derniers.
Quand vous utilisez la méthode d’installation d’ATA sans assistance, le programme d’installation est configuré pour redémarrer automatiquement le serveur à la fin de l’installation (si nécessaire). Pour éviter le redémarrage du serveur dans le cadre de l’installation, utilisez l’indicateur `-NoRestart`. Si vous utilisez l’indicateur `-NoRestart` et qu’un redémarrage est requis dans le cadre de l’installation, le programme d’installation s’interrompt jusqu’à ce que le serveur soit redémarré. Pour suivre la progression du déploiement, surveillez les journaux d’installation d’ATA, qui se trouvent dans **%AppData%\Local\Temp**.


## Installer le centre ATA

Utilisez la commande suivante pour installer le centre ATA :

**Syntaxe** :

    “Microsoft ATA Center Setup.exe” [/quiet] [/NoRestart] [/Help] [--LicenseAccepted] [NetFrameworkCommandLineArguments=”/q”] [InstallationPath=“<InstallPath>”] [DatabaseDataPath= “<DBPath>”] [CenterIpAddress=<CenterIPAddress>] [CenterPort=<CenterPort>] [CenterCertificateThumbprint=“<CertThumbprint>”] 
    [ConsoleIpAddress=<ConsoleIPAddress>] [ConsoleCertificateThumbprint=”<CertThumbprint >”]
    
**Options d’installation** :

|Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
|-------------|----------|---------|---------|
|Quiet|/quiet|Oui|Exécute le programme d’installation sans afficher d’interface utilisateur, ni d’invites.|
|NoRestart|/norestart|Non|Supprime toute tentative de redémarrage. Par défaut, l’interface utilisateur demande la confirmation du redémarrage.|
|Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Oui|Spécifie les paramètres d’installation de .Net Framework. Doit être définie de manière à effectuer l’installation sans assistance de .Net Framework.|
|LicenseAccepted|--LicenseAccepted|Oui|Indique que la licence a été lue et approuvée. Doit être définie sur installation sans assistance.|

**Paramètres d’installation** :

|Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
|-------------|----------|---------|---------|
|InstallationPath|InstallationPath=“<InstallPath>”|Non|Définit le chemin de l’installation des fichiers binaires ATA. Chemin par défaut : C:\Program Files\Microsoft Advanced Threat Analytics\Center|
|DatabaseDataPath|DatabaseDataPath= “<DBPath>”|Non|Définit le chemin du dossier des données de la base de données ATA. Chemin par défaut : C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|
|CenterIpAddress|CenterIpAddress=<CenterIPAddress>|Oui|Définit l’adresse IP du service du centre ATA|
|CenterPort|CenterPort=<CenterPort>|Oui|Définit le port réseau du service du centre ATA|
|CenterCertificateThumbprint|CenterCertificateThumbprint=“<CertThumbprint>”|Non|Définit l’empreinte numérique du certificat pour le service du centre ATA. Ce certificat est utilisé pour sécuriser la communication entre le centre ATA et la passerelle ATA. Si ce paramètre n’est pas défini, l’installation génère un certificat auto-signé.|
|ConsoleIpAddress|ConsoleIpAddress=<ConsoleIPAddress>|Oui|Définit l’adresse IP de la console ATA|
|ConsoleCertificateThumbprint|ConsoleCertificateThumbprint=”<CertThumbprint >”|Non|Spécifie l’empreinte numérique du certificat pour la console ATA. Ce certificat est utilisé pour valider l’identité du site web de la console ATA. Si ce paramètre n’est pas spécifié, l’installation génère un certificat auto-signé.|

**Exemples** : Pour installer le centre ATA avec les chemins d’installation par défaut et une seule adresse IP :

    “Microsoft ATA Center Setup.exe” /quiet --LicenseAccepted NetFrameworkCommandLineArguments="/q" CenterIpAddress=192.168.0.10
    CenterPort=444 ConsoleIpAddress=192.168.0.10

Pour installer le centre ATA avec les chemins d’installation par défaut, deux adresses IP et des empreintes numériques de certificat définies par l’utilisateur :

    “Microsoft ATA Center Setup.exe” /quiet --LicenseAccepted NetFrameworkCommandLineArguments ="/q" CenterIpAddress=192.168.0.10 CenterPort=443 CenterCertificateThumbprint= ‎"1E2079739F624148ABDF502BF9C799FCB8C7212F”
    ConsoleIpAddress=192.168.0.11  ConsoleCertificateThumbprint=”G9530253C976BFA9342FD1A716C0EC94207BFD5A”

## Mettez à jour le centre ATA.

Utilisez la commande suivante pour mettre à jour le centre ATA :

**Syntaxe** :

    Microsoft ATA Center Setup.exe” [/quiet] [-NoRestart] /Help] [NetFrameworkCommandLineArguments=”/q”]


**Options d’installation** :

|Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
|-------------|----------|---------|---------|
|Quiet|/quiet|Oui|Exécute le programme d’installation sans afficher d’interface utilisateur, ni d’invites.|
|NoRestart|/norestart|Non|Supprime toute tentative de redémarrage. Par défaut, l’interface utilisateur demande la confirmation du redémarrage.|
|Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Oui|Spécifie les paramètres d’installation de .Net Framework. Doit être définie de manière à effectuer l’installation sans assistance de .Net Framework.|


Pendant la mise à jour d’ATA, le programme d’installation détecte automatiquement qu’ATA est déjà installé sur le serveur, et aucune option d’installation de mise à jour n’est requise.

**Exemples** : Pour mettre à jour le centre ATA sans assistance. Dans les environnements de grande taille, la mise à jour du centre ATA peut prendre un certain temps. Surveillez les journaux ATA pour suivre la progression de la mise à jour.

        “Microsoft ATA Center Setup.exe” /quiet NetFrameworkCommandLineArguments="/q"

## Désinstaller le centre ATA sans assistance

Utilisez la commande suivante pour effectuer une désinstallation sans assistance du centre ATA : **Syntaxe** :

    Microsoft ATA Center Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
     [--DeleteExistingDatabaseData]

**Options d’installation** :

|Nom|Syntaxe|Obligatoire pour une désinstallation sans assistance ?|Description|
|-------------|----------|---------|---------|
|Quiet|/quiet|Oui|Exécute le programme de désinstallation sans afficher d’interface utilisateur, ni d’invites.|
|Désinstaller|/uninstall|Oui|Exécute la désinstallation sans assistance du centre ATA du serveur.|
|NoRestart|/norestart|Non|Supprime toute tentative de redémarrage. Par défaut, l’interface utilisateur demande la confirmation du redémarrage.|
|Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|

**Paramètres d’installation** :

|Nom|Syntaxe|Obligatoire pour une désinstallation sans assistance ?|Description|
|-------------|----------|---------|---------|
|DeleteExistingDatabaseData|DeleteExistingDatabaseData|Non|Supprime tous les fichiers de la base de données existante.|

**Exemples** : Pour désinstaller sans assistance le centre ATA du serveur, en supprimant toutes les données de base de données existantes :


    “Microsoft ATA Center Setup.exe” /quiet /uninstall --DeleteExistingDatabaseData

## Installation de la passerelle ATA sans assistance
Utilisez la commande suivante pour installer la passerelle ATA sans assistance :

**Syntaxe** :

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
    [GatewayCertificateThumbprint=”<CertThumbprint >”] [ConsoleAccountName=”<AccountName>”] 
    [ConsoleAccountPassword=”<AccountPassword>”]

**Options d’installation** :

|Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
|-------------|----------|---------|---------|
|Quiet|/quiet|Oui|Exécute le programme d’installation sans afficher d’interface utilisateur, ni d’invites.|
|NoRestart|/norestart|Non|Supprime toute tentative de redémarrage. Par défaut, l’interface utilisateur demande la confirmation du redémarrage.|
|Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Oui|Spécifie les paramètres d’installation de .Net Framework. Doit être définie de manière à effectuer l’installation sans assistance de .Net Framework.|
|LicenseAccepted|--LicenseAccepted|Oui|Indique que la licence a été lue et approuvée. Doit être définie sur installation sans assistance.|

**Paramètres d’installation** :

|Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
|-------------|----------|---------|---------|
|GatewayCertificateThumbprint|GatewayCertificateThumbprint=”<CertThumbprint >”|Non|Définit l’empreinte numérique du certificat pour le service du centre ATA. Ce certificat est utilisé pour sécuriser la communication entre le centre ATA et la passerelle ATA. Si ce paramètre n’est pas défini, l’installation génère un certificat auto-signé.|
|ConsoleAccountName|ConsoleAccountName=”<AccountName>”|Oui|Définit le nom du compte d’utilisateur (user@domain.com) qui est utilisé pour inscrire la passerelle ATA auprès du centre ATA.|
|ConsoleAccountPassword|ConsoleAccountPassword=”<AccountPassword>”|Oui|Définit le mot de passe du compte d’utilisateur (user@domain.com) qui est utilisé pour inscrire la passerelle ATA auprès du centre ATA.|

**Exemples** : Pour installer sans assistance la passerelle ATA et l’inscrire auprès du centre ATA en utilisant les informations d’identification spécifiées :

    “Microsoft ATA Gateway Setup.exe” /quiet NetFrameworkCommandLineArguments="/q" 
    ConsoleAccountName=”user@contoso.com” ConsoleAccountPassword=“userpwd”
    

## Mettre à jour la passerelle ATA

Utilisez la commande suivante pour mettre à jour la passerelle ATA sans assistance :

**Syntaxe** :

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] /Help] [NetFrameworkCommandLineArguments="/q"]


**Options d’installation** :

|Nom|Syntaxe|Obligatoire pour une installation sans assistance ?|Description|
|-------------|----------|---------|---------|
|Quiet|/quiet|Oui|Exécute le programme d’installation sans afficher d’interface utilisateur, ni d’invites.|
|NoRestart|/norestart|Non|Supprime toute tentative de redémarrage. Par défaut, l’interface utilisateur demande la confirmation du redémarrage.|
|Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Oui|Spécifie les paramètres d’installation de .Net Framework. Doit être définie de manière à effectuer l’installation sans assistance de .Net Framework.|


**Exemples** : Pour mettre à jour la passerelle ATA sans assistance :

        Microsoft ATA Gateway Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## Désinstaller la passerelle ATA sans assistance

Utilisez la commande suivante pour effectuer une désinstallation sans assistance de la passerelle ATA : **Syntaxe** :

    Microsoft ATA Gateway Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
    
**Options d’installation** :

|Nom|Syntaxe|Obligatoire pour une désinstallation sans assistance ?|Description|
|-------------|----------|---------|---------|
|Quiet|/quiet|Oui|Exécute le programme de désinstallation sans afficher d’interface utilisateur, ni d’invites.|
|Désinstaller|/uninstall|Oui|Exécute la désinstallation sans assistance de la passerelle ATA du serveur.|
|NoRestart|/norestart|Non|Supprime toute tentative de redémarrage. Par défaut, l’interface utilisateur demande la confirmation du redémarrage.|
|Aide|/help|Non|Fournit une aide et une référence rapide. Affiche l’utilisation correcte de la commande d’installation, y compris la liste de tous les comportements et options.|

**Exemples** : Pour désinstaller sans assistance la passerelle ATA du serveur :


    Microsoft ATA Gateway Setup.exe /quiet /uninstall
    









## Voir aussi

- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Conditions préalables au déploiement d’ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=Jul16_HO4-->


