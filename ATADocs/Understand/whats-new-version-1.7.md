---
title: "Nouveautés d’ATA version 1.7 | Microsoft ATA"
description: "Répertorie les nouveautés d’ATA version 1.7, ainsi que les problèmes connus"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 09/20/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 
ms.reviewer: 
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d47d9e7be294c68d764710c15c4bb78539e42f62
ms.openlocfilehash: 62f2aadc978547647a1dc3c27ed3453f7ed15828


---

# Nouveautés d’ATA version 1.7
Ces notes de publication fournissent des informations sur les problèmes connus de cette version d’Advanced Threat Analytics.

## Quelles sont les nouveautés d’ATA 1.7 ?
La mise à jour vers ATA 1.7 comprend des améliorations dans les domaines suivants :

-   Détections nouvelles et mises à jour

-   Contrôle d'accès en fonction du rôle

-   Prise en charge de Windows Server 2016 et Windows Server Core

-   Améliorations apportées à l’expérience utilisateur

-   Modifications mineures


### Détections nouvelles et mises à jour


- **Reconnaissance à l’aide d’une énumération de services d’annuaire** Dans le cadre de la phase de reconnaissance, les pirates collectent des informations sur les entités du réseau à l’aide de différentes méthodes. L’énumération des services d’annuaire à l’aide du protocole SAM-R permet aux pirates d’obtenir la liste des utilisateurs et des groupes dans un domaine et de comprendre l’interaction entre les différentes entités. 

- **Améliorations liées à Pass-the-Hash** Pour améliorer la détection Pass-the-Hash, nous avons ajouté des modèles de comportement supplémentaires pour les modèles d’authentification d’entités. Ces modèles permettent à ATA de mettre en corrélation le comportement d’entité avec les authentifications NTLM suspectes, et de différencier les attaques Pass-the-Hash réelles du comportement de scénarios de type « faux positif ».

- **Améliorations liées à Pass-the-Ticket** Pour détecter les attaques avancées en général et les attaques Pass-the-Ticket en particulier, la corrélation entre une adresse IP et le compte d’ordinateur doit être exacte. Il s’agit d’un véritable défi dans les environnements où les adresses IP changent rapidement par conception (par exemple sur les réseaux Wi-Fi et quand plusieurs machines virtuelles partagent le même hôte). Pour relever ce défi et améliorer la précision de la détection de Pass-the-Ticket, le mécanisme de résolution de nom de réseau d’ATA a été amélioré considérablement afin de réduire les faux positifs.

- **Améliorations liées aux comportements anormaux** Dans ATA 1.7, les données d’authentification NTLM ont été ajoutées comme source de données pour les détections de comportements anormaux, fournissant aux algorithmes une couverture plus étendue du comportement d’entité sur le réseau. 

- **Améliorations liées à l’implémentation de protocoles inhabituels** ATA détecte désormais l’implémentation de protocoles inhabituels dans le protocole Kerberos, ainsi que d’autres anomalies dans le protocole NTLM. Plus spécifiquement, ces nouvelles anomalies pour Kerberos sont couramment utilisées dans les attaques de type « Over-pass-the-Hash ».


### Infrastructure

- **Contrôle d’accès en fonction du rôle ** Fonctionnalité de contrôle d’accès en fonction du rôle (RBAC). ATA 1.7 inclut trois rôles : ATA Administrator, ATA Analyst et ATA Executive.

- **Prise en charge de Windows Server 2016 et Windows Server Core** ATA 1.7 prend en charge le déploiement de passerelles légères sur les contrôleurs de domaine exécutant Server Core pour Windows Server 2012 et Server Core pour Windows Server 2012 R2. De plus, cette version prend en charge Windows Server 2016 pour les composants Centre ATA et Passerelle ATA.

### Expérience de l'utilisateur
- **Expérience de configuration** Dans cette version, l’expérience de configuration d’ATA a été repensée pour une meilleure expérience utilisateur et pour mieux prendre en charge les environnements à plusieurs passerelles ATA. Cette version introduit également la page de mise à jour de la passerelle ATA pour une gestion plus simple et plus performante des mises à jour automatiques pour les différentes passerelles.

## Problèmes connus
Les problèmes connus de cette version sont les suivants :

### Risque d’échec de mise à jour automatique de passerelle
**Symptômes :** Dans les environnements avec des liaisons WAN lentes, la mise à jour de la passerelle ATA peut atteindre le délai d’expiration de mise à jour (100 secondes) et échouer.
Dans la console ATA, la passerelle ATA a l’état « Mise à jour (téléchargement du package) » pendant un laps de temps prolongé et l’opération finit par échouer.
**Solution de contournement :** Pour contourner ce problème, téléchargez le package de passerelle ATA le plus récent à partir de la console ATA et mettez à jour la passerelle ATA manuellement.

 > [!IMPORTANT]
 Le renouvellement automatique des certificats utilisés par ATA n’est pas pris en charge. L’utilisation de ces certificats peut provoquer le non-fonctionnement d’ATA lors du renouvellement automatique du certificat. 

### Aucune prise en charge du navigateur pour l’encodage JIS
**Symptômes :** La console ATA peut ne pas fonctionner comme prévu sur les navigateurs utilisant l’encodage JIS **Solution de contournement :** Modifiez l’encodage du navigateur et choisissez Unicode UTF-8.
 
## Modifications mineures

- ATA utilise désormais OWIN au lieu d’IIS pour la console ATA.
- Si le service du centre ATA ne fonctionne pas, vous ne pourrez pas accéder à la console ATA.
- Les sous-réseaux du bail à court terme ne sont plus nécessaires en raison des modifications apportées à la résolution de nom de réseau d’ATA.

## Voir aussi
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Mise à jour d’ATA vers la version 1.7 : guide de migration](ata-update-1.7-migration-guide.md)




<!--HONumber=Sep16_HO4-->


