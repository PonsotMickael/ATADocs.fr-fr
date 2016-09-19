---
title: Architecture ATA | Microsoft ATA
description: "Décrit l’architecture de Microsoft Advanced Threat Analytics (ATA)"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 050f1ef0b39d69b64ede53243a7fa2d33d0e4813
ms.openlocfilehash: c416fba5aace73cf585e7f6ca604a8c61c3c6fcc


---

*S’applique à : Advanced Threat Analytics version 1.7*




# Architecture d’ATA
L’architecture d’Advanced Threat Analytics est détaillée dans ce diagramme :

![Diagramme de la topologie de l’architecture ATA](media/ATA-architecture-topology.jpg)

ATA surveille le trafic réseau de votre contrôleur de domaine en utilisant la mise en miroir des ports vers une passerelle ATA avec des commutateurs physiques ou virtuels, ou en déployant la passerelle légère ATA directement sur vos contrôleurs de domaine, ce qui supprime la nécessité de la mise en miroir des ports. De plus, ATA peut tirer parti des événements Windows (transférés directement à partir de vos contrôleurs de domaine ou d’un serveur SIEM) et analyser les données à la recherche d’attaques et de menaces.
Cette section décrit le flux de capture réseau et d’événements, et décrire les fonctionnalités des principaux composants de la technologie ATA : la passerelle ATA, la passerelle légère ATA (qui a les mêmes fonctionnalités de base que la passerelle ATA) et le centre ATA.


![Diagramme du flux de trafic ATA](media/ATA-traffic-flow.jpg)

## Composants ATA
ATA est constitué des éléments suivants :

-   **Centre ATA** <br>
Le centre ATA reçoit des données à partir des passerelles ATA et/ou ATA légères que vous déployez.
-   **Passerelle ATA**<br>
La passerelle ATA est installée sur un serveur dédié qui surveille le trafic à partir de vos contrôleurs de domaine à l’aide de la mise en miroir des ports ou d’un TAP réseau.
-   **Passerelle légère ATA**<br>
La passerelle ATA légère est installée directement sur vos contrôleurs de domaine et analyse directement leur trafic, sans recourir à un serveur dédié ou à une configuration de mise en miroir des ports. Il s’agit d’une alternative à la passerelle ATA.

Un déploiement ATA peut se composer d’un seul centre ATA connecté à toutes les passerelles ATA, à toutes les passerelles légères ATA, ou à une combinaison de passerelles ATA et de passerelles légères ATA.


## Options de déploiement
Vous pouvez déployer ATA à l’aide de la combinaison de passerelles suivante :

-   **Utilisation de passerelles ATA uniquement** <br>
Si votre déploiement ATA contient uniquement des passerelles ATA, sans aucune passerelle légère ATA, tous les contrôleurs de domaine doivent être configurés pour activer la mise en miroir des ports vers une passerelle ATA ou des TAP réseau doivent être en place.
-   **Utilisation de passerelles légères ATA uniquement**<br>
Si votre déploiement ATA contient uniquement des passerelles légères ATA, celles-ci sont déployées sur chaque contrôleur de domaine et aucun serveur supplémentaire ou configuration de mise en miroir des ports n’est nécessaire.
-   **Utilisation de passerelles ATA et de passerelles légères ATA**<br>
Si votre déploiement ATA comprend des passerelles ATA et des passerelles légères ATA, où la passerelle légère ATA est installée sur certains contrôleurs de domaine (par exemple, tous les contrôleurs dans vos sites de succursale) tandis que les autres contrôleurs de domaine sont surveillés par des passerelles ATA (par exemple, les contrôleurs de domaine plus importants dans vos principaux centres de données).

Dans les trois scénarios, toutes les passerelles envoient leurs données au centre ATA.




## Centre ATA
Le **centre ATA** effectue ce qui suit :

-   Gère les paramètres de configuration des passerelles ATA et des passerelles légères ATA

-   Reçoit les données des passerelles ATA et des passerelles légères ATA 

-   Détecte les activités suspectes

-   Exécute des algorithmes d’apprentissage automatique de comportement ATA pour détecter les comportements anormaux

-   Exécute différents algorithmes déterministes pour détecter les attaques avancées en fonction de la chaîne de destruction d’attaque avancée

-   Exécute la console ATA

-   Facultatif : le centre ATA peut être configuré pour envoyer des e-mails et des événements quand une activité suspecte est détectée.

Le centre ATA reçoit le trafic analysé de la passerelle ATA et de la passerelle légère ATA, effectue le profilage, exécute la détection déterministe, puis exécute l’apprentissage automatique et les algorithmes comportementaux pour en savoir plus sur votre réseau afin de détecter les anomalies et vous avertir des activités suspectes.

