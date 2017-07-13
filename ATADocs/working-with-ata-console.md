---
title: "Présentation de la console Advanced Threat Analytics | Microsoft Docs"
description: "Explique comment se connecter à la console ATA et à ses composants"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3d687087dd9e1ae7f7642f9fdd7d89420f3bec27
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2017
---
*S’applique à : Advanced Threat Analytics version 1.8*



# Utilisation de la console ATA
<a id="working-with-the-ata-console" class="xliff"></a>

Utilisez la console ATA pour surveiller les activités suspectes et les gérer.

Tapez « ? » pour obtenir les raccourcis clavier d’accessibilité du portail ATA. 

## Activation de l’accès à la console ATA
<a id="enabling-access-to-the-ata-console" class="xliff"></a>
Pour ouvrir une session dans la console ATA, vous devez utiliser le compte d’un utilisateur auquel a été attribué le rôle ATA approprié pour accéder à la console ATA. Pour plus d’informations sur le contrôle d’accès en fonction du rôle (RBAC) dans ATA, consultez [Utilisation de groupes de rôles ATA](ata-role-groups.md).

## Connexion à la console ATA
<a id="logging-into-the-ata-console" class="xliff"></a>

1. Sur le serveur du centre ATA, cliquez sur l’icône **Console ATA Microsoft** sur le Bureau ou ouvrez un navigateur pour accéder à la console ATA.

    ![Icône du serveur ATA](media/ata-server-icon.png)

>[!NOTE]
> Vous pouvez également ouvrir un navigateur à partir du centre ATA ou de la passerelle ATA et accéder à l’adresse IP que vous avez configurée dans l’installation du centre ATA pour la console ATA.    

2.  Si l’ordinateur où le centre ATA est installé et l’ordinateur à partir duquel vous tentez d’accéder à la console ATA sont joints à un domaine, ATA prend en charge l’authentification unique intégrée avec l’authentification Windows. Si vous avez déjà ouvert une session sur votre ordinateur, ATA utilise ce jeton pour vous connecter à la console ATA. Vous pouvez également vous connecter à l’aide d’une carte à puce. Vos autorisations dans ATA correspondent à votre [rôle administrateur](ata-role-groups.md).

> [!NOTE]
> Veillez à ouvrir une session sur l’ordinateur à partir duquel vous voulez accéder à la console ATA en utilisant votre nom d’utilisateur et votre mot de passe d’administrateur ATA. Vous pouvez également exécuter votre navigateur en tant qu’un autre utilisateur, ou vous déconnecter de Windows et ouvrir une session avec votre utilisateur administrateur ATA. Pour faire en sorte que la console ATA demande des informations d’identification, accédez à la console en utilisant une adresse IP : vous êtes alors invité à entrer des informations d’identification.

Pour vous connecter à l’aide de l’authentification unique, vérifiez que le site de la console ATA est défini en tant que site intranet local dans votre navigateur et que vous y accédez en utilisant un nom court ou un localhost.

> [!NOTE]
> En plus de la journalisation de chaque alerte d’activité suspecte et d’intégrité, chaque modification de configuration apportée à la console ATA est auditée dans le journal des événements Windows sur l’ordinateur du centre ATA, sous **Journal des applications et des services** puis **Microsoft ATA**. Chaque connexion à la console ATA est également auditée.<br></br>  Les configurations qui affectent la passerelle ATA sont également consignées dans le journal des événements Windows de l’ordinateur de la passerelle ATA. 



## Console ATA
<a id="the-ata-console" class="xliff"></a>

La console ATA fournit un aperçu rapide de toutes les activités suspectes par ordre chronologique. Elle vous permet d’examiner les détails de toutes les activités et d’effectuer des actions en fonction de ces activités. La console affiche également des alertes et des notifications pour signaler des problèmes liés au réseau ATA ou aux nouvelles activités considérées comme suspectes.

Voici les principaux éléments de la console ATA.


### Chronologie des attaques
<a id="attack-time-line" class="xliff"></a>

Il s’agit de la page de destination qui s’affiche par défaut quand vous vous connectez à la console ATA. Par défaut, toutes les activités suspectes ouvertes sont affichées dans la chronologie des attaques. Vous pouvez filtrer la chronologie des attaques de manière à tout afficher ou de manière à afficher uniquement les activités suspectes dont l’état est Ouvert, Résolu ou Ignoré. Vous pouvez également voir le niveau de gravité attribué à chaque activité.

![Image de la chronologie des attaques ATA](media/ATA-Suspicious-Activity-Timeline.jpg)

Pour plus d’informations, consultez [Gestion des activités suspectes](working-with-suspicious-activities.md).

### Barre de notification
<a id="notification-bar" class="xliff"></a>

