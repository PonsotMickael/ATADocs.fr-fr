---
title: "Résolution des problèmes d’Advanced Threat Analytics en utilisant les journaux | Microsoft Docs"
description: "Décrit comment vous pouvez utiliser les journaux ATA pour résoudre les problèmes"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/26/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1291281273188a21b61b29f06a5220eee589767c
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
*S’applique à : Advanced Threat Analytics version 1.8*



# Résolution des problèmes de démarrage du service Centre ATA
<a id="troubleshooting-ata-center-service-startup" class="xliff"></a>

Si votre centre ATA ne démarre pas, effectuez la procédure de dépannage suivante :

1.  Exécutez la commande Windows PowerShell suivante : Get-Service Pla | Select Status pour vérifier que le service de compteur de performances est en cours d’exécution. Si ce n’est pas le cas, c’est qu’il s’agit d’un problème de la plateforme, et vous devez faire en sorte que ce service fonctionne à nouveau.
2.  S’il était en cours d’exécution, essayez de le redémarrer et vérifiez si cela résout le problème : Restart-Service Pla
3.  Essayez de créer manuellement un nouveau collecteur de données (n’importe quel collecteur fera l’affaire, vous pouvez même collecter par exemple l’utilisation de l’UC de l’ordinateur).
S’il peut démarrer, c’est que la plateforme ne pose probablement pas problème. Dans le cas contraire, c’est qu’il s’agit d’un problème de plateforme.

4.  Essayez de recréer manuellement le collecteur de données ATA en utilisant une invite de commandes avec élévation de privilèges pour exécuter ces commandes : sc stop ATACenter logman stop "Microsoft ATA Center" logman export "Microsoft ATA Center" -xml c:\center.xml logman delete "Microsoft ATA Center" logman import "Microsoft ATA Center" -xml c:\center.xml logman start "Microsoft ATA Center" sc start ATACenter



## Voir aussi
<a id="see-also" class="xliff"></a>
- [Prérequis au déploiement d’ATA](ata-prerequisites.md)
- [Planification de la capacité d’ATA](ata-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
