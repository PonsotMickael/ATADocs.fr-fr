---
title: Installer ATA | Microsoft Advanced Threat Analytics
description: "Lors de l’étape finale de l’installation d’ATA, vous configurez les sous-réseaux du bail à court terme et l’utilisateur Honeytoken."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 76305bc5f55e956c787fe3e8bd954a56f40fc56f


---

# Installer ATA - Étape 6

>[!div class="step-by-step"]
[« Étape 5](install-ata-step5.md)

## Étape 6. Configurer les sous-réseaux du bail à court terme et l’utilisateur Honeytoken
Les sous-réseaux du bail à court terme sont des sous-réseaux dans lesquels l’attribution d’adresses IP change très rapidement, en quelques secondes ou minutes, par exemple les adresses IP utilisées pour vos réseaux privés virtuels (VPN ) et les adresses IP Wi-Fi. Pour entrer la liste des sous-réseaux du bail à court terme utilisés dans votre organisation, procédez comme suit :

1.  Dans la console ATA de la machine de la passerelle ATA, cliquez sur l’icône des paramètres et sélectionnez **Configuration**.

    ![Paramètres de configuration ATA](media/ATA-config-icon.JPG)

2.  Sous **Détection**, entrez ce qui suit pour les sous-réseaux du bail à court terme. Entrez les sous-réseaux du bail à court terme sous un format de notation de barre oblique, par exemple `192.168.0.0/24`, et cliquez sur le signe plus.

3.  Pour les SID de compte Honeytoken, entrez le SID du compte d’utilisateur sans aucune activité réseau, puis cliquez sur le signe plus. Par exemple : `S-1-5-21-72081277-1610778489-2625714895-10511`.

    > [!NOTE]
    > Pour rechercher le SID d’un utilisateur, recherchez l’utilisateur dans la console ATA, puis cliquez sur l’onglet **Informations sur le compte**. 

4.  Configurer les exclusions : vous pouvez configurer des adresses IP à exclure d’activités suspectes spécifiques. Pour plus d’informations, consultez [Gestion des paramètres de la détection ATA](working-with-detection-settings.md).

5.  Cliquez sur **Enregistrer**.

![Enregistrer les modifications](media/ATA-VPN-Subnets.JPG)

Félicitations, vous avez correctement déployé Microsoft Advanced Threat Analytics !

Vérifiez la chronologie des attaques pour afficher les activités suspectes détectées et rechercher des utilisateurs ou des ordinateurs, puis afficher leurs profils.

ATA démarre immédiatement l’analyse pour rechercher les activités suspectes. Certaines activités, telles que certaines liées au comportement, ne sont disponibles qu’une fois qu’ATA a eu le temps de créer des profils de comportements (procédure qui prend au minimum trois semaines).


>[!div class="step-by-step"]
[« Étape 5](install-ata-step5.md)


## Voir aussi

- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Conditions préalables au déploiement d’ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jun16_HO4-->


