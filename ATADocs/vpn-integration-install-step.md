---
title: "Installer Advanced Threat Analytics - Étape 7 | Microsoft Docs"
description: "Dans cette étape d’installation d’ATA, vous intégrez votre VPN."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/31/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 748121a709ac05756edf34e04e13b996190e9711
ms.sourcegitcommit: b951c64228d4f165ee1fcc5acc0ad6bb8482d6a2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
*S’applique à : Advanced Threat Analytics version 1.8*



# <a name="install-ata---step-7"></a>Installer ATA - Étape 7

>[!div class="step-by-step"]
[« Étape 5](install-ata-step5.md)
[Étape 8 »](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>Étape 7. Intégrer le VPN

Microsoft Advanced Threat Analytics (ATA) version 1.8 peut collecter des informations de gestion de comptes dans les solutions VPN. Lors de la configuration, la page de profil de l’utilisateur contient des informations sur les connexions VPN, comme les adresses IP et les emplacements d’origine des connexions. Elles viennent en complément du processus d’investigation en fournissant des informations supplémentaires sur l’activité des utilisateurs. L’appel pour résoudre une adresse IP externe à un emplacement est anonyme. Aucun identificateur personnel n’est envoyé durant cet appel.

ATA s’intègre avec votre solution VPN en écoutant les événements de gestion de comptes RADIUS transférés aux passerelles ATA. Ce mécanisme est basé sur la gestion de comptes RADIUS standard ([RFC 2866](https://tools.ietf.org/html/rfc2866)) et les fournisseurs VPN suivants sont pris en charge :

-   Microsoft
-   F5
-   Check Point
-   Cisco ASA

## <a name="prerequisites"></a>Prérequis

Pour activer l’intégration VPN, veillez à définir ce qui suit :

-   Ouvrir le port UDP 1813 sur vos passerelles ATA et vos passerelles légères ATA.

-   Connecter le centre ATA à Internet afin qu’il puisse interroger l’emplacement des adresses IP entrantes.

Dans l’exemple ci-dessous, nous utilisons Microsoft Routing and Remote Access Server (RRAS) pour décrire le processus de configuration VPN.

Si vous utilisez une solution VPN tierce, consultez sa documentation pour obtenir des instructions sur l’activation de la gestion de comptes RADIUS.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Configurer la gestion de comptes RADIUS sur le système VPN

Effectuez les opérations suivantes sur votre serveur RRAS.
 
1.  Ouvrez la console Routage et accès distant.
2.  Cliquez avec le bouton droit sur le nom du serveur et cliquez sur **Propriétés**.
3.  Sous l’onglet **Sécurité**, sous **Fournisseur de comptes**, sélectionnez **Gestion de comptes RADIUS** et cliquez sur **Configurer**.

    ![Configuration de RADIUS](./media/radius-setup.png)

4.  Dans la fenêtre **Ajouter un serveur RADIUS**, tapez le **Nom du serveur** de la passerelle ATA ou de la passerelle légère ATA la plus proche. Sous **Port**, veillez à configurer la valeur par défaut 1813. Cliquez sur **Modifier** et tapez une nouvelle chaîne secrète partagée de caractères alphanumériques que vous pouvez mémoriser. Vous devrez la fournir plus loin dans votre configuration ATA. Cochez la case **Envoyer des messages de comptes RADIUS actifs et inactifs** et cliquez sur **OK** dans toutes les boîtes de dialogue ouvertes.
 
     ![Configuration du VPN](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-ata"></a>Configurer le VPN dans ATA

ATA collecte les données VPN qui vous aident à profiler les emplacements depuis lesquels les ordinateurs se connectent au réseau et à pouvoir détecter les connexions VPN anormales.

Pour configurer les données VPN dans ATA :

1.  Dans la console ATA, ouvrez la page Configuration d’ATA et accédez à **VPN**.
 
  ![Menu de configuration ATA](./media/config-menu.png)

2.  Activez **Gestion de comptes Radius** et tapez le **Secret partagé** que vous avez configuré sur votre serveur VPN RRAS. Cliquez ensuite sur **Enregistrer**.
 

  ![Configurer le VPN ATA](./media/vpn.png)


Une fois l’activation effectuée, toutes les passerelles et passerelles légères ATA écoutent le port 1813 pour les événements de gestion de comptes RADIUS. 

Votre configuration est terminée et vous pouvez voir maintenant l’activité VPN dans la page de profil de l’utilisateur :
 
   ![Configuration du VPN](./media/vpn-user.png)

Une fois que la passerelle ATA reçoit les événements VPN et les envoie au centre ATA pour traitement, le centre ATA nécessite une connectivité Internet pour permettre au port HTTPS 443 de résoudre les adresses IP externes dans les événements VPN pour leur géolocalisation.





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

