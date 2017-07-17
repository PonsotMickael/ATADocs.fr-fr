---
title: "Nouveautés de la version 1.8 d’ATA | Microsoft Docs"
description: "Liste les nouveautés de la version 1.8 d’ATA ainsi que les problèmes connus"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 9592d413-df0e-4cec-8e03-be1ae00ba5dc
ms.reviewer: 
ms.suite: ems
ms.openlocfilehash: 6850c5e8e264a9610e377a9ab4aadca338971ee1
ms.sourcegitcommit: be6bdfa24a9b25a3375a4768d513b93900b3a498
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# Nouveautés de la version 1.8 d’ATA
<a id="whats-new-in-ata-version-18" class="xliff"></a>

La dernière version de la mise à jour d’ATA peut être [téléchargée à partir du Centre de téléchargement](https://www.microsoft.com/download/details.aspx?id=55536) ou la version complète peut être téléchargée à partir du [centre d’évaluation](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).

Ces notes de publication fournissent des informations sur les mises à jour, les nouvelles fonctionnalités, les correctifs de bogue et les problèmes connus de cette version d’Advanced Threat Analytics.



## Détections nouvelles et mises à jour
<a id="new--updated-detections" class="xliff"></a>

- L’implémentation de protocole inhabituelle a été améliorée pour pouvoir détecter le logiciel malveillant WannaCry.

- NOUVEAU ! **Modification anormale des groupes sensibles** : Dans le cadre de la phase d’élévation de privilèges, l’attaquant modifie des groupes avec des privilèges élevés pour avoir accès à des ressources sensibles. ATA détecte désormais quand une modification anormale est effectuée dans un groupe avec privilèges élevés.
- NOUVEAU ! **Échecs d’authentification suspects** (comportement par force brute) : L’attaquant tente d’utiliser la force brute sur des informations d’identification pour compromettre des comptes. ATA déclenche désormais une alerte quand un comportement anormal d’authentification ayant échoué est détecté.   

- **Tentative d’exécution à distance - WMI exec** : L’attaquant peut tenter de contrôler votre réseau en exécutant du code à distance sur votre contrôleur de domaine. ATA a amélioré la détection de l’exécution à distance pour inclure la détection des méthodes WMI qui permettent d’exécuter du code à distance.

- Reconnaissance à l’aide de requêtes du service d’annuaire : Cette détection a été améliorée pour être en mesure d’intercepter les requêtes sur une seule entité sensible et de réduire le nombre de faux positifs générés dans la version précédente. Si vous avez désactivé cette option dans la version 1.7, l’installation de la version 1.8 l’active désormais automatiquement.

- Activité Golden Ticket Kerberos : ATA 1.8 inclut une technique supplémentaire pour détecter les attaques par golden ticket.
    - ATA détecte désormais les activités suspectes dans lesquelles la durée de vie du golden ticket a expiré. Si un ticket Kerberos est utilisé plus longtemps que la durée de vie autorisée, ATA le détecte comme une activité suspecte de création d’un golden ticket.
- Des améliorations ont été apportées aux détections suivantes pour supprimer les faux positifs connus :  
    - Détection de l’élévation des privilèges (faux PAC) 
    - Activité de passage à une version antérieure du chiffrement (Skeleton Key)
    - Implémentation de protocole inhabituelle
    - Relation de confiance rompue

## Triage amélioré des activités suspectes
<a id="improved-triage-of-suspicious-activities" class="xliff"></a>

-   NOUVEAU ! ATA 1.8 vous permet d’exécuter les actions suivantes sur les activités suspectes pendant le processus de triage : 
    - **Exclure des entités** pour qu’elles ne puissent pas lancer des activités suspectes afin d’empêcher ATA de déclencher des alertes quand il détecte des vrais positifs sans gravité (par exemple, un administrateur qui exécute du code à distance ou la détection des analyseurs de sécurité).
    - **Supprimer les activités suspectes récurrentes** dans les alertes.
    - **Supprimer les activités suspectes** de la chronologie des attaques.
-   Le processus de suivi des alertes d’activité suspecte est désormais plus efficace. La chronologie des activités suspectes a été repensée. Dans ATA 1.8, vous pouvez afficher bien plus de d’activités suspectes dans un même écran, avec des informations plus pertinentes pour le triage et l’examen. 

## Nouveaux rapports pour vous aider dans votre analyse
<a id="new-reports-to-help-you-investigate" class="xliff"></a> 
-   NOUVEAU ! Le **rapport de synthèse** a été ajouté pour vous permettre de consulter toutes les données synthétisées par ATA, notamment les activités suspectes, les problèmes d’intégrité et bien plus encore. Vous pouvez même définir un rapport personnalisé généré automatiquement sur une base régulière.
-   NOUVEAU ! Le **rapport des groupes sensibles** a été ajouté pour vous permettre de consulter toutes les modifications apportées dans les groupes sensibles sur une certaine période.


## Améliorations de l’infrastructure
<a id="infrastructure-improvements" class="xliff"></a>

-   Les performances du centre ATA ont été améliorées. Dans ATA 1.8, le centre ATA peut traiter plus de 1 million de paquets par seconde.
-   La passerelle légère ATA peut désormais lire les événements localement, sans qu’il soit nécessaire de configurer le transfert d’événements.
-   Vous pouvez maintenant configurer séparément la messagerie pour surveiller les alertes et les activités suspectes.

## Améliorations apportées à la sécurité
<a id="security-improvements" class="xliff"></a>

-   NOUVEAU ! **Authentification unique pour la gestion d’ATA**. ATA prend en charge l’authentification unique intégrée à l’authentification Windows : si vous avez déjà ouvert une session sur votre ordinateur, ATA utilise ce jeton pour vous connecter à la console ATA. Vous pouvez aussi vous connecter à l’aide d’une carte à puce. Les scripts d’installation sans assistance pour la passerelle ATA et la passerelle légère ATA utilisent désormais le contexte de l’utilisateur connecté, sans demander les informations d’identification.
-   Les privilèges sur le système local ont été supprimés du processus de passerelle ATA, vous pouvez maintenant utiliser des comptes virtuels (disponibles uniquement sur les passerelles ATA autonomes), des comptes de service administrés et des comptes de service administrés de groupe pour exécuter le processus de passerelle ATA.   
-   Des journaux d’audit pour le centre et les passerelles ATA ont été ajoutés et toutes les actions sont maintenant consignées dans le journal des événements Windows.
-   La prise en charge des certificats KSP a été ajoutée pour le centre ATA.




## Voir aussi
<a id="see-also" class="xliff"></a>
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Mise à jour d’ATA vers la version 1.8 : guide de migration](ata-update-1.8-migration-guide.md)

