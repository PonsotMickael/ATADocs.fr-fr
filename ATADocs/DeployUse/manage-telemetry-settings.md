---
title: "Gérer les paramètres de télémétrie | Microsoft ATA"
description: "Décrit les données collectées par ATA et explique comment désactiver la collecte de données."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: b2b1ae963e8786b77c2fd124a612305be2c6b0bf


---

# Gérer les paramètres de télémétrie
ATA (Advanced Threat Analytics) collecte des données de télémétrie rendues anonymes sur ATA et les transmet via une connexion HTTPS aux serveurs Microsoft.  Ces données sont utilisées par Microsoft pour améliorer les futures versions d’ATA.

## Données collectées
Les données rendues anonymes collectées incluent les éléments suivants :

-   Compteurs de performances du centre ATA et de la passerelle ATA

-   ID de produit des copies sous licence d’ATA

-   Date de déploiement du centre ATA

-   Nombre de passerelles ATA déployées

-   Informations Active Directory rendues anonymes suivantes :

    -   ID du domaine dont le nom correspond au premier domaine lors d’un tri par ordre alphabétique

    -   Nombre de contrôleurs de domaine

    -   Nombre de contrôleurs de domaine surveillés par ATA via la mise en miroir des ports

    -   Nombre de sites

    -   Nombre d’ordinateurs

    -   Nombre de groupes

    -   Nombre d’utilisateurs

-   Activités suspectes : les données rendues anonymes suivantes sont collectées pour chaque activité suspecte :

    (Les noms d’ordinateurs, noms d’utilisateurs et adresses IP ne sont **pas** collectés)

    -   Type d’activité suspecte

    -   ID d’activité suspecte

    -   État

    -   Heures de début et de fin

    -   Entrée fournie

### Désactiver la collecte de données
Procédez comme suit pour arrêter la collecte et l’envoi de données de télémétrie à Microsoft :

1.  Connectez-vous à la console ATA, cliquez sur les trois points dans la barre d’outils, puis sélectionnez **À propos de**.

2.  Décochez la case **Envoyez-nous des informations d’utilisation pour nous aider à améliorer votre expérience utilisateur à l’avenir**.

## Voir aussi
- [Nouveautés de la version 1.6](/advanced-threat-analytics/understand-explore/whats-new-version-1.6)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


