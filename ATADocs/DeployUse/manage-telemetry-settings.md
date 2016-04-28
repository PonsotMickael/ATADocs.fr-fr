---
# required metadata

title: Gérer les paramètres de télémétrie | Microsoft Advanced Threat Analytics
description: Décrit les données collectées par ATA et explique comment désactiver la collecte de données.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Gérer les paramètres de télémétrie
ATA (Advanced Threat Analytics) collecte des données de télémétrie anonymes sur ATA et les transmet via une connexion HTTPS aux serveurs Microsoft.  Ces données sont utilisées par Microsoft pour améliorer les futures versions d’ATA.

## Données collectées
Les données collectées incluent les éléments suivants :

-   Compteurs de performances du centre ATA et de la passerelle ATA

-   ID de produit après la concession sous licence d’ATA

-   Date de déploiement du centre ATA

-   Nombre de passerelles ATA déployées

-   Informations Active Directory suivantes :

    -   ID du domaine dont le nom correspond au premier domaine lors d’un tri par ordre alphabétique

    -   Nombre de contrôleurs de domaine

    -   Nombre de contrôleurs de domaine surveillés par ATA via la mise en miroir des ports

    -   Nombre de sites

    -   Nombre d’ordinateurs

    -   Nombre de groupes

    -   Nombre d’utilisateurs

-   Activités suspectes : les données suivantes sont collectées pour chaque activité suspecte :

    (Les noms d’ordinateurs, noms d’utilisateurs et adresses IP ne sont **pas** collectés)

    -   Type d’activité suspecte

    -   ID d’activité suspecte

    -   État

    -   Heures de début et de fin

    -   Entrée fournie

### Désactiver la collecte de données
Pour arrêter la collecte et l’envoi de données de télémétrie à Microsoft, procédez comme suit.

1.  Connectez-vous à la console ATA, cliquez sur les trois points dans la barre d’outils, puis sélectionnez **À propos de**.

2.  Décochez la case **Envoyez-nous des informations d’utilisation pour nous aider à améliorer votre expérience utilisateur à l’avenir**.

## Voir aussi
- [Nouveautés de la version 1.5](whats-new-version-1.5.md)
- [Nouveautés de la version 1.4](whats-new-version-1.4.md)
- [Pour obtenir de l’aide, consultez notre forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


