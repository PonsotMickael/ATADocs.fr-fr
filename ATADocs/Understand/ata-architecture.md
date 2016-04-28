---
# required metadata

title: Architecture ATA | Microsoft Advanced Threat Analytics
description: Décrit l’architecture de Microsoft Advanced Threat Analytics (ATA)
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Architecture d’ATA
L’architecture d’Advanced Threat Analytics est détaillée dans ce diagramme :

![Diagramme de la topologie de l’architecture ATA](media/ATA-architecture-topology.jpg)

ATA est constitué de deux composants principaux : la passerelle ATA et le centre ATA.

Ces composants se connectent à votre réseau existant en mettant en miroir le trafic réseau entrant et sortant de vos contrôleurs de domaine, ainsi qu’en examinant les événements Windows (transmis directement par les contrôleurs de domaine ou un serveur SIEM) et en analysant les données à la recherche d’attaques et de menaces.

Cette section décrit le flux de réseau et de capture d’événements, et examine en détail les principaux composants de la passerelle et du centre ATA, ainsi que leurs fonctionnalités.

![Diagramme du flux de trafic ATA](media/ATA-traffic-flow.jpg)

## Composants ATA
ATA est constitué des éléments suivants :

-   Une ou plusieurs passerelles ATA

-   Un centre de données ATA

## Passerelle ATA
La **passerelle ATA** effectue ce qui suit :

-   Capture et surveille le trafic des contrôleurs de domaine via la mise en miroir des ports

-   Reçoit des événements de Windows provenant de serveurs SIEM ou Syslog, ou de contrôleurs de domaine via le transfert d’événements Windows

-   Récupère les données concernant les utilisateurs et les ordinateurs du domaine Active Directory

-   Effectue la résolution des entités réseau (utilisateurs, groupes et ordinateurs)

-   Transfère les données pertinentes au centre ATA

-   Analyse plusieurs contrôleurs de domaine d’une passerelle ATA

La passerelle ATA reçoit le trafic réseau mis en miroir et les événements Windows de votre réseau, et les traite dans les composants principaux suivants :

|||
|-|-|
|Écouteur réseau|L’écouteur réseau est responsable de la capture du trafic réseau et de l’analyse du trafic. Il s’agit d’une tâche qui nécessite une utilisation intensive du processeur. Il est donc important de consulter la [configuration requise pour ATA](/advanced-threat-analytics/PlanDesign/ata-prerequisites) quand vous planifiez votre passerelle ATA.|
|Écouteur d’événements|L’écouteur d’événements est responsable de la capture et de l’analyse des événements Windows transférés à partir d’un serveur SIEM vers votre réseau.|
|Lecteur du journal des événements Windows|Le lecteur du journal des événements Windows est responsable de la lecture et de l’analyse des événements Windows transférés vers le journal des événements Windows de la passerelle ATA par les contrôleurs de domaine.|
|Traducteur d’activité réseau | Traduit le trafic analysé en la représentation logique ATA de ce trafic (NetworkActivity).
|Programme de résolution des entités|Le programme de résolution des entités reçoit les données analysées (le trafic réseau et les événements) et les résout à l’aide d’Active Directory afin de trouver les informations de compte et d’identité et de les mettre en correspondance avec les adresses IP trouvées dans les données analysées.  En outre, le programme de résolution des entités inspecte les en-têtes de paquets, permet l’analyse des paquets d’authentification pour les noms, propriétés et identités d’ordinateur, et combine ces informations avec les données du paquet.|
|Expéditeur d’entité|L’expéditeur d’entité est chargé d’envoyer au centre ATA les données analysées et mises en correspondance.|
Prenez en compte les éléments suivants quand vous devez déterminer le nombre de passerelles ATA à déployer sur votre réseau :

-   Les forêts et les domaines Active Directory

    Les passerelles ATA peuvent surveiller le trafic provenant de plusieurs domaines d’une même forêt Active Directory.   La surveillance de plusieurs forêts Active Directory nécessite des déploiements ATA distincts. Les passerelles ATA ne doivent pas être configurées pour surveiller le trafic réseau des contrôleurs de domaine de plusieurs forêts.

-   Mise en miroir de port

    La mise en miroir des ports nécessitera probablement le déploiement d’au moins une passerelle ATA par centre de données ou zone géographique.

-   Capacité

    Chaque passerelle ATA peut analyser et envoyer une certaine quantité de trafic par seconde. Si les contrôleurs de domaine que vous surveillez envoient et reçoivent plus de trafic que la passerelle ATA ne peut gérer, vous devrez ajouter des passerelles ATA supplémentaires en fonction du volume du trafic. Pour plus d’informations, consultez [Planification de la capacité ATA](/advanced-threat-analytics/PlanDesign/ata-capacity-planning).

## Centre ATA
Le **centre ATA** effectue ce qui suit :

-   Gère les paramètres de configuration de la passerelle ATA

-   Reçoit les données transmises par les passerelles ATA

-   Détecte les activités suspectes

-   Exécute différents moteurs d’apprentissage automatique des comportements

-   Exécute la console ATA

-   Facultatif : le centre ATA peut être configuré pour envoyer des e-mails et des événements quand une activité suspecte est détectée.

