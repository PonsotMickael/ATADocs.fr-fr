---
title: "Gestion des activités suspectes dans Advanced Threat Analytics | Microsoft Docs"
description: "Explique comment passer en revue les activités suspectes identifiées par ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 44d7c899-816c-4f7f-91d3-84a09d291a24
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: c94f61853aa45d45600cbcc0ba0a5a64adc6fd3f


---

*S’applique à : Advanced Threat Analytics version 1.7*



# <a name="working-with-suspicious-activities"></a>Gestion des activités suspectes
Cette rubrique explique les principes de base d’Advanced Threat Analytics.

## <a name="review-suspicious-activities-on-the-attack-time-line"></a>Passer en revue les activités suspectes sur la chronologie des attaques
Une fois connecté à la console ATA, la **Chronologie des activités suspectes** s’ouvre automatiquement. Les activités suspectes sont répertoriées par ordre chronologique, avec les plus récentes en haut de la liste.
Chaque activité suspecte comporte les informations suivantes :

-   Les entités impliquées, y compris les utilisateurs, les ordinateurs, les serveurs, les contrôleurs de domaine et les ressources

-   Les date et heure et la durée des activités suspectes

-   Gravité de l’activité suspecte (haute, moyenne ou faible)

-   État : Ouvert, Résolu ou Ignoré.

-   La capacité à :

    -   Partager l’activité suspecte avec d’autres personnes de votre entreprise par e-mail.

    -   Exporter l’activité suspecte dans Excel.

    -   Ajouter une note à l’activité suspecte.

    -   Fournir des commentaires sur l’activité suspecte.

-   Fournir des recommandations sur la gestion de l’activité suspecte.

> [!NOTE]
> -   Quand vous pointez votre souris sur un utilisateur ou un ordinateur, un mini-profil d’entité s’affiche avec des informations complémentaires sur l’entité, notamment le nombre d’activités suspectes auxquelles est liée l’entité.
> -   Quand vous cliquez sur une entité, vous êtes dirigé vers le profil d’entité de l’utilisateur ou l’ordinateur.

![Image de la chronologie des activités suspectes ATA](media/ATA-Suspicious-Activity-Timeline.JPG)

## <a name="filter-suspicious-activities-list"></a>Filtrer la liste des activités suspectes
Pour filtrer la liste des activités suspectes :

1.  Dans le volet **Filtrer par** sur le côté gauche de l’écran, sélectionnez l’une des options suivantes : **Tout**, **Ouvert**, **Résolu** ou **Ignoré**.

2.  Pour filtrer la liste, sélectionnez **Haute**, **Moyenne** ou **Faible**.

**Gravité des activités suspectes**

-   **Faible**

    Correspond aux activités suspectes pouvant conduire à des attaques durant lesquelles des utilisateurs ou logiciels malveillants accèdent aux données d’une entreprise.

-   **Moyenne**

    Correspond aux activités suspectes qui peuvent faire courir un risque à certaines identités en permettant des attaques plus graves qui pourraient entraîner une usurpation d’identité ou une élévation des privilèges.

-   **Importante**

    Correspond aux activités suspectes pouvant conduire à une usurpation d’identité, une élévation des privilèges ou d’autres attaques à impact élevé

**État des activités suspectes**

-   **Ouverte**

    Toutes les nouvelles activités suspectes apparaissent dans cette liste

-   **Résolue**

    Utilisé pour effectuer le suivi des activités suspectes que vous avez identifiées, examinées et résolues.

    > [!NOTE]
    > ATA peut rouvrir une activité résolue si celle-ci est détectée à nouveau peu de temps après.

-   **Ignorée**

    Activités que vous avez choisi d’ignorer manuellement. Si ATA détecte une activité suspecte similaire, il crée une nouvelle détection.

## <a name="provide-input-on-a-suspicious-activity"></a>Fournir des commentaires sur une activité suspecte
Pour permettre à ATA d’en savoir plus sur votre réseau, vous devez ajouter des commentaires concernant certaines activités suspectes (DNS Reconnaissance, Pass-the-Ticket, énumération de sessions SMB, comportement inhabituel et exécution à distance) afin d’améliorer leur détection à l’avenir.

1.  La fenêtre de commentaires s’ouvre automatiquement pour les activités suspectes qui permettent de fournir des commentaires. Vous devrez répondre à des questions concernant les activités de votre réseau, et si oui ou non elles doivent être considérées comme suspectes. Dans l’exemple ci-dessous, vous devez indiquer si l’exécution d’outils d’analyse est autorisée sur l’ordinateur.

    ![Image des commentaires ATA sur les activités suspectes](media/ATA-Input.JPG)

2.  Si vous répondez « Non », l’activité sera considérée comme suspecte et vous serez alerté dès qu’ATA rencontrera cette activité sur cet ordinateur.

3.  Toutefois, si vous répondez « Oui », l’activité suspecte sera ignorée. De plus, à l’avenir, les activités de ce type effectuées sur cet ordinateur ne généreront pas d’alerte d’activité suspecte ou bien l’alerte sera automatiquement ignorée.

4.  Si vous n’êtes pas sûr, vous pouvez cliquer sur **Annuler**.

## <a name="change-the-status-of-a-suspicious-activity"></a>Modifier l’état d’une activité suspecte
Vous pouvez modifier l’état d’une activité suspecte en cliquant sur son état actuel, puis en sélectionnant l’une des options suivantes : **Ouvert**, **Résolu** ou **Ignoré**.

## <a name="see-also"></a>Voir aussi
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Gestion des paramètres de la détection ATA](working-with-detection-settings.md)
- [Modification de la configuration d’ATA](modifying-ata-configuration.md)



<!--HONumber=Feb17_HO1-->