Quand une activité suspecte est détectée, la barre de notification s’ouvre automatiquement sur la droite. Si de nouvelles activités suspectes ont été détectées depuis la dernière ouverture de session, la barre de notification s’ouvrira après votre connexion. Pour accéder à la barre de notification, vous pouvez cliquer sur la flèche de droite à tout moment.

![Image de la barre de notification ATA](media/notification-bar-1.7.png)

### Filtrage du panneau
<a id="filtering-panel" class="xliff"></a>

Vous pouvez filtrer les activités suspectes qui s’affichent dans la chronologie des attaques ou sous l’onglet Activités suspectes du profil d’entité, selon leur l’état et leur niveau de gravité.

### Barre de recherche
<a id="search-bar" class="xliff"></a>

Le menu supérieur comprend une barre de recherche. Vous pouvez rechercher un utilisateur spécifique, un ordinateur ou un groupe dans ATA. Pour tester la fonction de recherche, commencez à taper un nom.

![Image de la recherche dans la console ATA](media/ATA-console-search.png)

### Centre d’intégrité
<a id="health-center" class="xliff"></a>

Le centre d’intégrité envoie des alertes quand un élément du déploiement ATA ne fonctionne pas correctement.

![Image du centre d’intégrité ATA](media/ATA-Health-Issue.jpg)

Quand votre système rencontre un problème, par exemple une erreur de connectivité ou une passerelle ATA déconnectée, l’icône du centre d’intégrité vous en informe à l’aide d’un point rouge. ![Image du point rouge du centre d’intégrité ATA](media/ATA-Health-Center-Alert-red-dot.png)

Les alertes du centre d’intégrité peuvent être ignorées ou résolues, et classées comme étant d’importance haute, moyenne ou faible. Si vous résolvez une alerte que le service ATA détecte comme étant toujours active, elle sera automatiquement mise dans la liste des alertes ouvertes. Si le système détecte que l’alerte n’a plus de raison d’être (le problème a été résolu), l’alerte est placée automatiquement dans la liste des alertes résolues.

### Profils d’utilisateur et d’ordinateur
<a id="user-and-computer-profiles" class="xliff"></a>

ATA crée un profil pour chaque utilisateur et chaque ordinateur du réseau. Le profil utilisateur contient des informations générales, telles que l’appartenance aux groupes, les connexions récentes et les ressources récemment consultées. Il fournit également une liste des emplacements où l’utilisateur s’est connecté via un VPN. Pour obtenir la liste des appartenances aux groupes considérées comme sensibles, voir ci-dessous.

![Profil utilisateur](media/user-profile.png)

Le profil d’ordinateur contient des informations générales, comme les connexions récentes et les ressources qui ont récemment fait l’objet d’un accès.

![Profil d’ordinateur](media/computer-profile.png)

ATA fournit des informations supplémentaires sur les entités (ordinateurs, appareils, utilisateurs) dans les pages suivantes : Résumé, Activités et Activités suspectes.

Quand ATA n’est pas en mesure de résoudre complètement un profil, il l’indique par une icône représentant un cercle à demi rempli.


![Image du profil non résolu dans ATA](media/ATA-Unresolved-Profile.jpg)

### Groupes sensibles
<a id="sensitive-groups" class="xliff"></a>

Les groupes de la liste suivante sont considérés comme **sensibles** par ATA. Il s’agit de groupes qui seront marqués comme ayant des privilèges d’administrateur et qui déclenchent des alertes correspondant à des comptes sensibles :

- Contrôleurs de domaine d’entreprise en lecture seule 
- Administrateurs du domaine 
- Contrôleurs de domaine 
- Administrateurs de schéma
- Administrateurs de l’entreprise 
- Propriétaires créateurs de la stratégie de groupe 
- Contrôleurs de domaine en lecture seule 
- Administrateurs  
- Utilisateurs avec pouvoir  
- Opérateurs de compte  
- Opérateurs de serveur   
- Opérateurs d’impression
- Opérateurs de sauvegarde
- Duplicateurs 
- Utilisateurs du Bureau à distance 
- Opérateurs de configuration réseau 
- Générateurs d’approbation de forêt entrante 
- Administrateurs DNS 


### Mini-profil
<a id="mini-profile" class="xliff"></a>

Quand une entité est présentée dans la console (par exemple un utilisateur ou un ordinateur), si vous pointez votre souris dessus, un mini-profil s’ouvre automatiquement et affiche les informations suivantes si elles sont disponibles :

![Image du mini-profil dans ATA](media/ATA-mini-profile.jpg)

-   Nom

-   Image

-   E-mail

-   Téléphone

-   Nombre d’activités suspectes par niveau de gravité



## Voir aussi
<a id="see-also" class="xliff"></a>
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