Le centre ATA reçoit le trafic analysé via la passerelle ATA, effectue le profilage, exécute la détection déterministe, puis exécute l’apprentissage automatique et les algorithmes comportementaux pour en savoir plus sur votre réseau afin de détecter les anomalies et vous avertir des activités suspectes.

|||
|-|-|
|Récepteur d’entité|Reçoit un lot d’entités provenant de toutes les passerelles ATA.|
|Processeur d’activité réseau|Traite toutes les activités réseau au sein de chaque lot reçu, par exemple, en mettant en correspondance les différentes étapes Kerberos effectuées depuis des ordinateurs potentiellement différents.|
|Profileur d’entité|Associe un profil à toutes les entités uniques en fonction du trafic et des événements. Par exemple, c’est là qu’ATA met à jour la liste des ordinateurs avec une session ouverte pour chaque profil utilisateur.|
|Client de base de données du centre ATA |Gère le processus d’écriture des activités réseau et des événements dans la base de données. |
|Database|ATA utilise MongoDB pour stocker l’ensemble des données du système :<br /><br />- Activités réseau<br />- Événements<br />- Entités uniques<br />- Activités suspectes<br />- Configuration ATA|
|Moteurs de détection|Les moteurs de détection utilisent des algorithmes d’apprentissage automatique et des règles déterministes pour rechercher les activités suspectes et les comportements anormaux des utilisateurs sur votre réseau.|
|Console ATA|La console ATA permet de configurer ATA et de surveiller les activités suspectes détectées par ATA sur votre réseau. La console ATA ne dépend pas du centre ATA et s’exécute même quand celui-ci est arrêté, tant qu’il peut communiquer avec la base de données.|
Prenez en compte les éléments suivants quand vous devez déterminer le nombre de centres ATA à déployer sur votre réseau :

-   Un centre ATA ne peut surveiller qu’une seule forêt Active Directory. Si vous avez plusieurs forêts Active Directory, vous aurez besoin d’au moins un centre ATA par forêt Active Directory.

    Dans les déploiements d’Active Directory à grande échelle, un seul centre ATA ne sera peut-être pas suffisant pour gérer le trafic de tous les contrôleurs de domaine. Dans ce cas, plusieurs centres ATA seront nécessaires et les détections ATA seront moins efficaces. Le nombre de centres ATA doit être défini par la [planification de la capacité ATA](/advanced-threat-analytics/PlanDesign/ata-capacity-planning).

## Composants du réseau
Pour utiliser ATA, vous devrez apporter des modifications mineures à votre réseau existant, mais vous devrez d’abord vous assurer de ce qui suit.

### Mise en miroir des ports
Pour qu’ATA fonctionne, vous devez activer la mise en miroir des ports pour tous les contrôleurs de domaine de la forêt Active Directory actuellement surveillée. ATA fonctionnera si la mise en miroir des ports est définie vers ATA pour plusieurs contrôleurs de domaine, mais pas pour tous. Toutefois, la détection sera moins efficace.

Définissez la mise en miroir des ports depuis les contrôleurs de domaine vers la passerelle ATA. Même si le trafic réseau de tous les contrôleurs de domaine est mis en miroir vers la passerelle ATA, seul un très petit pourcentage de ce trafic est envoyé (compressé) au centre ATA à des fins d’analyse.

Les contrôleurs de domaine et les passerelles ATA peuvent être physiques ou virtuels. Pour plus d’informations, voir [Configurer la mise en miroir des ports](/advanced-threat-analytics/PlanDesign/configure-port-mirroring).

### Événements
Pour améliorer la détection ATA de Pass-the-Hash, ATA a besoin du journal des événements Windows ID 4776. Les événements peuvent être transférés à la passerelle ATA de deux manières : en configurant la passerelle ATA de façon à écouter les événements SIEM ou à l’aide du transfert d’événements Windows.

-   Configuration de la passerelle ATA pour écouter les événements SIEM

    Configurez votre serveur SIEM de manière à transférer des événements Windows spécifiques vers ATA. ATA prend en charge plusieurs fournisseurs SIEM. Pour plus d’informations, voir [Configure event collection](/advanced-threat-analytics/PlanDesign/configure-event-collection) (Configurer la collecte d’événements).

-   Configuration du transfert d’événements Windows

    Une autre méthode permettant à ATA d’obtenir vos événements consiste à configurer vos contrôleurs de domaine de manière à transférer l’événement Windows 4776 vers votre passerelle ATA. Cette méthode est particulièrement utile si vous n’avez pas de serveur SIEM ou si votre serveur SIEM n’est pas actuellement pris en charge par ATA. Pour plus d’informations sur le transfert d’événements Windows dans ATA, voir [Configuration du transfert d’événements Windows](/advanced-threat-analytics/PlanDesign/configure-event-collection#ATA_event_WEF).

## Voir aussi
- [Configuration requise pour ATA](/advanced-threat-analytics/PlanDesign/ata-prerequisites)
- [Planification de la capacité ATA](/advanced-threat-analytics/PlanDesign/ata-capacity-planning)
- [Configurer la collecte d’événements](/advanced-threat-analytics/PlanDesign/configure-event-collection)
- [Configuration du transfert d’événements Windows](/advanced-threat-analytics/PlanDesign/configure-event-collection#ATA_event_WEF)
- [Pour obtenir de l’aide, consultez notre forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


