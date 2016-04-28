---
# required metadata

title: Installer ATA - Étape 5 | Microsoft Advanced Threat Analytics
description: La cinquième étape de la procédure d’installation d’ATA vous aide à configurer les paramètres de votre passerelle ATA.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Installer ATA - Étape 5

>[!div class="step-by-step"]
[« Étape 4](install-ata-step4.md)
[Étape 6 »](install-ata-step6.md)


## Étape 5. Configurer les paramètres de la passerelle ATA
Une fois la passerelle ATA installée, procédez comme suit pour configurer ses paramètres.

1.  Dans la console ATA de la machine de la passerelle ATA, cliquez sur **Configuration**, puis sélectionnez la page **Passerelles ATA**.

2.  Entrez les informations suivantes.



  - **Description** : <br>Entrez une description de la passerelle ATA (facultatif).
  - **Contrôleurs de domaine** (obligatoire) : <br>Voir plus bas pour plus d’informations sur la liste des contrôleurs.<br>Entrez le nom de domaine complet de votre contrôleur de domaine et cliquez sur le signe plus (+) pour l’ajouter à la liste. Par exemple, **dc01.contoso.com**.<br /><br />![Image d’un exemple de nom de domaine complet](media/ATAGWDomainController.png)<br>Les objets du premier contrôleur de domaine dans la liste sont synchronisés au moyen de requêtes LDAP. Selon la taille du domaine, cette opération peut prendre du temps.<br>
  **Remarque :** <br>Vérifiez que le premier contrôleur de domaine **n’est pas** en lecture seule. Les contrôleurs de domaine en lecture seule doivent être ajoutés uniquement au terme de la synchronisation initiale.<br>


 - **Adaptateurs de réseau de capture** (obligatoire) :<br>Sélectionnez parmi les cartes réseau connectées au commutateur celles qui sont configurées en tant que port miroir de destination pour recevoir le trafic du contrôleur de domaine.|Sélectionnez la carte réseau de capture.
    ![Image de la configuration des paramètres de la passerelle](media/ATA-Config-GW-Settings.jpg)

3.  Cliquez sur **Enregistrer**.

    > [!NOTE]
    > Le démarrage initial du service de la passerelle ATA nécessite quelques minutes, car il construit le cache des analyseurs de capture réseau utilisés par la passerelle ATA.

Les informations suivantes s’appliquent aux serveurs que vous entrez dans la liste **Contrôleurs de domaine**.

-   Le premier contrôleur de domaine de la liste est utilisé par la passerelle ATA pour synchroniser les objets de domaine au moyen de requêtes LDAP. Selon la taille du domaine, cette opération peut prendre du temps.

-   Tous les contrôleurs de domaine dont le trafic est surveillé par l’intermédiaire de la mise en miroir des ports par la passerelle ATA doivent figurer dans la liste **Contrôleurs de domaine**. Si un contrôleur de domaine n’est pas répertorié dans la liste **Contrôleurs de domaine**, il est possible que la détection des activités suspectes ne fonctionne pas comme prévu.

-   Vérifiez que le premier contrôleur de domaine **n’est pas** un contrôleur de domaine en lecture seule.

    Les contrôleurs de domaine en lecture seule doivent être ajoutés uniquement au terme de la synchronisation initiale.

-   Au moins un contrôleur de domaine figurant dans la liste doit être un serveur de catalogue global. ATA peut ainsi résoudre les objets ordinateur et utilisateur dans d’autres domaines de la forêt.

Les modifications de configuration sont appliquées à la passerelle ATA lors de la prochaine synchronisation planifiée entre la passerelle ATA et le centre ATA.

### Validez l’installation :
Pour vous assurer que la passerelle ATA a été déployée avec succès, effectuez les vérifications suivantes :

1.  Vérifiez que le service Microsoft Advanced Threat Analytics Center est en cours d’exécution. Après avoir enregistré les paramètres de la passerelle ATA, vous devrez peut-être patienter quelques minutes avant le démarrage du service.

2.  Si le service ne démarre pas, examinez le fichier Microsoft.Tri.Gateway-Errors.log situé dans le dossier par défaut suivant : %programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs. Recherchez les entrées contenant « transfer » ou « service start ».

3.  Vérifiez les compteurs de performances suivants de la passerelle Microsoft ATA :

    -   **Messages capturés par NetworkListener/s** : ce compteur fait le suivi du nombre de messages capturés par ATA par seconde. En fonction du nombre de contrôleurs de domaine surveillés et du niveau d’activité de chaque contrôleur de domaine, la valeur doit être de l’ordre de quelques centaines voire de quelques milliers. Des valeurs à un ou deux chiffres peuvent indiquer un problème lié à la configuration de la mise en miroir des ports.

    -   **Transferts d’activité EntityTransfer/s** : cette valeur doit être de l’ordre de quelques centaines dans un intervalle de quelques secondes.

4.  S’il s’agit de la première passerelle ATA installée, patientez quelques minutes, puis connectez-vous à la console ATA. Ouvrez ensuite le volet de notification en effectuant un mouvement de balayage à partir du côté droit de l’écran. La liste **Entités apprises récemment	** doit s’afficher dans la barre de notification à droite de la console.

5.  Pour vérifier que l’installation a été correctement effectuée :

    Dans la console, recherchez un élément dans la barre de recherche, comme un utilisateur ou un groupe sur votre domaine.

    Ouvrez l’Analyseur de performances. Dans l’arborescence des performances, cliquez sur **Analyseur de performances**, puis sur l’icône du signe Plus (+) pour **Ajouter un compteur**. Développez ** Passerelle Microsoft ATA**, puis descendez dans la liste jusqu’au compteur **Messages capturés par NetworkListener/s** et ajoutez-le. Vérifiez que l’activité apparaît sur le graphique.

    ![Image de l’ajout du compteur de performances](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"]
[« Étape 4](install-ata-step4.md)
[Étape 6 »](install-ata-step6.md)

## Voir aussi

- [Pour obtenir de l’aide, consultez notre forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurer la collecte d’événements](/advanced-threat-analytics/plandesign/configure-event-collection)
- [Conditions préalables au déploiement d’ATA](/advanced-threat-analytics/plandesign/ata-prerequisites)


<!--HONumber=Apr16_HO2-->