|||
|-|-|
|Récepteur d’entité|Reçoit des lots d’entités provenant de toutes les passerelles ATA et passerelles légères ATA.|
|Processeur d’activité réseau|Traite toutes les activités réseau au sein de chaque lot reçu. par exemple, en mettant en correspondance les différentes étapes Kerberos effectuées depuis des ordinateurs potentiellement différents.|
|Profileur d’entité|Associe un profil à toutes les entités uniques en fonction du trafic et des événements. Par exemple, c’est là qu’ATA met à jour la liste des ordinateurs avec une session ouverte pour chaque profil utilisateur.|
|Base de données du centre|Gère le processus d’écriture des activités réseau et des événements dans la base de données. |
|Database|ATA utilise MongoDB pour stocker l’ensemble des données du système :<br /><br />- Activités réseau<br />- Activités d’événements<br />- Entités uniques<br />- Activités suspectes<br />- Configuration ATA|
|Détecteurs|Les détecteurs utilisent des algorithmes d’apprentissage automatique et des règles déterministes pour rechercher les activités suspectes et les comportements anormaux des utilisateurs sur votre réseau.|
|Console ATA|La console ATA permet de configurer ATA et de surveiller les activités suspectes détectées par ATA sur votre réseau. La console ATA ne dépend pas du centre ATA et s’exécute même quand celui-ci est arrêté, tant qu’il peut communiquer avec la base de données.|
Prenez en compte les éléments suivants quand vous devez déterminer le nombre de centres ATA à déployer sur votre réseau :

-   Un centre ATA ne peut surveiller qu’une seule forêt Active Directory. Si vous avez plusieurs forêts Active Directory, vous aurez besoin d’au moins un centre ATA par forêt Active Directory.

-    Dans les déploiements d’Active Directory à très grande échelle, un seul centre ATA ne sera peut-être pas suffisant pour gérer le trafic de tous les contrôleurs de domaine. Dans ce cas, plusieurs centres ATA seront nécessaires. Le nombre de centres ATA doit être défini par la [planification de la capacité ATA](ata-capacity-planning.md).

## Passerelle ATA et passerelle légère ATA

### Fonctionnalité de base de la passerelle
La **passerelle ATA** et la **passerelle légère ATA** ont la même fonctionnalité de base :

-   Capturer et inspecter le trafic réseau des contrôleurs de domaine (le trafic de mise en miroir des ports dans le cas d’une passerelle ATA et le trafic local du contrôleur de domaine dans le cas d’une passerelle légère ATA) 

-   Recevoir des événements Windows provenant de serveurs SIEM ou Syslog, ou de contrôleurs de domaine par le biais du transfert d’événements Windows

-   Récupérer les données concernant les utilisateurs et les ordinateurs à partir du domaine Active Directory

-   Effectuer la résolution des entités réseau (utilisateurs, groupes et ordinateurs)

-   Transférer les données pertinentes au centre ATA

-   Surveiller plusieurs contrôleurs de domaine à partir d’une seule passerelle ATA, ou surveiller un seul contrôleur de domaine pour une passerelle légère ATA

La passerelle ATA reçoit le trafic réseau et les événements Windows de votre réseau, et les traite dans les composants principaux suivants :

|||
|-|-|
|Écouteur réseau|L’écouteur réseau est responsable de la capture du trafic réseau et de l’analyse du trafic. Il s’agit d’une tâche qui nécessite une utilisation intensive du processeur. Il est donc important de consulter la [configuration requise pour ATA](ata-prerequisites.md) quand vous planifiez votre passerelle ATA ou passerelle légère ATA.|
|Écouteur d’événements|L’écouteur d’événements est responsable de la capture et de l’analyse des événements Windows transférés à partir d’un serveur SIEM vers votre réseau.|
|Lecteur du journal des événements Windows|Le lecteur du journal des événements Windows est responsable de la lecture et de l’analyse des événements Windows transférés vers le journal des événements Windows de la passerelle ATA par les contrôleurs de domaine.|
|Traducteur d’activité réseau | Traduit le trafic analysé en une représentation logique du trafic utilisée par ATA (NetworkActivity).
|Programme de résolution des entités|Le programme de résolution des entités reçoit les données analysées (le trafic réseau et les événements) et les résout à l’aide d’Active Directory pour trouver les informations de compte et d’identité. Ensuite, il les met en correspondance avec les adresses IP trouvées dans les données analysées. Le programme de résolution des entités inspecte les en-têtes de paquets de manière efficace, pour permettre l’analyse des noms, propriétés et identités d’ordinateurs dans les paquets d’authentification. Le programme de résolution des entités combine les paquets d’authentification analysés avec les données du paquet.|
|Expéditeur d’entité|L’expéditeur d’entité est chargé d’envoyer au centre ATA les données analysées et mises en correspondance.|

## Fonctionnalités de la passerelle légère ATA

Les fonctionnalités suivantes fonctionnent différemment selon que vous exécutez une passerelle ATA ou une passerelle légère ATA.

