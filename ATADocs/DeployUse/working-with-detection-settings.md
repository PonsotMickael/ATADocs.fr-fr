---
title: "Gestion des paramètres de la détection ATA | Microsoft Advanced Threat Analytics"
description: "Décrit comment configurer une liste d’adresses IP et de sous-réseaux ayant des circonstances inhabituelles et qui doivent donc être gérés différemment des autres entités de votre réseau."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 3840a5f7abdd496ad245a3f1c2589ad1855fddb5


---

# Gestion des paramètres de la détection ATA
La page de configuration **Détection** permet de configurer une liste d’adresses IP et de sous-réseaux ayant des circonstances inhabituelles et qui doivent donc être gérés différemment des autres entités de votre réseau.

## Configuration de la détection
Dans la page **Détection**, vous pouvez définir les éléments suivants :

-   **Sous-réseaux du bail à court terme** : si votre entreprise dispose de sous-réseaux avec des adresses IP à très court terme, comme des sous-réseaux d’adresses IP VPN ou des sous-réseaux Wi-Fi, il est important de fournir à ATA des commentaires sur ces adresses IP et ces sous-réseaux, afin qu’il stocke l’association entre un ordinateur et une adresse IP de ces plages pendant une durée plus courte que pour d’autres adresses IP.

-   **SID de comptes honeytoken** : ce compte d’utilisateur ne doit pas avoir d’activité réseau. Ce compte sera configuré comme l’utilisateur honeytoken ATA. Si quelqu’un tente d’utiliser ce compte d’utilisateur, ATA crée une alerte d’activité suspecte avec une indication d’activité malveillante. Pour configurer l’utilisateur honeytoken, vous aurez besoin du SID du compte d’utilisateur, et non du nom d’utilisateur.

Vous pouvez exclure des adresses IP des détections suivantes. Si vous ajoutez une adresse IP dans une de ces listes, ATA exclura cette adresse IP de ce type précis d’activité.

-   Exclusions d’adresses IP DNS Reconnaissance

-   Exclusions d’adresses IP Pass-the-Ticket

## Voir aussi
- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Modification de la configuration d’ATA](modifying-ata-configuration.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->


