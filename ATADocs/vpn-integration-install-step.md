---
title: "Installer Advanced Threat Analytics - Étape 7 | Microsoft Docs"
description: "Dans cette étape d’installation d’ATA, vous intégrez votre VPN."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/9/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c02649a6acb6a083145ba81b3b9c1647e7f8ea2a
ms.sourcegitcommit: e9f2bfd610b7354ea3fef749275f16819d60c186
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2017
---
*S’applique à : Advanced Threat Analytics version 1.8*



# <a name="install-ata---step-7"></a>Installer ATA - Étape 7

>[!div class="step-by-step"]
[« Étape 5](install-ata-step5.md)
[Étape 8 »](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>Étape 7. Intégrer le VPN

### <a name="configuring-vpn"></a>Configuration du VPN

ATA collecte les données VPN qui vous aident à profiler les emplacements depuis lesquels les ordinateurs se connectent au réseau et à pouvoir détecter les connexions VPN anormales.

Pour configurer les données VPN dans ATA :

1. Accédez à **Configuration**, puis cliquez sur l’onglet **VPN**.

2. Entrez le **secret partagé de compte** de votre serveur RADIUS. Pour obtenir le secret partagé, consultez la documentation de votre VPN.

 ![Configurer le VPN ATA](media/vpn.png)

3.  Une fois ce paramètre activé, toutes les passerelles et passerelles légères ATA écoutent le port 1813 pour les événements comptables RADIUS. 

4.  Les événements comptables RADIUS de VPN doivent être transférés vers une passerelle ATA ou une passerelle légère ATA après la configuration.

5.  Une fois que la passerelle ATA reçoit les événements VPN et les envoie au centre ATA pour traitement, le centre ATA nécessite une connectivité Internet pour permettre au port HTTPS 443 de résoudre les adresses IP externes dans les événements VPN pour leur géolocalisation.

L’appel pour résoudre une adresse IP externe à un emplacement est anonyme. Aucun identificateur personnel n’est envoyé durant cet appel.

Les fournisseurs VPN pris en charge sont les suivants :
- Microsoft
- F5
- Check Point
- Cisco ASA




>[!div class="step-by-step"]
[« Étape 6](install-ata-step5.md)
[Étape 8 »](install-ata-step7.md)



## <a name="related-videos"></a>Vidéos connexes
- [Vue d’ensemble du déploiement ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Sélection du type de passerelle ATA approprié](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Voir aussi
- [Guide de déploiement ATA POC](http://aka.ms/atapoc)
- [Outil de dimensionnement ATA](http://aka.ms/atasizingtool)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration requise pour ATA](ata-prerequisites.md)

