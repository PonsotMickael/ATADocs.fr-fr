---
title: "Qu’est-ce que Microsoft Advanced Threat Analytics (ATA) ? | Microsoft Docs"
description: "Explique ce qu’est Microsoft Advanced Threat Analytics (ATA) et quels types d’activités suspectes il peut détecter"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/26/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c338441b37c41b810023ecf5c5ae348651f5ad64
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2017
---
*S’applique à : Advanced Threat Analytics version 1.8*


# Qu’est-ce qu’Advanced Threat Analytics ?
<a id="what-is-advanced-threat-analytics" class="xliff"></a>
Advanced Threat Analytics (ATA) est une plateforme locale qui aide à protéger votre entreprise contre plusieurs types d’attaques informatiques ciblées et de menaces internes avancées.

## Fonctionnement d’ATA
<a id="how-ata-works" class="xliff"></a>

ATA s’appuie sur un moteur d’analyse réseau propriétaire pour capturer et analyser le trafic réseau de plusieurs protocoles (comme Kerberos, DNS, RPC, NTLM et d’autres) pour l’authentification, l’autorisation et la collecte d’informations. Ces informations sont collectées par ATA via :

-   La mise en miroir des ports des contrôleurs de domaine et des serveurs DNS vers la passerelle ATA et/ou
-   Le déploiement d’une passerelle légère ATA directement sur les contrôleurs de domaine

ATA prend les informations de plusieurs sources de données, comme les journaux et les événements de votre réseau, pour apprendre le comportement des utilisateurs et autres entités de l’organisation, puis générer ainsi un profil de leur comportement.
ATA peut recevoir des événements et des journaux des éléments suivants :

-   Intégration SIEM
-   Windows Event Forwarding (WEF)
-   Directement depuis le collecteur d’événements Windows (pour la passerelle légère)


Pour plus d’informations sur l’architecture d’ATA, consultez [Architecture d’ATA](ata-architecture.md).

## Que fait ATA ?
<a id="what-does-ata-do" class="xliff"></a>

La technologie ATA détecte plusieurs activités suspectes, en se focalisant sur différentes phases de la chaîne de cyber-attaque, notamment :

-   Reconnaissance, pendant laquelle les pirates recueillent des informations sur l’architecture de l’environnement et sur les différents composants et entités qui existent. C’est généralement lors de cette phase qu’ils élaborent leur plan pour les étapes suivantes de l’attaque.
-   Cycle de mouvement latéral, pendant lequel un attaquant investit temps et efforts dans la propagation de sa surface d’attaque au sein de votre réseau.
-   Dominance (persistance) de domaine, pendant laquelle un attaquant capture les informations lui permettant de reprendre sa campagne à l’aide d’un ensemble varié de points d’entrée, d’informations d’identification et de techniques. 

Ces phases d’une cyber-attaque sont similaires et prévisibles, quel que soit le type de société visé ou le type d’informations ciblé.
ATA recherche trois principaux types d’attaques : les attaques malveillantes, le comportement anormal, et les risques et problèmes de sécurité.

Les **attaques malveillantes** sont détectées de manière déterministe, en recherchant la liste complète des types d’attaques connus, notamment :

-   Pass-the-Ticket (PtT)
-   Pass-the-Hash (PtH)
-   Overpass-the-Hash
-   Faux PAC (MS14-068)
-   Golden Ticket
-   Réplications malveillantes
-   Reconnaissance
-   Force brute
-   Exécution à distance

Pour obtenir la liste complète des détections et leurs descriptions, consultez [Quelles sont les activités suspectes détectables par ATA ?](ata-threats.md)
ATA détecte ces activités suspectes et expose les informations dans la console ATA, avec une vue claire précisant qui, quoi, quand et comment. Comme vous pouvez le voir, en surveillant ce tableau de bord simple et convivial, vous êtes averti qu’ATA soupçonne qu’une attaque pass-the-ticket a été tentée sur les ordinateurs Client 1 et Client 2 de votre réseau.

 ![exemple d’écran ATA pour pass-the-ticket](media/pass_the_ticket_sa.png)

Un **comportement anormal** est détecté par ATA en effectuant une analyse comportementale et en tirant parti de Machine Learning pour découvrir les activités douteuses et un comportement anormal chez les utilisateurs et les périphériques de votre réseau, notamment :

-   Connexions anormales
-   Menaces inconnues
-   Partage de mot de passe
-   Mouvement latéral
-   Modification de groupes sensibles


Vous pouvez afficher les activités suspectes de ce type dans le tableau de bord ATA. Dans l’exemple suivant, ATA vous avertit quand un utilisateur accède à quatre ordinateurs auxquels il n’accède pas normalement, ce qui peut être une cause d’alerte.

 ![exemple d’écran ATA pour un comportement anormal](media/abnormal-behavior-sa.png) 

ATA détecte également les **risques et problèmes de sécurité**, notamment :

-   Relation de confiance rompue
-   Protocoles faibles
-   Vulnérabilités de protocole connues

Vous pouvez afficher les activités suspectes de ce type dans le tableau de bord ATA. Dans l’exemple suivant, ATA vous signale qu’il existe une relation de confiance rompue entre un ordinateur de votre réseau et le domaine.

  ![exemple d’écran ATA pour une relation de confiance rompue](media/broken-trust-sa.png)


## Problèmes connus
<a id="known-issues" class="xliff"></a>

- Si vous mettez à jour vers ATA 1.7 et immédiatement vers ATA 1.8 sans d’abord mettre à jour les passerelles ATA, vous ne pourrez pas migrer vers ATA 1.8. Vous devez commencer par mettre à jour toutes les passerelles vers la version 1.7.1 ou 1.7.2 avant de mettre à jour le centre ATA vers la version 1.8.

- Si vous choisissez d’effectuer une migration complète, elle peut durer très longtemps en fonction de la taille de la base de données. Quand vous sélectionnez vos options de migration, le temps estimé s’affiche : notez-le bien avant de décider quelle option choisir. 


## Étapes suivantes
<a id="whats-next" class="xliff"></a>

-   Pour plus d’informations sur la façon dont ATA s’intègre à votre réseau, consultez [Architecture ATA](ata-architecture.md).

-   Pour commencer le déploiement d’ATA, consultez [Installer ATA](install-ata-step1.md).

## Voir aussi
<a id="see-also" class="xliff"></a>
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
