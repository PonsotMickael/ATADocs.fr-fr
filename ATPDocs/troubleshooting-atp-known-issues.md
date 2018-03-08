---
title: "Dépannage des problèmes connus d’Azure ATP | Microsoft Docs"
description: "Décrit comment résoudre les problèmes d’Azure ATP."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/6/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2895a38e2328fb7de4fe7f47d00c4e40ac854e74
ms.sourcegitcommit: 84556e94a3efdf20ca1ebf89a481550d7f8f0f69
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/08/2018
---
*S’applique à : Azure - Protection avancée contre les menaces*


# <a name="troubleshooting-azure-atp-known-issues"></a>Dépannage des problèmes connus d’Azure ATP 

## <a name="azure-atp-sensor-nic-teaming-issue"></a>Problème d’association de cartes réseau du capteur Azure ATP

Si vous essayez d’installer le capteur ATP sur un ordinateur configuré avec une carte d’association de cartes réseau, vous recevez une erreur d’installation. Si vous souhaitez installer le capteur ATP sur un ordinateur configuré avec une association de cartes réseau, suivez ces instructions :

Si vous n’avez pas encore installé le capteur :

1.  Téléchargez Npcap à partir du site [https://nmap.org/npcap/](https://nmap.org/npcap/).
2.  Désinstallez WinPcap, s’il était installé.
3.  Installez Npcap avec les options suivantes : loopback_support=no & winpcap_mode=yes
4.  Installez le package du capteur.

Si vous avez déjà installé le capteur :

1.  Téléchargez Npcap à partir du site [https://nmap.org/npcap/](https://nmap.org/npcap/).
2.  Désinstallez le capteur.
3.  Désinstallez WinPcap.
4.  Installez Npcap avec les options suivantes : loopback_support=no & winpcap_mode=yes
5.  Réinstallez le package du capteur.

## <a name="windows-defender-atp-integration-issue"></a>Problème d’intégration Windows Defender ATP

Azure - Protection avancée contre les menaces vous permet d’intégrer Azure ATP et Windows Defender ATP. L’intégration est actuellement activée uniquement si vous êtes client de la préversion limitée de Windows Defender ATP. 

## <a name="vmware-virtual-machine-sensor-issue"></a>Problème de capteur pour la machine virtuelle VMware

Si vous avez un capteur Azure ATP sur des machines virtuelles VMware, vous pouvez recevoir l’alerte de surveillance **Une partie du trafic réseau n’est pas analysée**. Ce scénario se produit à cause d’une différence de configuration dans VMware.

Pour résoudre ce problème :

Définissez les paramètres suivants avec les valeurs **0** ou **Désactivé** dans la configuration de carte réseau de la machine virtuelle : TsoEnable, LargeSendOffload, TSO Offload, Giant TSO Offload.
> [!NOTE]
> Pour les capteurs Azure ATP, il vous suffit de désactiver **IPv4 TSO Offload** dans la configuration de la carte réseau.

 ![Problème de capteur VMware](./media/vm-sensor-issue.png)

## <a name="see-also"></a>Voir aussi
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Planification de la capacité Azure ATP](atp-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)