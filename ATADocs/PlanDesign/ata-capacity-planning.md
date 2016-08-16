---
title: "Planification de votre déploiement ATA | Microsoft Advanced Threat Analytics"
description: "Vous aide à planifier votre déploiement et à déterminer le nombre de serveurs ATA nécessaires pour prendre en charge votre réseau"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 279d79f2-962c-4c6f-9702-29744a5d50e2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d6e7d7bef97bfc4ffde07959dd9256f0319d685f
ms.openlocfilehash: ff8eb5361d3dfeaa3715d325ed91c0ad422211ed


---

# Planification de la capacité ATA
Cette rubrique vous aide à déterminer le nombre de serveurs ATA nécessaires pour prendre en charge votre réseau, notamment le nombre de passerelles ATA et de passerelles légères ATA dont vous avez besoin et la capacité de serveur pour votre centre ATA et les passerelles ATA.

## Dimensionnement du centre ATA
Le centre ATA nécessite l’équivalent de 30 jours de données qui est le minimum recommandé pour obtenir des analyses comportementales des utilisateurs. L’espace disque nécessaire pour la base de données ATA pour chaque contrôleur de domaine est indiqué ci-dessous. Si vous avez plusieurs contrôleurs de domaine, ajoutez l’espace disque requis par chaque contrôleur de domaine pour calculer l’espace total nécessaire pour la base de données ATA.
> [!NOTE] 
> En cas d’exécution en tant que machine virtuelle, la mémoire dynamique ou toute autre fonctionnalité d’augmentation de la mémoire n’est pas prise en charge.

|Paquets par seconde&#42;|Unité centrale (cœurs&#42;&#42;)|Mémoire (Go)|Stockage de la base de données par jour (Go)|Stockage de la base de données par mois (Go)|E/S par seconde&#42;&#42;&#42;|
|---------------------------|-------------------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1 000|2|32|0.3|9|30 (100)
|10 000|4|48|3|90|200 (300)
|40 000|8|64|12|360|500 (1,000)
|100 000|12|96|30|900|1 000 (1 500)
|400 000|40|128|120|1 800|2 000 (2 500)
&#42; Nombre total, moyen et quotidien de paquets par seconde provenant de l’ensemble des contrôleurs de domaine surveillés par l’ensemble des passerelles ATA.

&#42;&#42; Cela comprend des cœurs physiques et non des cœurs multithread.

&#42;&#42;&#42; Nombres moyens (pic)
> [!NOTE]
> -   Le centre ATA peut gérer un maximum agrégé de 400 000 images par seconde provenant de l’ensemble des contrôleurs de domaine surveillés.
> -   Les quantités de stockage citées ici sont des valeurs nettes. Vous devez toujours prendre en compte une croissance future et vous assurer que le disque sur lequel réside la base de données comprend au moins 20 % d’espace libre.
> -   Si l’espace libre atteint la valeur minimale de 20 % ou 100 Go, la collecte de données la plus ancienne est supprimée. Ce processus de suppression continuera jusqu’à atteindre l’équivalent de deux jours de données, ou bien 5 % ou 50 Go d’espace libre. Une fois ces valeurs atteintes, la collecte de données s’arrêtera.
> -  La latence de stockage pour les activités de lecture et d’écriture doit être inférieure à 10 ms.
> -  Le rapport entre les activités de lecture et d’écriture est d’environ 1 pour 3 en dessous de 100 000 paquets par seconde et de 1 pour 6 au-dessus de 100 000 paquets par seconde.

## Choix du type de passerelle appropriée pour votre déploiement
Dans un déploiement ATA, toutes les combinaisons de types de passerelles ATA sont prises en charge :

- Uniquement des passerelles ATA
- Uniquement des passerelles légères ATA
- Une combinaison des deux

Quand vous déterminez le type de déploiement de passerelle, considérez les facteurs suivants :

|Type de passerelle|Avantages|Coût|Topologie de déploiement|Utilisation des contrôleurs de domaine|
|----|----|----|----|-----|
|Passerelle ATA|Avec un déploiement hors bande, il est plus difficile pour les agresseurs de détecter qu’ATA est présent|Plus élevé|Installée en même temps que le contrôleur de domaine (hors bande)|Prend en charge jusqu’à 50 000 paquets par seconde|
|Passerelle légère ATA|Ne nécessite pas de configuration de la mise en miroir de port ni de serveur dédié|Plus faible|Installée sur un contrôleur de domaine|Prend en charge jusqu’à 10 000 paquets par seconde|

Voici quelques exemples de scénarios dans lesquels les contrôleurs de domaine doivent être couverts par la passerelle légère ATA :


- Sites de succursale

- Contrôleurs de domaine virtuels déployés dans le cloud (IaaS)


Voici quelques exemples de scénarios dans lesquels les contrôleurs de domaine doivent être couverts par la passerelle ATA :


- Siège social de centres de données (comptant des contrôleurs de domaine avec plus de 10 000 paquets par seconde)


## Dimensionnement de passerelle légère ATA

Une passerelle légère ATA peut prendre en charge la surveillance d’un contrôleur de domaine en fonction de la quantité de trafic réseau qu’il génère. 
> [!NOTE] 
> En cas d’exécution en tant que machine virtuelle, la mémoire dynamique ou toute autre fonctionnalité d’augmentation de la mémoire n’est pas prise en charge.

|Paquets par seconde&#42;|Unité centrale (cœurs&#42;&#42;)|Mémoire (Go)&#42;&#42;&#42;|
|---------------------------|-------------------------|---------------|
|1 000|2|6|
|5 000|6|16|
    |10 000|10|24|

&#42;Nombre total de paquets par seconde sur le contrôleur de domaine surveillé par une passerelle légère ATA donnée.

