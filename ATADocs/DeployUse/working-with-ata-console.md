---
title: Utilisation de la console ATA | Microsoft ATA
description: "Explique comment se connecter à la console ATA et à ses composants"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 1eb9397b541eb64cef553f61e8517568d16b0092


---

# Utilisation de la console ATA

Utilisez la console ATA pour surveiller les activités suspectes et les gérer.

## Activation de l’accès à la console ATA
Tout utilisateur membre du groupe Administrateurs local sur le serveur du centre ATA est autorisé à se connecter à la console ATA et à gérer les paramètres d’ATA.
Pour autoriser un utilisateur à se connecter à la console ATA sans en faire un administrateur local, ajoutez-le au groupe local **Administrateurs Microsoft Advanced Threat Analytics**.

## Connexion à la console ATA

1. Sur le serveur du centre ATA, cliquez sur l’icône **Console ATA Microsoft** sur le Bureau ou ouvrez un navigateur pour accéder à la console ATA.

    ![Icône du serveur ATA](media/ata-server-icon.png)

>[!NOTE]
> Vous pouvez également ouvrir un navigateur à partir du centre ATA ou de la passerelle ATA et accéder à l’adresse IP que vous avez configurée dans l’installation du centre ATA pour la console ATA.    

2.  Entrez votre nom d’utilisateur et votre mot de passe, puis cliquez sur **Se connecter**.

![Image de l’écran connexion ATA](media/ATA-log-in-screen.jpg)

> [!NOTE]
> Vous devez ouvrir une session en tant qu’utilisateur membre du groupe Administrateurs local ou du groupe Administrateurs Microsoft Advanced Threat Analytics.

## Console ATA

La console ATA fournit un aperçu rapide de toutes les activités suspectes par ordre chronologique. Elle vous permet d’examiner les détails de toutes les activités et d’effectuer des actions en fonction de ces activités. La console affiche également des alertes et des notifications pour signaler des problèmes liés au réseau ATA ou aux nouvelles activités considérées comme suspectes.

Voici les principaux éléments de la console ATA.


### Chronologie des attaques

Il s’agit de la page de destination qui s’affiche par défaut quand vous vous connectez à la console ATA. Par défaut, toutes les activités suspectes ouvertes sont affichées dans la chronologie des attaques. Vous pouvez filtrer la chronologie des attaques de manière à tout afficher ou de manière à afficher uniquement les activités suspectes dont l’état est Ouvert, Résolu ou Ignoré. Vous pouvez également voir le niveau de gravité attribué à chaque activité.

![Image de la chronologie des attaques ATA](media/attack-timeline.png)

Pour plus d’informations, consultez [Gestion des activités suspectes](/advanced-threat-analytics/deploy-use/working-with-suspicious-activities).

### Barre de notification

Quand une activité suspecte est détectée, la barre de notification s’ouvre automatiquement sur la droite. Si de nouvelles activités suspectes ont été détectées depuis la dernière ouverture de session, la barre de notification s’ouvrira après votre connexion. Pour accéder à la barre de notification, vous pouvez cliquer sur la flèche de droite à tout moment.

![Image de la barre de notification ATA](media/notification-bar.png)

### Filtrage du panneau

Vous pouvez filtrer les activités suspectes qui s’affichent dans la chronologie des attaques ou sous l’onglet Activités suspectes du profil d’entité, selon leur l’état et leur niveau de gravité.

### Barre de recherche

Le menu supérieur comprend une barre de recherche. Vous pouvez rechercher un utilisateur spécifique, un ordinateur ou un groupe dans ATA. Pour tester la fonction de recherche, commencez à taper un nom.

![Image de la recherche dans la console ATA](media/ATA-console-search.png)

### Centre d’intégrité

Le centre d’intégrité envoie des alertes quand un élément du déploiement ATA ne fonctionne pas correctement.

![Image du centre d’intégrité ATA](media/health-center.png)

Quand votre système rencontre un problème, par exemple une erreur de connectivité ou une passerelle ATA déconnectée, l’icône du centre d’intégrité vous en informe à l’aide d’un point rouge. ![Image du point rouge du centre d’intégrité ATA](media/ATA-Health-Center-Alert-red-dot.png)

Les alertes du centre d’intégrité peuvent être ignorées ou résolues, et classées comme étant d’importance haute, moyenne ou faible. Si vous résolvez une alerte que le service ATA détecte comme étant toujours active, elle sera automatiquement mise dans la liste des alertes ouvertes. Si le système détecte que l’alerte n’a plus de raison d’être (le problème a été résolu), l’alerte est placée automatiquement dans la liste des alertes résolues.

### Profils d’utilisateur et d’ordinateur

ATA crée un profil pour chaque utilisateur et chaque ordinateur du réseau. Le profil utilisateur contient des informations générales, telles que l’appartenance aux groupes, les connexions récentes et les ressources récemment consultées.

![Profil utilisateur](media/user-profile.png)

Le profil d’ordinateur contient des informations générales, telles que les connexions récentes et les ressources récemment consultées.

![Profil d’ordinateur](media/computer-profile.png)

ATA fournit des informations supplémentaires sur les entités (ordinateurs, appareils, utilisateurs) dans les pages suivantes : Résumé, Activités et Activités suspectes.

Quand ATA n’est pas en mesure de résoudre complètement un profil, il l’indique par une icône représentant un cercle à demi rempli.


![Image du profil non résolu dans ATA](media/ATA-Unresolved-Profile.jpg)

### Mini-profil

Quand une entité est présentée dans la console (par exemple un utilisateur ou un ordinateur), si vous pointez votre souris dessus, un mini-profil s’ouvre automatiquement et affiche les informations suivantes si elles sont disponibles :

![Image du mini-profil dans ATA](media/ATA-mini-profile.jpg)

-   Nom

-   Image

-   Courrier électronique

-   Téléphone

-   Nombre d’activités suspectes par niveau de gravité



## Voir aussi
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->


