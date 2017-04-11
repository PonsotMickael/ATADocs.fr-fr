---
title: "Résolution des problèmes d’Advanced Threat Analytics en utilisant les journaux | Microsoft Docs"
description: "Décrit comment vous pouvez utiliser les journaux ATA pour résoudre les problèmes"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 5bde3ff8abbdace3c56bb86b8889b53320470b00
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*S’applique à : Advanced Threat Analytics version 1.7*



# <a name="troubleshooting-ata-using-the-ata-logs"></a>Résolution des problèmes liés à ATA à l’aide des journaux ATA
Les journaux ATA offrent un aperçu de ce que fait chaque composant ATA à un moment donné.

## <a name="ata-gateway-logs"></a>Journaux de la passerelle ATA
Dans cette section, chaque référence à la passerelle ATA concerne également la passerelle légère ATA. 

Les journaux de la passerelle ATA se trouvent dans un sous-dossier nommé **Logs** où ATA est installé. L’emplacement par défaut est : **C:\Program Files\Microsoft Advanced Threat Analytics\**. Dans l’emplacement de l’installation par défaut, il se trouve ici :**C:\Program Files\Microsoft Advanced Threat Analytics\Gateway\Logs**.

La passerelle ATA dispose des journaux suivants :

-   **Microsoft.Tri.Gateway.log** : ce journal contient tout ce qui se produit dans la passerelle ATA (y compris les erreurs et la résolution). Son utilisation principale consiste à obtenir l’état général de toutes les opérations dans l’ordre chronologique dans lequel elles se sont produites.

-   **Microsoft.Tri.Gateway-Resolution.log** : ce journal contient les détails de la résolution des entités visibles dans le trafic par la passerelle ATA. Son utilisation principale consiste à examiner les problèmes de résolution des entités.

-   **Microsoft.Tri.Gateway-Errors.log** : ce journal contient uniquement les erreurs interceptées par la passerelle ATA. Son utilisation principale consiste à exécuter des vérifications d’intégrité et à examiner les problèmes qui doivent être mis en corrélation avec des heures spécifiques.

-   **Microsoft.Tri.Gateway-ExceptionStatistics.log** : ce journal regroupe l’ensemble des erreurs et exceptions similaires, et évalue leur nombre.
    Ce fichier est vide lors de chaque démarrage du service de la passerelle ATA et est mis à jour toutes les minutes. Son utilisation principale consiste à déterminer d’éventuels nouveaux problèmes ou erreurs liés à la passerelle ATA. Les erreurs étant regroupées, il est plus facile de déterminer rapidement la présence de nouveaux problèmes.
-    **Microsoft.Tri.Gateway.Updater.log** : ce journal est utilisé pour le processus de mise à jour de passerelle, qui est responsable de la mise à jour automatique de la passerelle si elle est configurée. Pour la passerelle légère ATA, le processus de mise à jour de passerelle est également responsable des limitations de ressources de la passerelle légère ATA.
-    **Microsoft.Tri.Gateway.Updater-ExceptionStatistics.log** : ce journal regroupe toutes les erreurs et exceptions similaires, et mesure leur nombre. Ce fichier est vide à chaque démarrage du service de mise à jour ATA et est mis à jour chaque minute. Il vous permet de vérifier s’il existe de nouveaux problèmes ou erreurs avec la mise à jour ATA. Les erreurs étant regroupées, il est très facile de savoir rapidement si de nouveaux problèmes ou erreurs ont été détectées.

> [!NOTE]
> Les trois premiers fichiers journaux ont une taille maximale de 50 Mo. Quand cette taille est atteinte, un nouveau fichier journal est ouvert et le précédent est renommé en « &lt;nom_fichier_origine&gt;-Archive-00000 » où le nombre augmente chaque fois qu’il est renommé. Par défaut, s’il existe déjà plus de 10 fichiers du même type, les plus anciens sont supprimés.

## <a name="ata-center-logs"></a>Journaux du centre ATA
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


## <a name="ata-deployment-logs"></a>Journaux de déploiement ATA
Les journaux de déploiement ATA sont situés dans le répertoire temp de l’utilisateur qui a installé le produit. Dans l’emplacement de l’installation par défaut, il se trouve ici : **C:\Users\Administrator\AppData\Local\Temp** (ou un répertoire au-dessus de %temp%).

Journaux de déploiement du centre ATA :

-   **Microsoft Advanced Threat Analytics Center_YYYYMMDDHHMMSS.log** : ce journal répertorie les étapes du processus de déploiement du centre ATA. Son utilisation principale consiste à suivre le processus de déploiement du centre ATA.

-   **Microsoft Advanced Threat Analytics Center_YYYYMMDDHHMMSS_0_MongoDBPackage.log** : ce journal répertorie les étapes du processus de déploiement de MongoDB sur le centre ATA. Son utilisation principale consiste à suivre le processus de déploiement de MongoDB.

-   **Microsoft Advanced Threat Analytics Center_YYYYMMDDHHMMSS_1_MsiPackage.log** : ce fichier journal répertorie les étapes du processus de déploiement des fichiers binaires du centre ATA. Son utilisation principale consiste à suivre le déploiement des fichiers binaires du centre ATA.

Journaux de déploiement de la passerelle ATA et de la passerelle légère ATA :

-   **Microsoft Advanced Threat Analytics Gateway_YYYYMMDDHHMMSS.log** : ce journal répertorie les étapes du processus de déploiement de la passerelle ATA. Son utilisation principale consiste à suivre le processus de déploiement de la passerelle ATA.

-   **Microsoft Advanced Threat Analytics Gateway_YYYYMMDDHHMMSS_001_MsiPackage.log** : ce fichier journal répertorie les étapes du processus de déploiement des fichiers binaires de la passerelle ATA. Son utilisation principale consiste à suivre le déploiement des fichiers binaires de la passerelle ATA.


## <a name="see-also"></a>Voir aussi
- [Prérequis au déploiement d’ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planification de la capacité d’ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurer la collecte d’événements](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configuration du transfert d’événements Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