&#42;&#42;Quantité totale de cœurs non multithreads installés sur ce contrôleur de domaine.<br>Même si le multithread est acceptable pour la passerelle légère ATA, vous devez compter les cœurs réels et non les cœurs multithreads lors de la planification de la capacité.

&#42;&#42;&#42;Quantité totale de mémoire installée sur ce contrôleur de domaine.
> [!NOTE]   
> Si le contrôleur de domaine ne dispose pas de la quantité de ressources requise par la passerelle légère ATA, les performances du contrôleur de domaine ne seront pas affectées, mais la passerelle légère ATA risque de ne pas fonctionner comme prévu.


## Dimensionnement de la passerelle ATA

Prenez en compte les éléments suivants quand vous devez déterminer le nombre de passerelles ATA à déployer.

-   **Forêts et domaines Active Directory**<br>
    ATA peut surveiller le trafic provenant de plusieurs domaines d’une même forêt Active Directory. La surveillance de plusieurs forêts Active Directory nécessite des déploiements ATA distincts. Vous ne devez pas configurer un déploiement ATA unique pour surveiller le trafic réseau des contrôleurs de domaine de plusieurs forêts.

-   **Mise en miroir des ports**<br>
Les considérations relatives à la mise en miroir des ports peuvent vous amener à déployer plusieurs passerelles ATA par site de succursale ou centre de données.

-   **Capacité**<br>
    Une passerelle ATA peut prendre en charge la surveillance de plusieurs contrôleurs de domaine, en fonction de la quantité de trafic réseau des contrôleurs de domaine surveillés. 
<br>

> [!NOTE] 
> La mémoire dynamique n’est pas prise en charge.

|Paquets par seconde&#42;|Unité centrale (cœurs&#42;&#42;)|Mémoire (Go)|
|---------------------------|-------------------------|---------------|
|1 000|1|6|
|5 000|2|10|
|10 000|3|12|
|20,000|6|24|
|50 000|16|48|
&#42;Nombre total moyen de paquets par seconde provenant de l’ensemble des contrôleurs de domaine surveillés par une passerelle ATA donnée durant leur heure de la journée la plus occupée.

&#42; La quantité totale de trafic des contrôleurs de domaine avec mise en miroir des ports ne peut pas dépasser la capacité de la carte réseau de capture de la passerelle ATA.

&#42;&#42; L’hyper-threading doit être désactivé.



## Estimation du trafic des contrôleurs de domaine
Il existe différents outils qui permettent de détecter le nombre moyen de paquets par seconde de vos contrôleurs de domaine. Si vous n’avez pas d’outil permettant d’effectuer le suivi de ce compteur, vous pouvez utiliser l’Analyseur de performances pour collecter les informations nécessaires.

Pour déterminer le nombre de paquets par seconde, effectuez les opérations suivantes pour chaque contrôleur de domaine :

1.  Ouvrez l’Analyseur de performances.

    ![Image de l’Analyseur de performances](media/ATA-traffic-estimation-1.png)

2.  Développez **Ensembles de collecteurs de données**.

    ![Image d’Ensembles de collecteurs de données](media/ATA-traffic-estimation-2.png)

3.  Cliquez avec le bouton droit sur **Défini par l’utilisateur**, puis sélectionnez **Nouveau** &gt; **Ensemble de collecteurs de données**.

    ![Image du nouvel ensemble de collecteurs de données](media/ATA-traffic-estimation-3.png)

4.  Entrez un nom pour l’ensemble de collecteurs, puis sélectionnez **Créer manuellement (avancé)**.

5.  Sous **Quel type de données inclure ?**, sélectionnez **Créer des journaux de données et Compteur de performances**.

    ![Image du type de données pour le nouvel ensemble de collecteurs de données](media/ATA-traffic-estimation-5.png)

6.  Sous **Quels compteurs de performance enregistrer dans un journal ?**, cliquez sur **Ajouter**.

7.  Développez **Carte réseau**. Sélectionnez **Paquets/s**, puis l’instance appropriée. Si vous n’êtes pas sûr, vous pouvez sélectionner **&lt;Toutes les instances&gt;**, puis cliquer sur **Ajouter** et **OK**.

    > [!NOTE]
    > Pour ce faire, depuis la ligne de commande, exécutez `ipconfig /all` pour afficher le nom de la carte réseau et sa configuration.

    ![Image de l’ajout du compteur de performances](media/ATA-traffic-estimation-7.png)

8.  Définissez l’**Intervalle d’échantillonnage** sur **1 seconde**.

9. Définissez l’emplacement où vous voulez enregistrer les données.

10. Sous **Créer l’ensemble de collecteurs de données**, sélectionnez **Démarrer maintenant cet ensemble de collecteurs de données**, puis cliquez sur **Terminer**.

    Vous devez maintenant voir l’ensemble de collecteurs de données que vous venez de créer avec un triangle vert indiquant qu’il est activé.

11. Au bout de 24 heures, arrêtez l’ensemble de collecteurs de données en cliquant dessus avec le bouton droit et en sélectionnant **Arrêter**.

    ![Image de l’arrêt de l’ensemble de collecteurs de données](media/ATA-traffic-estimation-12.png)

12. Dans l’Explorateur de fichiers, accédez au dossier où le fichier .blg a été enregistré, puis double-cliquez dessus pour l’ouvrir dans l’Analyseur de performances.

13. Sélectionnez le compteur Paquets par seconde, puis enregistrez les valeurs moyenne et maximale.

    ![Image du compteur Paquets par seconde](media/ATA-traffic-estimation-14.png)

## Voir aussi
- [Configuration requise pour ATA](ata-prerequisites.md)
- [Architecture ATA](ata-architecture.md)
- [Consultez le forum ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->


