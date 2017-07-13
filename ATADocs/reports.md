---
title: Utilisation des rapports ATA | Microsoft Docs
description: "Explique comment vous pouvez générer des rapports dans ATA pour surveiller votre réseau."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/12/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 38ea49b5-cd5e-43e5-bc39-5071f759633b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4f29dfcc8b18ff755f6c0dcdaa08eaa807b08072
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
*S’applique à : Advanced Threat Analytics version 1.8*


# Rapports ATA
<a id="ata-reports" class="xliff"></a>

La section Rapports ATA de la console vous permet de générer des rapports contenant des informations sur l’état du système, sur l’intégrité du système et sur les activités suspectes détectées dans votre environnement.

Pour accéder à la page Rapports, cliquez sur l’icône de rapport dans la barre de menus : ![icône de rapport](./media/ata-report-icon.png).
Les rapports disponibles sont : 
- Rapport de synthèse : ce rapport présente un tableau de bord de l’état dans le système. Vous pouvez afficher trois onglets : un pour un **Résumé** de ce qui a été détecté sur votre réseau, un pour les **Activités suspectes ouvertes** qui répertorie les activités suspectes nécessitant votre attention, et un pour les **Problèmes d’intégrité ouverts** qui répertorie les problèmes d’intégrité système ATA nécessitant votre attention. Les activités suspectes répertoriées sont regroupées par type, tout comme les problèmes d’intégrité. 
- Modification des groupes sensibles : ce rapport répertorie toutes les modifications apportées à des groupes sensibles (comme les administrateurs).

Il existe deux façons de générer un rapport : à la demande ou en planifiant un rapport à envoyer périodiquement à votre adresse e-mail.

Pour générer un rapport à la demande :

1. Dans la barre de menus de la console ATA, cliquez sur l’icône de rapport dans la barre de menus : ![icône de rapport](./media/ata-report-icon.png).
2. Sous **Résumé** ou **Modifications des groupes sensibles**, définissez les dates **De** et **À**, et cliquez sur **Télécharger**. 
![rapports](./media/reports.png)

Pour définir un rapport planifié :
 
1. Dans la page **Rapports**, cliquez sur **Définir les rapports planifiés** ou, dans la page de configuration de la console ATA, sous Notifications et rapports, cliquez sur **Rapports planifiés**.

   ![Planification de rapports](./media/ata-sched-reports.png)

2. Cliquez sur **Planifier** en regard de **Résumé** ou de **Modifications des groupes sensibles** pour définir la fréquence et l’adresse e-mail de remise des rapports, cliquez sur le signe plus en regard des adresses e-mail pour les ajouter, puis cliquez sur **Enregistrer**.

   ![Planifier la fréquence et l’adresse e-mail des rapports](./media/sched-report1.png)


> [!NOTE]
> Les rapports planifiés sont remis par e-mail et peuvent être envoyés seulement que si vous avez déjà configuré un serveur de messagerie sous **Configuration**, en sélectionnant **Serveur de messagerie** sous Notifications et rapports.


## Voir aussi
<a id="see-also" class="xliff"></a>
- [Prérequis au déploiement d’ATA](ata-prerequisites.md)
- [Planification de la capacité d’ATA](ata-capacity-planning.md)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Configuration du transfert d’événements Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
