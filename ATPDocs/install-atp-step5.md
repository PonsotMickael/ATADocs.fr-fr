---
title: "Installer Azure - Protection avancée contre les menaces – Étape 5 | Microsoft Docs"
description: "L’étape 5 de la procédure d’installation d’Azure ATP permet de configurer les paramètres du capteur autonome Azure ATP."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: d7c95f8c-04f8-4946-9bae-c27ed362fcb0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a2e61758e06aedfe607afc0d3365227af872fe20
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2018
---
*S’applique à : Azure - Protection avancée contre les menaces*



# <a name="install-azure-atp---step-5"></a>Installer Azure ATP – Étape 5

>[!div class="step-by-step"]
[« Étape 4](install-atp-step4.md)
[Étape 6 »](install-atp-step6-vpn.md)


## <a name="step-5-configure-the-azure-atp-sensor-settings"></a>Étape 5. Configurer les paramètres du capteur Azure ATP
Une fois le capteur Azure ATP installé, effectuez les étapes suivantes pour configurer ses paramètres.

1.  Dans le portail d’espace de travail Azure ATP, accédez à **Configuration** et, sous **Système**, sélectionnez **capteur**.
   
     ![Image de la configuration des paramètres du capteur](media/atp-sensor-config.png)


2.  Cliquez sur le capteur que vous voulez configurer et entrez les informations suivantes :

    ![Image de la configuration des paramètres du capteur](media/atp-sensor-config-2.png)

  - **Description** : entrez une description pour le capteur Azure ATP (facultatif).
  - **Contrôleurs de domaine (FQDN)** (obligatoire pour le capteur autonome Azure ATP, ne peut pas être modifié pour le capteur Azure ATP) : entrez le nom de domaine complet de votre contrôleur de domaine et cliquez sur le signe plus (+) pour l’ajouter à la liste. Par exemple, **dc01.contoso.com**.

      Les informations suivantes s’appliquent aux serveurs que vous entrez dans la liste **Contrôleurs de domaine** :
      - Tous les contrôleurs de domaine dont le trafic est surveillé par l’intermédiaire de la mise en miroir des ports par le capteur autonome Azure ATP doivent figurer dans la liste **Contrôleurs de domaine**. Si un contrôleur de domaine n’est pas répertorié dans la liste **Contrôleurs de domaine**, il est possible que la détection des activités suspectes ne fonctionne pas comme prévu.
      - Au moins un contrôleur de domaine figurant dans la liste doit être un catalogue général. Azure ATP peut ainsi résoudre les objets d’ordinateur et d’utilisateur dans d’autres domaines de la forêt.

  - **Adaptateurs de réseau de capture** (obligatoire) :
     - Dans le cas d’un capteur autonome Azure ATP sur un serveur dédié, sélectionnez les cartes réseau qui sont configurées en tant que port miroir de destination. Elles reçoivent le trafic du contrôleur de domaine mis en miroir.
     - Dans le cas d’un capteur Azure ATP, il doit s’agir de toutes les cartes réseau utilisées pour la communication avec les autres ordinateurs de votre organisation.


  - **Candidat synchronisateur de domaine** : tout capteur autonome Azure ATP défini comme candidat synchronisateur de domaine peut être responsable de la synchronisation entre Azure ATP et votre domaine Active Directory. Suivant la taille du domaine, la synchronisation initiale peut prendre un certain temps et consommer beaucoup de ressources. Par défaut, seuls les capteurs autonomes Azure ATP sont définis comme candidats synchronisateurs de domaine.
   Dans la mesure du possible, évitez qu’un capteur autonome Azure ATP de site distant soit candidat synchronisateur de domaine.
   Si votre contrôleur de domaine est en lecture seule, ne le définissez pas comme candidat synchronisateur de domaine. Pour plus d'informations, consultez [Architecture Azure ATP](atp-architecture.md#azure-atp-sensor-features).
  
4. Cliquez sur **Enregistrer**.


## <a name="validate-installations"></a>Valider les installations
Pour vous assurer que le capteur Azure ATP a été déployé avec succès, effectuez les étapes suivantes :

1.  Vérifiez que le service nommé **Capteur Azure - Protection avancée contre les menaces** est en cours d’exécution. Après avoir enregistré les paramètres du capteur Azure ATP, vous devrez peut-être patienter quelques secondes avant le démarrage du service.

2.  Si le service ne démarre pas, examinez le fichier Microsoft.Tri.sensor-Errors.log situé dans le dossier par défaut suivant : %programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs.
 
 >[!NOTE]
 > La version d’Azure ATP est fréquemment mise à jour. Pour vérifier la version la plus récente, dans le portail d’espace de travail Azure ATP, accédez à **Configuration**, puis à **A propos**. 

3.  Accédez à l’URL de votre espace de travail. Dans le portail d’espace de travail, recherchez un élément dans la barre de recherche, tel qu’un utilisateur ou un groupe sur votre domaine.



>[!div class="step-by-step"]
[« Étape 4](install-atp-step4.md)
[Étape 6 »](install-atp-step6-vpn.md)


## <a name="see-also"></a>Voir aussi

- [Outil de dimensionnement Azure ATP](http://aka.ms/aatpsizingtool)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Prérequis d’Azure ATP](atp-prerequisites.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)
