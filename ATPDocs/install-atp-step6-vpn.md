---
title: "Installer Azure - Protection avancée contre les menaces – Étape 6 | Microsoft Docs"
description: "Dans cette étape de la procédure d’installation d’ATP, vous intégrez votre VPN."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/14/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 0d9d2a1d-6c76-4909-b6f9-58523df16d4f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d29210983f3f9f879b462ef760d0b3fe6e53cd5d
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2018
---
*S’applique à : Azure - Protection avancée contre les menaces*



# <a name="install-azure-atp---step-6"></a>Installer Azure ATP – Étape 6

>[!div class="step-by-step"]
[« Étape 5](install-atp-step5.md)
[Étape 7 »](install-atp-step7.md)

## <a name="step-6-integrate-vpn"></a>Étape 6 : Intégrer le VPN

Azure - Protection avancée contre les menaces (ATP) peut collecter des informations de gestion de comptes dans les solutions VPN. Lors de la configuration, la page de profil de l’utilisateur contient des informations sur les connexions VPN, comme les adresses IP et les emplacements d’origine des connexions. Elles viennent en complément du processus d’investigation en fournissant des informations supplémentaires sur l’activité des utilisateurs, ainsi qu’une nouvelle détection pour les connexions VPN anormales. L’appel pour résoudre une adresse IP externe à un emplacement est anonyme. Aucun identificateur personnel n’est envoyé durant cet appel.

Azure ATP s’intègre à votre solution VPN en écoutant les événements de gestion de comptes RADIUS transférés aux capteurs Azure ATP. Ce mécanisme est basé sur la gestion de comptes RADIUS standard ([RFC 2866](https://tools.ietf.org/html/rfc2866)) et les fournisseurs VPN suivants sont pris en charge :

-   Microsoft
-   F5
-   Check Point
-   Cisco ASA

## <a name="prerequisites"></a>Prérequis

Pour activer l’intégration VPN, veillez à définir les paramètres suivants :

-   Ouvrez le port UDP 1813 sur vos capteurs autonomes Azure ATP et votre capteur Azure ATP.


L’exemple ci-dessous utilise Microsoft Routing and Remote Access Server (RRAS) pour décrire le processus de configuration VPN.

Si vous utilisez une solution VPN tierce, consultez sa documentation pour obtenir des instructions sur l’activation de la gestion de comptes RADIUS.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Configurer la gestion de comptes RADIUS sur le système VPN

Effectuez les étapes suivantes sur votre serveur RRAS.
 
1.  Ouvrez la console Routage et accès distant.
2.  Cliquez avec le bouton droit sur le nom du serveur et cliquez sur **Propriétés**.
3.  Sous l’onglet **Sécurité**, sous **Fournisseur de comptes**, sélectionnez **Gestion de comptes RADIUS** et cliquez sur **Configurer**.

    ![Configuration de RADIUS](./media/radius-setup.png)

4.  Dans la fenêtre **Ajouter un serveur RADIUS**, tapez le **nom du serveur** du capteur Azure ATP ou du capteur autonome Azure ATP le plus proche. Sous **Port**, veillez à configurer la valeur par défaut 1813. Cliquez sur **Modifier** et tapez une nouvelle chaîne secrète partagée de caractères alphanumériques que vous pouvez mémoriser. Vous devez la fournir plus loin dans votre configuration Azure ATP. Cochez la case **Envoyer des messages de comptes RADIUS actifs et inactifs** et cliquez sur **OK** dans toutes les boîtes de dialogue ouvertes.
 
     ![Configuration du VPN](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-atp"></a>Configurer le VPN dans ATP

Azure ATP collecte les données VPN qui vous aident à profiler les emplacements depuis lesquels les ordinateurs se connectent au réseau et à pouvoir détecter les connexions VPN anormales.

Pour configurer les données VPN dans ATP :

1.  Dans le portail d’espace de travail Azure ATP, cliquez sur l’icône de configuration (roue dentée), puis sur **VPN**.
 

2.  Activez **Gestion de comptes Radius** et tapez le **Secret partagé** que vous avez configuré sur votre serveur VPN RRAS. Cliquez ensuite sur **Enregistrer**.
 

  ![Configurer le VPN Azure ATP](./media/atp-vpn-radius.png)


Une fois l’activation effectuée, tous les capteurs et capteurs autonomes Azure ATP sont à l’écoute sur le port 1813 pour les événements de gestion de comptes RADIUS. 

L'installation est terminée. 

Une fois que le capteur Azure ATP a reçu les événements VPN et les envoie au service cloud Azure ATP en vue de leur traitement, le profil d’entité indique différents emplacements VPN d’accès et les activités figurant dans le profil indiquent les emplacements.





>[!div class="step-by-step"]
[« Étape 6](install-atp-step5.md)
[Étape 7 »](install-atp-step7.md)


## <a name="see-also"></a>Voir aussi
- [Outil de dimensionnement Azure ATP](http://aka.ms/aatpsizingtool)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)
