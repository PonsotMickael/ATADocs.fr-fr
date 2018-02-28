---
title: "Installer Azure - Protection avancée contre les menaces – Étape 7 | Microsoft Docs"
description: "Lors de l’étape finale de l’installation d’Azure ATP, vous configurez l’utilisateur Honeytoken."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 1ad5e923-9bbd-4f56-839a-b11a9f387d4b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: bef13d0f4799a4483eda6604a8ed96befaa13508
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2018
---
*S’applique à : Azure - Protection avancée contre les menaces*



# <a name="install-azure-atp---step-7"></a>Installer Azure ATP – Étape 7

>[!div class="step-by-step"]
[« Étape 6](install-atp-step6-vpn.md)
[Étape 8 »](install-atp-step8-samr.md)

## <a name="step-7-configure-detection-exclusions-and-honeytoken-user"></a>Étape 7. Configurer des exclusions d’adresses IP et l’utilisateur honeytoken

Azure ATP permet d’exclure des adresses IP ou des utilisateurs spécifiques d’un certain nombre de détections. 

Par exemple, une **exclusion DNS Reconnaissance** peut être un analyseur de sécurité qui utilise DNS comme mécanisme d’analyse. L’exclusion permet à Azure ATP d’ignorer ces analyseurs.  

Avec Azure ATP, vous pouvez aussi configurer un utilisateur Honeytoken servant de piège pour les utilisateurs malveillants. Toute authentification associée à ce compte (normalement dormant) déclenche une alerte.

Pour configurer ceci, procédez comme suit :

1.  À partir du portail d’espace de travail Azure ATP, cliquez sur l’icône des paramètres et sélectionnez **Configuration**.

    ![Paramètres de configuration d’Azure ATP](media/atp-config-menu.png)

2.  Sous **Détection**, cliquez sur **Étiquettes d’entité**.

3. Sous **Comptes Honeytoken**, entrez le nom du compte Honeytoken et cliquez sur le signe **+**. Le champ des comptes Honeytoken peut faire l’objet d’une recherche et affiche automatiquement les entités dans votre réseau. Cliquez sur **Enregistrer**.

   ![Honeytoken](media/honeytoken-sensitive.png)

4. Cliquez sur **Exclusions**. Pour chaque type de menace, entrez un compte d’utilisateur ou une adresse IP à exclure de la détection de ces menaces, et cliquez sur le signe *plus*. Le champ **Ajouter une entité** (utilisateur ou ordinateur) peut faire l’objet d’une recherche et est automatiquement renseigné avec les entités de votre réseau. Pour plus d’informations, consultez [Exclusion d’entités des détections](excluding-entities-from-detections.md) et le [guide des activités suspectes](suspicious-activity-guide.md).

   ![Exclusions](media/exclusions.png)

5.  Cliquez sur **Enregistrer**.


Félicitations, vous avez correctement déployé Azure - Protection avancée contre les menaces !

Vérifiez la chronologie des attaques pour afficher les activités suspectes détectées et rechercher des utilisateurs ou des ordinateurs, puis afficher leurs profils.

Azure ATP démarre immédiatement l’analyse pour rechercher les activités suspectes. Certaines détections, telles que les modifications anormales de groupe, nécessitent une période d’apprentissage et ne sont pas disponibles immédiatement après le déploiement d’Azure ATP.



>[!div class="step-by-step"]
[« Étape 6](install-atp-step6-vpn.md)
[Étape 8 »](install-atp-step8-samr.md)

## <a name="see-also"></a>Voir aussi
- [Outil de dimensionnement Azure ATP](http://aka.ms/aatpsizingtool)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)
