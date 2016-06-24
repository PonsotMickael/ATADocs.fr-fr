---
# required metadata

title: Planification de la capacité ATA | Microsoft Advanced Threat Analytics
description: Vous aide à déterminer le nombre de serveurs ATA qui seront nécessaires pour prendre en charge votre réseau
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 279d79f2-962c-4c6f-9702-29744a5d50e2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Planification de la capacité ATA
Cette rubrique vous aide à déterminer le nombre de serveurs ATA qui seront nécessaires pour prendre en charge votre réseau.

## Dimensionnement du centre ATA
Le centre ATA nécessite l’équivalent de 30 jours de données qui est le minimum recommandé pour obtenir des analyses comportementales des utilisateurs. L’espace disque nécessaire pour la base de données ATA pour chaque contrôleur de domaine est indiqué ci-dessous. Si vous avez plusieurs contrôleurs de domaine, ajoutez l’espace disque requis par chaque contrôleur de domaine pour calculer l’espace total nécessaire pour la base de données ATA.

|Paquets par seconde&#42;|Unité centrale (cœurs&#42;&#42;)|Mémoire (Go)|Stockage du système d’exploitation (Go)|Stockage de la base de données par jour (Go)|Stockage de la base de données par mois (Go)|E/S par seconde&#42;&#42;&#42;|
|---------------------------|-------------------------|---------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1 000|4|48|200|1.5|45|30 (100)
|10 000|4|48|200|15|450|200 (300)
|40 000|8|64|200|60|1 800|500 (1,000)
|100 000|12|96|200|150|4,500|1 000 (1 500)
|200 000|16|128|200|300|9 000|2 000 (2 500)
&#42; Nombre total, moyen et quotidien de paquets par seconde provenant de l’ensemble des contrôleurs de domaine surveillés par l’ensemble des passerelles ATA.

&#42;&#42; Cela comprend des cœurs physiques et non des cœurs multithread.

&#42;&#42;&#42; Nombres moyens (pic)
> [!NOTE]
> -   Le centre ATA peut gérer un maximum agrégé de 200 000 images par seconde provenant de l’ensemble des contrôleurs de domaine surveillés.
> -   Pour les déploiements à grande échelle (à partir de 100 000 paquets par seconde), le journal de la base de données doit se trouver sur un disque autre que celui de la base de données.
> -   Les quantités de stockage citées ici sont des valeurs nettes. Vous devez toujours prendre en compte une croissance future et vous assurer que le disque sur lequel réside la base de données comprend au moins 20 % d’espace libre.
> -   Si l’espace libre atteint la valeur minimale de 20 % ou 100 Go, les données les plus anciennes collectées au cours des dernières 24 heures seront supprimées. Ce processus de suppression continuera jusqu’à atteindre l’équivalent de deux jours de données, ou bien 5 % ou 50 Go d’espace libre. Une fois ces valeurs atteintes, la collecte de données s’arrêtera.
> -  La latence de stockage pour les activités de lecture et d’écriture doit être inférieure à 10 ms.
> -  Le rapport entre les activités de lecture et d’écriture est d’environ 1 pour 3 en dessous de 100 000 paquets par seconde et de 1 pour 6 au-dessus de 100 000 paquets par seconde.

## Dimensionnement de la passerelle ATA
Une passerelle ATA peut prendre en charge la surveillance de plusieurs contrôleurs de domaine, en fonction de la quantité de trafic réseau des contrôleurs de domaine surveillés.

|Paquets par seconde&#42;|Unité centrale (cœurs&#42;&#42;)|Mémoire (Go)|Stockage du système d’exploitation (Go)|
|---------------------------|-------------------------|---------------|-------------------|
|10 000|4|12|80|
|20,000|8|24|100|
|40 000|16|64|200|
&#42; Nombre total de paquets par seconde provenant de l’ensemble des contrôleurs de domaine surveillés par une passerelle ATA donnée.

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

11. Au bout de 24 heures, arrêtez l’ensemble de collecteurs de données. Pour cela, cliquez dessus avec le bouton droit, puis sélectionnez **Arrêter**

    ![Image de l’arrêt de l’ensemble de collecteurs de données](media/ATA-traffic-estimation-12.png)

12. Dans l’Explorateur de fichiers, accédez au dossier où le fichier .blg a été enregistré, puis double-cliquez dessus pour l’ouvrir dans l’Analyseur de performances.

13. Sélectionnez le compteur Paquets par seconde, puis enregistrez les valeurs moyenne et maximale.

    ![Image du compteur Paquets par seconde](media/ATA-traffic-estimation-14.png)

## Voir aussi
- [Configuration requise pour ATA](ata-prerequisites.md)
- [Architecture d’ATA](/advanced-threat-analytics/Understand/ata-architecture)
- [Pour obtenir de l’aide, consultez notre forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


