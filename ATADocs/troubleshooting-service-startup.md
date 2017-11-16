---
title: "Résolution des problèmes d’Advanced Threat Analytics en utilisant les journaux | Microsoft Docs"
description: "Décrit comment vous pouvez utiliser les journaux ATA pour résoudre les problèmes"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 125376b1e3530481a3b9f62c4661dd10dce13f22
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/07/2017
---
*S’applique à : Advanced Threat Analytics version 1.8*



# <a name="troubleshooting-ata-center-service-startup"></a>Résolution des problèmes de démarrage du service Centre ATA

Si votre centre ATA ne démarre pas, effectuez la procédure de dépannage suivante :

1.  Exécutez la commande Windows PowerShell suivante : `Get-Service Pla | Select Status` pour vérifier que le service de compteur de performances est en cours d’exécution. Si ce n’est pas le cas, c’est qu’il s’agit d’un problème de la plateforme, et vous devez faire en sorte que ce service fonctionne à nouveau.
2.  S’il était en cours d’exécution, essayez de le redémarrer et vérifiez si cela résout le problème : `Restart-Service Pla`
3.  Essayez de créer manuellement un nouveau collecteur de données (n’importe quel collecteur fera l’affaire, vous pouvez même collecter par exemple l’utilisation de l’UC de l’ordinateur).
S’il peut démarrer, la plateforme est probablement opérationnelle. Sinon, il s’agit toujours d’un problème de plateforme.

4.  Essayez de recréer manuellement le collecteur de données ATA à l’aide d’une invite de commandes avec élévation de privilèges en exécutant ces commandes :

        sc stop ATACenter
        logman stop "Microsoft ATA Center"
        logman export "Microsoft ATA Center" -xml c:\center.xml
        logman delete "Microsoft ATA Center"
        logman import "Microsoft ATA Center" -xml c:\center.xml
        logman start "Microsoft ATA Center"
        sc start ATACenter



## <a name="see-also"></a>Voir aussi
- [Prérequis au déploiement d’ATA](ata-prerequisites.md)
- [Planification de la capacité d’ATA](ata-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
