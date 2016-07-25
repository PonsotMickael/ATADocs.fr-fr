---
title: "Installer ATA - Étape 5 | Microsoft ATA"
description: "La cinquième étape de la procédure d’installation d’ATA vous aide à configurer les paramètres de votre passerelle ATA."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 3e9f68e9868dc9aaf20fe9d1c4fe2b8bdd685291


---

# Installer ATA - Étape 5

>[!div class="step-by-step"]
[« Étape 4](install-ata-step4.md)
[Étape 6 »](install-ata-step6.md)


## Étape 5. Configurer les paramètres de la passerelle ATA
Une fois la passerelle ATA installée, procédez comme suit pour configurer ses paramètres.

1.  Dans la console ATA, cliquez sur **Configuration**, puis sélectionnez la page **Passerelles ATA**.

2.  Entrez les informations suivantes.

  - **Description** : <br>Entrez une description de la passerelle ATA (facultatif).
  - **Contrôleurs de domaine de port d’écoute (FQDN)** (requis pour la passerelle ATA, ce paramètre ne peut pas être défini pour la passerelle légère ATA) : <br>Entrez le nom de domaine complet de votre contrôleur de domaine et cliquez sur le signe plus (+) pour l’ajouter à la liste. Par exemple, **dc01.contoso.com**.<br /><br />![Image d’un exemple de nom de domaine complet](media/ATAGWDomainController.png)

Les informations suivantes s’appliquent aux serveurs que vous entrez dans la liste **Contrôleurs de domaine** : - Tous les contrôleurs de domaine dont le trafic est surveillé par l’intermédiaire de la mise en miroir des ports par la passerelle ATA doivent figurer dans la liste **Contrôleurs de domaine**. Si un contrôleur de domaine n’est pas répertorié dans la liste **Contrôleurs de domaine**, il est possible que la détection des activités suspectes ne fonctionne pas comme prévu.
- Au moins un contrôleur de domaine figurant dans la liste doit être un serveur de catalogue global. ATA peut ainsi résoudre les objets ordinateur et utilisateur dans d’autres domaines de la forêt.

 - **Adaptateurs de réseau de capture** (obligatoire) :<br>
     - Dans le cas d’une passerelle ATA sur un serveur dédié, sélectionnez les cartes réseau qui sont configurées en tant que port miroir de destination. Elles recevront le trafic du contrôleur de domaine mis en miroir.
     - Dans le cas d’une passerelle légère ATA, il doit s’agir de toutes les cartes réseau utilisées pour la communication avec les autres ordinateurs de votre organisation.

![Image de la configuration des paramètres de la passerelle](media/ATA-Config-GW-Settings.jpg)

 - **Candidat synchronisateur de domaine**<br>
Toute passerelle ATA définie comme candidat synchronisateur de domaine peut être responsable de la synchronisation entre ATA et votre domaine Active Directory. Suivant la taille du domaine, la synchronisation initiale peut prendre un certain temps et consomme beaucoup de ressources. Par défaut, seules les passerelles ATA sont définies comme candidats synchronisateurs de domaine. <br>Dans la mesure du possible, évitez qu’une passerelle ATA de site distant soit candidat synchronisateur de domaine.<br>Si votre contrôleur de domaine est en lecture seule, ne le définissez pas comme candidat synchronisateur de domaine. Pour plus d’informations, consultez [ATA architecture](/advanced-threat-analytics/plan-design/ata-architecture#ata-lightweight-gateway-features) (Architecture d’ATA).

> [!NOTE] 
> Le démarrage initial du service de la passerelle ATA prend quelques minutes, car il construit le cache des analyseurs de capture réseau.<br>
> Les modifications de configuration sont appliquées à la passerelle ATA lors de la prochaine synchronisation planifiée entre la passerelle ATA et le centre ATA.



    

3. Si vous le souhaitez, vous pouvez définir le [détecteur Syslog et la collecte des transferts d’événements Windows](configure-event-collection.md). 
4. Activez **Mettre la passerelle ATA à jour automatiquement** pour que cette passerelle ATA soit automatiquement mise à jour si vous mettez à jour le centre ATA à l’occasion de futures publications de version.
3.  Cliquez sur **Enregistrer**.


## Valider les installations
Pour vous assurer que la passerelle ATA a été déployée avec succès, effectuez les vérifications suivantes :

1.  Vérifiez que le service nommé **Microsoft Advanced Threat Analytics Gateway** est en cours d’exécution. Après avoir enregistré les paramètres de la passerelle ATA, vous devrez peut-être patienter quelques minutes avant le démarrage du service.

2.  Si le service ne démarre pas, examinez le fichier Microsoft.Tri.Gateway-Errors.log situé dans le dossier par défaut suivant : %programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs.

3.  Pour obtenir de l’aide, consultez [ATA Troubleshooting](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-known-errors) (Résolution des problèmes liés à ATA).

4.  S’il s’agit de la première passerelle ATA installée, patientez quelques minutes, puis connectez-vous à la console ATA. Ouvrez ensuite le volet de notification en effectuant un mouvement de balayage à partir du côté droit de l’écran. La liste **Entités apprises récemment	** doit s’afficher dans la barre de notification à droite de la console.

5.  Sur le Bureau, cliquez sur le raccourci **Microsoft Advanced Threat Analytics** pour vous connecter à la console ATA. Connectez-vous avec les mêmes informations d’identification utilisateur que celles que vous avez utilisées pour installer le centre ATA.
6.  Dans la console, recherchez un élément dans la barre de recherche, comme un utilisateur ou un groupe sur votre domaine.
7.  Ouvrez l’Analyseur de performances. Dans l’arborescence des performances, cliquez sur **Analyseur de performances**, puis sur l’icône du signe Plus (+) pour **Ajouter un compteur**. Développez **Passerelle Microsoft ATA**, puis descendez dans la liste jusqu’au compteur **Messages capturés par Network Listener PEF/s** et ajoutez-le. Vérifiez que l’activité apparaît sur le graphique.

    ![Image de l’ajout du compteur de performances](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"]
[« Étape 4](install-ata-step4.md)
[Étape 6 »](install-ata-step6.md)

## Voir aussi

- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Conditions préalables au déploiement d’ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jul16_HO3-->


