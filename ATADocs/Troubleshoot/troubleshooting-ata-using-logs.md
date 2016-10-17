---
title: "Résolution des problèmes liés à ATA à l’aide des journaux ATA | Microsoft ATA"
description: "Décrit comment vous pouvez utiliser les journaux ATA pour résoudre les problèmes"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ee5f60e43f50562e7a7309eafa3b52cf946b0d3b
ms.openlocfilehash: 493f255ae09b51d27079a186bb802f0f3f9706bc


---

*S’applique à : Advanced Threat Analytics version 1.7*



# Résolution des problèmes liés à ATA à l’aide des journaux ATA
Les journaux ATA offrent un aperçu de ce que fait chaque composant ATA à un moment donné.

## Journaux de la passerelle ATA
Dans cette section, chaque référence à la passerelle ATA concerne également la passerelle légère ATA. 

Les journaux de la passerelle ATA se trouvent dans un sous-dossier nommé **Logs** où ATA est installé. L’emplacement par défaut est :  . Dans l’emplacement de l’installation par défaut, il se trouve ici : **C:\Program Files\Microsoft Advanced Threat Analytics\Gateway\Logs**.

La passerelle ATA dispose des journaux suivants :

-   **Microsoft.Tri.Gateway.log** : ce journal contient tout ce qui se produit dans la passerelle ATA (y compris les erreurs et la résolution). Son utilisation principale consiste à obtenir l’état général de toutes les opérations dans l’ordre chronologique dans lequel elles se sont produites.

-   **Microsoft.Tri.Gateway-Resolution.log** : ce journal contient les détails de la résolution des entités visibles dans le trafic par la passerelle ATA. Son utilisation principale consiste à examiner les problèmes de résolution des entités.

-   **Microsoft.Tri.Gateway-Errors.log** : ce journal contient uniquement les erreurs interceptées par la passerelle ATA. Son utilisation principale consiste à exécuter des vérifications d’intégrité et à examiner les problèmes qui doivent être mis en corrélation avec des heures spécifiques.

-   **Microsoft.Tri.Gateway-ExceptionStatistics.log** : ce journal regroupe l’ensemble des erreurs et exceptions similaires, et évalue leur nombre.
    Ce fichier est vide à chaque démarrage du service de passerelle ATA et est mis à jour chaque minute. Il sert principalement à vérifier s’il existe de nouveaux problèmes ou erreurs au niveau de la passerelle ATA (les erreurs étant groupées, il est plus facile de voir rapidement s’il y a de nouveaux problèmes).
-   **Microsoft.Tri.Gateway.Updater.log** : ce journal est utilisé pour le processus de mise à jour de passerelle, qui est responsable de la mise à jour automatique de la passerelle si elle est configurée. Pour la passerelle légère ATA, le processus de mise à jour de passerelle est également responsable des limitations de ressources de la passerelle légère ATA.
-   **Microsoft.Tri.Gateway.Updater-ExceptionStatistics.log** : ce journal regroupe toutes les erreurs et exceptions similaires, et mesure leur nombre. Ce fichier est vide à chaque démarrage du service de mise à jour ATA et est mis à jour chaque minute. Il vous permet de vérifier s’il existe de nouveaux problèmes ou erreurs avec la mise à jour ATA. Les erreurs étant regroupées, il est très facile de savoir rapidement si de nouveaux problèmes ou erreurs ont été détectées.

> [!NOTE]
> Les trois premiers fichiers journaux ont une taille maximale de 50 Mo. Quand cette taille est atteinte, un nouveau fichier journal est ouvert et le précédent est renommé en « &lt;nom_fichier_origine&gt;-Archive-00000 » où le nombre augmente chaque fois qu’il est renommé. Par défaut, s’il existe déjà plus de 10 fichiers du même type, les plus anciens sont supprimés.

