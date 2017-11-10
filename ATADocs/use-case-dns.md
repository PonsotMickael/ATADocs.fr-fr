---
title: "Examen de la reconnaissance à l’aide de DNS | Microsoft Docs"
description: "Cet article décrit la reconnaissance à l’aide de DNS et fournit des instructions d’examen quand cette menace est détectée sur votre réseau."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 5ec554b303a19a6e7b12cd788755604f1aaf43db
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/07/2017
---
*S’applique à : Advanced Threat Analytics version 1.8*

# <a name="investigating-reconnaissance-using-dns"></a>Examen de la reconnaissance à l’aide de DNS

Si ATA détecte une **reconnaissance à l’aide de DNS** sur votre réseau et vous en alerte, utilisez cet article pour vous aider à examiner l’alerte et à déterminer comment résoudre le problème.

## <a name="what-is-reconnaissance-using-dns"></a>Qu’est-ce que la reconnaissance à l’aide de DNS ?

L’alerte de **reconnaissance à l’aide de DNS** indique que des requêtes DNS (Domain Name System) sont envoyées par un hôte inhabituel afin d’effectuer une reconnaissance de votre réseau interne.

Le DNS (Domain Name System) est un service implémenté comme une base de données hiérarchique et distribuée qui fournit la résolution des noms d’hôtes et des noms de domaine. Les noms dans une base de données DNS forment une arborescence hiérarchique appelée espace de noms de domaine.
Pour un adversaire, votre DNS contient des informations précieuses sur le mappage d’un réseau interne, notamment une liste de tous les serveurs et souvent la liste de tous les clients mappés à leurs adresses IP. Par ailleurs, ces informations ont de la valeur, car elles listent les noms d’hôte qui sont souvent évocateurs dans un environnement réseau donné. En récupérant ces informations, l’adversaire peut concentrer ses efforts sur les entités qui l’intéressent pendant une campagne. Des outils comme [Nmap](https://nmap.org/), [Fierce](https://github.com/mschwager/fierce) et des outils intégrés comme [Nslookup](https://technet.microsoft.com/library/cc725991(v=ws.11).aspx) fournissent des fonctionnalités pour découvrir les hôtes qui utilisent la reconnaissance DNS.
La détection des requêtes de reconnaissance à l’aide de DNS provenant d’un hôte interne est une source de préoccupation et le signe qu’un hôte existant a pu être compromis, ou à plus grande échelle, le réseau, ou qu’il existe une menace interne.

## <a name="dns-query-types"></a>Types de requêtes DNS

Il existe plusieurs types de requêtes dans le protocole DNS. ATA détecte les requêtes AXFR (transfert) et crée une alerte le cas échéant. Ce type de requête doit provenir uniquement des serveurs DNS.

## <a name="discovering-the-attack"></a>Détection de l’attaque

Quand un attaquant tente d’effectuer une reconnaissance à l’aide de DNS, ATA la détecte et la marque avec une gravité moyenne.

![ATA détecte une reconnaissance DNS](./media/dns-recon.png)
 
ATA affiche le nom de l’ordinateur source ainsi que des détails supplémentaires sur la requête DNS réelle qui a été effectuée. Par exemple, plusieurs tentatives ont pu être effectuées à partir du même hôte.

## <a name="investigating"></a>Examen

Pour examiner la reconnaissance à l’aide de DNS, vous devez d’abord déterminer la cause des requêtes. Elle peut être identifiée dans l’une des catégories suivantes : 
-   Vrais positifs : un attaquant ou un programme malveillant est présent sur votre réseau. Il peut s’agir d’un attaquant qui a violé le périmètre du réseau ou d’une menace interne.
-   Vrais positifs sans gravité : il peut s’agir d’alertes déclenchées par les tests de stylet, l’activité du groupe red-team, les analyseurs de sécurité, le pare-feu nouvelle génération ou les administrateurs informatiques exécutant des activités approuvées.
-   Faux positifs : vous pouvez obtenir des alertes liées à une mauvaise configuration, par exemple, si le port UDP 53 est bloqué entre la passerelle ATA et votre serveur DNS (ou tout autre problème réseau).

Le graphique suivant vous permet de déterminer les étapes à suivre dans l’examen de l’alerte :

![Résolution de la reconnaissance DNS avec ATA](./media/dns-recon-diagram.png)
 
1.  La première étape consiste à identifier l’ordinateur émetteur de l’alerte, comme illustré dans l'écran suivant :
 
    ![Consulter l’activité suspecte de reconnaissance dans ATA](./media/dns-recon.png)
2.  Identifiez l’ordinateur concerné. Est-ce une station de travail, un serveur, une station de travail d’administration, une station de test du stylet, etc. ?
3.  Si l’ordinateur est un serveur DNS et dispose des droits légitimes pour demander une copie secondaire de la zone, il s’agit d’un faux positif. Quand vous trouvez un faux positif, utilisez l’option **Exclure** pour ne plus recevoir cette alerte pour cet ordinateur.
4. Vérifiez que le port UDP 53 est ouvert entre la passerelle ATA et votre serveur DNS.
4.  Si l’ordinateur est utilisé pour le travail de l’administrateur ou le test du stylet, il s’agit d’un vrai positif sans gravité et l’ordinateur impliqué peut également être configuré comme une exception.
5.  S’il n’est pas utilisé pour le test du stylet, vérifiez si l’ordinateur exécute un analyseur de sécurité ou un pare-feu nouvelle génération qui peuvent envoyer des requêtes DNS de type AXFR.
6.  Enfin, si aucun de ces critères n’est rempli, il est possible que l’ordinateur soit compromis. Si tel est le cas, il doit être entièrement examiné. 
7.  Si les requêtes sont isolées sur des ordinateurs spécifiques et sont considérées comme n’étant pas sans gravité, suivez les étapes suivantes :
    1.  Passez en revue les sources de journal disponibles. 
    2.  Effectuez une analyse basée sur un hôte. 
    3.  Si l’activité ne vient pas d’un utilisateur suspecté, vous devez effectuer l’analyse d’investigation sur l’ordinateur pour déterminer si celui-ci a été compromis par des programmes malveillants.

## <a name="post-investigation"></a>Après l’examen

Les programmes malveillants utilisés pour compromettre l’hôte peuvent inclure des chevaux de Troie avec des fonctionnalités de porte dérobées. Quand un mouvement latéral a été identifié à partir de l’hôte compromis, les actions correctives doivent s’étendre à ces hôtes, y compris le changement des mots de passe et des informations d’identification utilisés sur l’hôte et sur tous les hôtes inclus dans le mouvement latéral. 

Quand il n’est pas possible de confirmer que l’hôte cible est sain une fois les étapes de correction effectuées ou d’identifier la cause racine de la compromission, Microsoft recommande de sauvegarder les données critiques et de reconstruire l’ordinateur hôte. Par ailleurs, les hôtes nouveaux ou reconstruits doivent faire l’objet d’une protection renforcée avant d’être réintégrés au réseau afin d’empêcher toute nouvelle infection. 

Microsoft recommande d’utiliser une équipe IR&R (Incident Response & Recovery) professionnelle, qui peut être contactée via votre équipe des comptes Microsoft, afin de détecter si un attaquant a déployé des méthodes de persistance sur votre réseau.

## <a name="mitigation"></a>Limitation des risques

La sécurisation d’un serveur DNS interne pour éviter la reconnaissance à l’aide de DNS est possible en désactivant les transferts de zone ou en les limitant uniquement aux adresses IP spécifiées. Pour plus d’informations sur la limitation des transferts de zone, consultez [Restrict Zone Transfers](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx) (Limiter les transferts de zone). Les transferts de zone limités peuvent être verrouillés davantage en [sécurisant les transferts de zone avec IPsec](https://technet.microsoft.com/library/ee649192(v=ws.10).aspx). La modification des transferts de zone est l’une des tâches de la liste de contrôle que vous devez suivre pour [sécuriser vos serveurs DNS contre les attaques internes et externes](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx).



## <a name="see-also"></a>Voir aussi
- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
