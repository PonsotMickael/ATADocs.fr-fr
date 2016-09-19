---
title: Installer ATA | Microsoft ATA
description: "Lors de l’étape finale de l’installation d’ATA, vous configurez les sous-réseaux du bail à court terme et l’utilisateur Honeytoken."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/28/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e3b690767e5c6f5561a97a73eccfbf50ddb04148
ms.openlocfilehash: 57fe1272e95f69ef9d614505bbef0bb6c1d8ccb6


---

*S’applique à : Advanced Threat Analytics version 1.7*



# Installer ATA - Étape 6

>[!div class="step-by-step"]
[« Étape 5](install-ata-step5.md)

## Étape 6. Configurer des exclusions d’adresses IP et un utilisateur Honeytoken
Avec ATA, vous pouvez exclure des adresses IP et des sous-réseaux IP spécifiques de deux types de détections : **DNS Reconnaissance** et **Pass-the-Ticket**. 

Par exemple, une **exclusion DNS Reconnaissance** peut être un analyseur de sécurité qui utilise DNS comme mécanisme d’analyse. L’exclusion aide ATA à ignorer ces analyseurs. Un appareil NAT constitue un exemple d’exclusion *Pass-the-Ticket*.    

Avec ATA, vous pouvez aussi configurer un utilisateur Honeytoken servant de piège pour les utilisateurs malveillants. Toute authentification associée à ce compte (normalement dormant) déclenche une alerte.

Pour configurer les éléments suivants, procédez comme suit :

1.  À partir de la console ATA, cliquez sur l’icône des paramètres et sélectionnez **Configuration**.

    ![Paramètres de configuration ATA](media/ATA-config-icon.JPG)

2.  Sous **Exclusions de détection**, entrez ce qui suit pour les adresses IP *DNS Reconnaissance* ou *Pass-the-Ticket*. Utilisez le format CIDR, par exemple : `192.168.1.0/24` et cliquez sur le signe *plus*.

    ![Enregistrer les modifications](media/ATA-exclusions.png)

3.  Sous **Paramètres de détection**, entrez les SID des comptes Honeytoken et cliquez sur le signe plus (+). Par exemple : `S-1-5-21-72081277-1610778489-2625714895-10511`.

    ![Paramètres de configuration ATA](media/ATA-honeytoken.png)

    > [!NOTE]
    > Pour rechercher le SID d’un utilisateur, recherchez l’utilisateur dans la console ATA, puis cliquez sur l’onglet **Informations sur le compte**. 

4.  Cliquez sur **Enregistrer**.


Félicitations, vous avez correctement déployé Microsoft Advanced Threat Analytics !

Vérifiez la chronologie des attaques pour afficher les activités suspectes détectées et rechercher des utilisateurs ou des ordinateurs, puis afficher leurs profils.

ATA démarre immédiatement l’analyse pour rechercher les activités suspectes. Certaines activités, telles que certaines liées au comportement, ne sont disponibles qu’une fois qu’ATA a eu le temps de créer des profils de comportements (procédure qui prend au minimum trois semaines).


>[!div class="step-by-step"]
[« Étape 5](install-ata-step5.md)


## Voir aussi

- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Conditions préalables au déploiement d’ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Aug16_HO5-->