-   **Candidat synchronisateur de domaine**<br>
La passerelle synchronisatrice de domaine est responsable de la synchronisation proactive de toutes les entités d’un domaine Active Directory spécifique (semblable au mécanisme utilisé par les contrôleurs de domaine eux-mêmes pour la réplication). Une passerelle est choisie au hasard comme synchronisateur de domaine dans la liste des candidats. <br><br>
Si le synchronisateur est hors connexion pendant plus de 30 minutes, un autre candidat est choisi à la place. Si aucun synchronisateur de domaine n’est disponible pour un domaine spécifique, ATA ne peut pas synchroniser de manière proactive les entités et leurs modifications, mais il récupère de manière réactive les nouvelles entités à mesure qu’elles sont détectées dans le trafic analysé. 
<br>Si aucun synchronisateur de domaine n’est disponible et que vous recherchez une entité avec laquelle aucun trafic n’était associé, aucun résultat de recherche ne s’affiche.<br><br>
Par défaut, toutes les passerelles ATA sont des candidats synchronisateurs.<br><br>
Comme il est plus probable que toutes les passerelles légères ATA soient déployées dans des sites de succursale et sur des contrôleurs de domaine de petite taille, par défaut elles ne sont pas candidats synchronisateurs.


-   **Limitations des ressources**<br>
La passerelle légère ATA inclut un composant d’analyse qui évalue la capacité de calcul et de mémoire disponible sur le contrôleur de domaine sur lequel elle s’exécute. Le processus d’analyse s’exécute toutes les 10 secondes et met à jour de manière dynamique le quota d’utilisation du processeur et de la mémoire sur le processus de la passerelle légère ATA pour s’assurer qu’à tout moment le contrôleur de domaine dispose d’au moins 15 % de ressources de calcul et de mémoire libres.<br><br>
Quoi qu’il se passe sur le contrôleur de domaine, ce processus libère toujours des ressources pour s’assurer que la fonctionnalité de base du contrôleur de domaine n’est pas affectée.<br><br>
Si à cause de cela la passerelle légère ATA manque de ressources, le trafic est seulement partiellement analysé et l’alerte de surveillance « Le trafic réseau du port en miroir qui a été supprimé » s’affiche dans la page Intégrité.

Le tableau suivant présente un exemple de contrôleur de domaine qui dispose de suffisamment de ressources de calcul pour autoriser un quota plus élevé que ce qui est nécessaire actuellement. Ainsi, tout le trafic est analysé :

||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Passerelle légère ATA (Microsoft.Tri.Gateway.exe)|Divers (autres processus) |Quota de passerelle légère ATA|Trafic ignoré par la passerelle|
|30 %|20 %|10 %|45 %|Non|

Si Active Directory a besoin de davantage de puissance de calcul, le quota requis par la passerelle légère ATA est réduit. Dans l’exemple suivant, la passerelle légère ATA a besoin de davantage que le quota alloué et ignore une partie du trafic (analyse partielle du trafic) :

||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Passerelle légère ATA (Microsoft.Tri.Gateway.exe)|Divers (autres processus) |Quota de passerelle légère ATA|Trafic ignoré par la passerelle|
|60 %|15 %|10 %|15 %|Oui|



## Composants du réseau
Pour que vos composants réseau fonctionne avec ATA, vérifiez les éléments suivants :

### Mise en miroir des ports
Si vous utilisez des passerelles ATA, vous devez configurer la mise en miroir des ports pour les contrôleurs de domaine qui seront surveillés et définir la passerelle ATA comme destination à l’aide des commutateurs physiques ou virtuels. Une autre option consiste à utiliser des TAP réseau. ATA fonctionnera si plusieurs contrôleurs de domaine sont surveillés, mais pas tous. Toutefois, la détection sera moins efficace.

Même si tout le trafic réseau des contrôleurs de domaine est mis en miroir vers la passerelle ATA, seul un très petit pourcentage de ce trafic est envoyé (compressé) au centre ATA à des fins d’analyse.

Les contrôleurs de domaine et les passerelles ATA peuvent être physiques ou virtuels. Pour plus d’informations, consultez [Configurer la mise en miroir des ports](/advanced-threat-analytics/deploy-use/configure-port-mirroring).


### Événements
Pour améliorer la détection des attaques Pass-the-Hash, force brute et Honey Tokens, ATA doit accéder à l’événement associé à l’ID 4776 du journal des événements Windows. Les événements peuvent être transférés à la passerelle ATA de deux manières : en configurant la passerelle ATA de façon à écouter les événements SIEM ou à l’aide du transfert d’événements Windows.

-   Configuration de la passerelle ATA pour écouter les événements SIEM <br>Configurez votre serveur SIEM de manière à transférer des événements Windows spécifiques vers ATA. ATA prend en charge plusieurs fournisseurs SIEM. Pour plus d’informations, consultez [Configurer la collecte d’événements](/advanced-threat-analytics/deploy-use/configure-event-collection).

-   Configuration du transfert d’événements Windows<br>Une autre méthode permettant à ATA d’obtenir vos événements consiste à configurer vos contrôleurs de domaine de manière à transférer l’événement Windows 4776 vers votre passerelle ATA. Cette méthode est particulièrement utile si vous n’avez pas de serveur SIEM ou si votre serveur SIEM n’est pas actuellement pris en charge par ATA. Pour plus d’informations sur le transfert d’événements Windows dans ATA, consultez [Configuration du transfert d’événements Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding).

## Voir aussi
- [Configuration requise pour ATA](ata-prerequisites.md)
- [Planification de la capacité ATA](ata-capacity-planning.md)
- [Configurer la collecte d’événements](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configuration du transfert d’événements Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Aug16_HO5-->