## Journaux du centre ATA
Les journaux du centre ATA sont situés dans un sous-dossier appelé **Logs**. Dans l’emplacement de l’installation par défaut, il se trouve ici : **C:\Program Files\Microsoft Advanced Threat Analytics\Center\Logs**.
> [!Note]
> Les journaux de la console ATA qui étaient autrefois sous Journaux IIS se trouvent désormais sous Journaux du centre ATA.

Le centre ATA dispose des journaux suivants :

-   **Microsoft.Tri.Center.log** : ce journal contient tout ce qui se produit dans le centre ATA (y compris les détections et les erreurs). Son utilisation principale consiste à obtenir l’état général de toutes les opérations dans l’ordre chronologique dans lequel elles se sont produites.

-   **Microsoft.Tri.Center-Detection.log** : ce journal contient uniquement les détails des détections du centre ATA. Son utilisation principale consiste à examiner les problèmes de détection.

-   **Microsoft.Tri.Center-Errors.log** : ce journal contient uniquement les erreurs interceptées par le centre ATA. Son utilisation principale consiste à exécuter des vérifications d’intégrité et à examiner les problèmes qui doivent être mis en corrélation avec des heures spécifiques.

-   **Microsoft.Tri.Center-ExceptionStatistics.log** : ce journal regroupe l’ensemble des erreurs et exceptions similaires, et évalue leur nombre.
    Ce fichier est vide lors de chaque démarrage du service du centre ATA et est mis à jour toutes les minutes. Son utilisation principale consiste à déterminer d’éventuels nouveaux problèmes ou erreurs liés au centre ATA. Les erreurs étant regroupées, il est plus facile de vérifier rapidement la présence de nouveaux problèmes ou erreurs.

> [!NOTE]
> Les trois premiers fichiers journaux ont une taille maximale de 50 Mo. Quand cette taille est atteinte, un nouveau fichier journal est ouvert et le précédent est renommé en « &lt;nom_fichier_origine&gt;-Archive-00000 » où le nombre augmente chaque fois qu’il est renommé. Par défaut, s’il existe déjà plus de 10 fichiers du même type, les plus anciens sont supprimés.


## Journaux de déploiement ATA
Les journaux de déploiement ATA sont situés dans le répertoire temp de l’utilisateur qui a installé le produit. Dans l’emplacement de l’installation par défaut, il se trouve ici : **C:\Users\Administrator\AppData\Local\Temp** (ou un répertoire au-dessus de %temp%).

Journaux de déploiement du centre ATA :

-   **Microsoft Advanced Threat Analytics Center_20150601104213.log** : ce journal répertorie les étapes du processus de déploiement du centre ATA. Son utilisation principale consiste à suivre le processus de déploiement du centre ATA.

-   **Microsoft Advanced Threat Analytics Center_20150601104213_0_MongoDBPackage.log** : ce journal répertorie les étapes du processus de déploiement de MongoDB sur le centre ATA. Son utilisation principale consiste à suivre le processus de déploiement de MongoDB.

-   **Microsoft Advanced Threat Analytics Center_20150601104213_1_MsiPackage.log** : ce fichier journal répertorie les étapes du processus de déploiement des fichiers binaires du centre ATA. Son utilisation principale consiste à suivre le déploiement des fichiers binaires du centre ATA.

Journaux de déploiement de la passerelle ATA et de la passerelle légère ATA :

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801.log** : ce journal répertorie les étapes du processus de déploiement de la passerelle ATA. Son utilisation principale consiste à suivre le processus de déploiement de la passerelle ATA.

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801_001_MsiPackage.log** : ce fichier journal répertorie les étapes du processus de déploiement des fichiers binaires de la passerelle ATA. Son utilisation principale consiste à suivre le déploiement des fichiers binaires de la passerelle ATA.


## Voir aussi
- [Configuration requise pour ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planification de la capacité ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurer la collecte d’événements](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configuration du transfert d’événements Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->

