---
title: "Configurer la mise en miroir des ports lors du déploiement d’Azure - Protection avancée contre les menaces | Microsoft Docs"
description: "Décrit les options de mise en miroir des ports et comment les configurer pour Azure ATP"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 9ec7eb4c-3cad-4543-bbf0-b951d8fc8ffe
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1cc622f1a8306530423920873e5efa05e8c87064
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2018
---
*S’applique à : Azure - Protection avancée contre les menaces*



# <a name="configure-port-mirroring"></a>Configurer la mise en miroir des ports
> [!NOTE] 
> Cet article s’applique uniquement si vous déployez le capteur autonome Azure ATP à la place du capteur Azure ATP. Pour déterminer si vous devez utiliser le capteur autonome Azure ATP, consultez [Choix des capteurs appropriés pour votre déploiement](atp-capacity-planning.md#choosing-the-right-sensor-type-for-your-deployment).
 
La principale source de données utilisée par Azure ATP est l’inspection approfondie des paquets du trafic réseau entrant et sortant de vos contrôleurs de domaine. Pour qu’Azure ATP puisse voir le trafic réseau, vous devez configurer la mise en miroir des ports ou utiliser un TAP réseau.

Pour la **mise en miroir des ports**, configurez-la pour chaque contrôleur de domaine à surveiller en tant que **source** du trafic réseau. En règle générale, vous devez collaborer avec l’équipe de virtualisation ou de mise en réseau pour configurer la mise en miroir des ports.
Pour plus d’informations, reportez-vous à la documentation de votre fournisseur.

Vos contrôleurs de domaine et votre capteur autonome Azure ATP peuvent être physiques ou virtuels. Voici les méthodes couramment employées dans le cadre de la mise en miroir des ports et quelques considérations à prendre en compte. Pour plus d’informations, reportez-vous à la documentation produit de votre commutateur ou de votre serveur de virtualisation. Le fabricant de votre commutateur peut utiliser une terminologie différente.

**SPAN (Switched Port Analyzer)** : copie le trafic réseau à partir d’un ou plusieurs ports de commutateur vers un autre port du même commutateur. Le capteur autonome Azure ATP et les contrôleurs de domaine doivent être connectés au même commutateur physique.

**RSPAN (Remote Switch Port Analyzer)** : vous permet de surveiller le trafic réseau à partir de ports sources répartis sur plusieurs commutateurs physiques. RSPAN copie le trafic source dans un VLAN spécial configuré pour RSPAN. Ce VLAN doit être relié en mode trunk aux autres commutateurs impliqués. RSPAN fonctionne sur la couche 2.

**ERSPAN (Encapsulated Remote Switch Port Analyzer)** : il s’agit d’une technologie propriétaire qui fonctionne sur la couche 3. ERSPAN vous permet de surveiller le trafic entre les commutateurs sans faire appel à des trunks VLAN. ERSPAN utilise le protocole GRE (Generic Routing Encapsulation) pour copier le trafic réseau surveillé. Azure ATP ne peut actuellement pas recevoir directement le trafic ERSPAN. Pour qu’Azure ATP fonctionne avec le trafic ERSPAN, un commutateur ou un routeur capable de décapsuler le trafic doit être configuré comme destination d’ERSPAN à l’endroit où le trafic est décapsulé. Configurez ensuite le commutateur ou le routeur pour transférer le trafic décapsulé vers le capteur autonome Azure ATP à l’aide de SPAN ou de RSPAN.

> [!NOTE]
> Si le contrôleur de domaine faisant l’objet d’une mise en miroir des ports est connecté via une liaison WAN, vérifiez que celle-ci peut gérer la charge supplémentaire du trafic ERSPAN.
> Azure ATP prend uniquement en charge la surveillance du trafic quand le trafic atteint la carte réseau et le contrôleur de domaine de la même manière. Azure ATP ne prend pas en charge la surveillance du trafic quand celui-ci est réparti sur différents ports.

## <a name="supported-port-mirroring-options"></a>Options de mise en miroir des ports prises en charge

|Capteur autonome Azure ATP|Contrôleur de domaine|Éléments à prendre en considération|
|---------------|---------------------|------------------|
|Virtuelle|Virtuel sur le même hôte|Le commutateur virtuel doit prendre en charge la mise en miroir des ports.<br /><br />Le fait de déplacer l’une des machines virtuelles vers un autre hôte où elle sera toute seule risque de briser la mise en miroir des ports.|
|Virtuel|Virtuel sur des hôtes différents|Vérifiez que votre commutateur virtuel prend en charge ce scénario.|
|Les machines|Physique|Nécessite une carte réseau dédiée ; sinon, Azure ATP détecte tout le trafic entrant et sortant de l’hôte, même le trafic qu’il envoie au service cloud Azure ATP.|
|Physique|Les machines|Vérifiez que votre commutateur virtuel prend en charge ce scénario et configurez la mise en miroir des ports sur vos commutateurs physiques selon le cas :<br /><br />Si l’hôte virtuel se trouve sur le même commutateur physique, vous devez configurer SPAN au niveau du commutateur.<br /><br />Si l’hôte virtuel se trouve sur un autre commutateur, vous devez configurer RSPAN ou ERSPAN&#42;.|
|Physique|Physique sur le même commutateur|Le commutateur physique doit prendre en charge SPAN/la mise en miroir des ports.|
|Physique|Physique sur un autre commutateur|Exige que les commutateurs physiques prennent en charge RSPAN ou ERSPAN&#42;.|
&#42; ERSPAN est uniquement pris en charge quand la décapsulation est effectuée avant l’analyse du trafic par ATP.

> [!NOTE]
> Veillez à ce que les horloges des contrôleurs de domaine et du capteur autonome Azure ATP auquel ils se connectent soient synchronisées pour ne pas différer de plus de cinq minutes.

**Si vous travaillez avec des clusters de virtualisation :**

-   Pour chaque contrôleur de domaine qui s’exécute dans le cluster de virtualisation sur une machine virtuelle avec le capteur autonome Azure ATP, configurez l’affinité entre le contrôleur de domaine et le capteur autonome Azure ATP. De cette manière, quand le contrôleur de domaine passe à un autre hôte dans le cluster, le capteur autonome Azure ATP le suit. Cela fonctionne bien quand il y a quelques contrôleurs de domaine.

 > [!NOTE]
 > Si votre environnement prend en charge la configuration « virtuel à virtuel » sur différents hôtes (RSPAN), vous n’avez pas à vous soucier de l’affinité.
 
-   Pour s’assurer que les capteurs autonomes Azure ATP sont correctement dimensionnés pour gérer eux-mêmes la surveillance de tous les contrôleurs de domaine, essayez cette option : installez une machine virtuelle sur chaque hôte de virtualisation et installez un capteur autonome Azure ATP sur chaque hôte. Configurez chaque capteur autonome Azure ATP de façon à surveiller tous les contrôleurs de domaine qui s’exécutent dans le cluster. Ainsi, n’importe quel hôte sur lequel les contrôleurs de domaine s’exécutent est surveillé.

Après avoir configuré la mise en miroir des ports, validez son fonctionnement avant d’installer le capteur autonome Azure ATP.

## <a name="see-also"></a>Voir aussi
- [Configurer le transfert d’événements](configure-event-forwarding.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)