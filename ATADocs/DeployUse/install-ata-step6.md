---
title: "Installer Advanced Threat Analytics - Étape 6 | Microsoft Docs"
description: "Lors de l’étape finale de l’installation d’ATA, vous configurez l’utilisateur Honeytoken."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: da6e72ac5c2966f3e77ce3bef8fe23fcda6770a4
ms.sourcegitcommit: 9b128d6946e32b00f595e00902b9ff95f18141ff
translationtype: HT
---
*S’applique à : Advanced Threat Analytics version 1.7*



# <a name="install-ata---step-6"></a>Installer ATA - Étape 6

>[!div class="step-by-step"]
[« Étape 5](install-ata-step5.md)

## <a name="step-6-configure--ip-address-exclusions-and-honeytoken-user"></a>Étape 6. Configurer des exclusions d’adresses IP et un utilisateur Honeytoken
Avec ATA, vous pouvez exclure des adresses IP spécifiques de deux types de détections : **DNS Reconnaissance** et **Pass-the-Ticket**. 

Par exemple, une **exclusion DNS Reconnaissance** peut être un analyseur de sécurité qui utilise DNS comme mécanisme d’analyse. L’exclusion aide ATA à ignorer ces analyseurs. Un appareil NAT constitue un exemple d’exclusion *Pass-the-Ticket*.    

Avec ATA, vous pouvez aussi configurer un utilisateur Honeytoken servant de piège pour les utilisateurs malveillants. Toute authentification associée à ce compte (normalement dormant) déclenche une alerte.

Pour configurer les éléments suivants, procédez comme suit :

1.  À partir de la console ATA, cliquez sur l’icône des paramètres et sélectionnez **Configuration**.

    ![Paramètres de configuration ATA](media/ATA-config-icon.JPG)

2.  Sous **Exclusions de détection**, entrez l’adresse IP pour *DNS Reconnaissance* ou *Pass-the-Ticket*, puis cliquez sur le signe *plus*.

    ![Enregistrer les modifications](media/ATA-exclusions.png)

3.  Sous **Paramètres de détection**, entrez les SID des comptes Honeytoken et cliquez sur le signe plus (+). Par exemple : `S-1-5-21-72081277-1610778489-2625714895-10511`.

    ![Paramètres de configuration ATA](media/ATA-honeytoken.png)

    > [!NOTE]
    > Pour rechercher le SID d’un utilisateur, recherchez l’utilisateur dans la console ATA, puis cliquez sur l’onglet **Informations sur le compte**. 

4.  Cliquez sur **Enregistrer**.


Félicitations, vous avez correctement déployé Microsoft Advanced Threat Analytics !

Vérifiez la chronologie des attaques pour afficher les activités suspectes détectées et rechercher des utilisateurs ou des ordinateurs, puis afficher leurs profils.

ATA démarre immédiatement l’analyse pour rechercher les activités suspectes. Certaines activités, telles que certaines liées au comportement, ne sont disponibles qu’une fois qu’ATA a eu le temps de créer des profils de comportements (procédure qui prend au minimum trois semaines).

Pour vérifier qu’ATA est opérationnel et qu’il détecte les violations dans votre réseau, vous pouvez consulter le [Scénario de simulation d’attaque Advanced Threat Analytics](https://docs.microsoft.com/enterprise-mobility-security/solutions/ata-attack-simulation-playbook).


>[!div class="step-by-step"]
[« Étape 5](install-ata-step5.md)


## <a name="see-also"></a>Voir aussi

- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration requise pour ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)

