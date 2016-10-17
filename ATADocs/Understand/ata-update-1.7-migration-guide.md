---
title: "Mise à jour d’ATA vers la version 1.7 : guide de migration | Microsoft ATA"
description: "Procédures pour mettre à jour ATA vers la version 1.7"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e3b690767e5c6f5561a97a73eccfbf50ddb04148
ms.openlocfilehash: 5c20c41c3fe587f18087d64f4f84c1df65072fde


---

# Mise à jour d’ATA vers la version 1.7 : guide de migration
La mise à jour vers ATA 1.7 comprend des améliorations dans les domaines suivants :

-   Nouvelles détections

-   Détections existantes plus efficaces
  

## Mise à jour d’ATA vers la version 1.7
> [!NOTE] 
> Si ATA n’est pas installé dans votre environnement, téléchargez la version complète d’ATA qui inclut la version 1.7. Suivez ensuite la procédure d’installation standard décrite dans [Installer ATA](/advanced-threat-analytics/deploy-use/install-ata).

Si vous avez déjà déployé ATA version 1.6, cette procédure vous guide tout au long des étapes nécessaires pour mettre à jour votre déploiement.

> [!NOTE] 
> Vous ne pouvez pas installer ATA version 1.7 directement sur ATA version 1.4 ou 1.5. Vous devez d’abord installer ATA version 1.6. 

Suivez ces étapes pour mettre à jour ATA vers la version 1.7 :

1.  [Télécharger la mise à jour vers la version 1.7](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
Dans cette version, le même fichier d’installation (Microsoft ATA Center Setup.exe) est utilisé pour l’installation d’un nouveau déploiement d’ATA et la mise à niveau des déploiements existants.

2.  Mettez à jour le centre ATA.

4.  Mettez à jour les passerelles ATA.

    > [!IMPORTANT]
    > Pour assurer le bon fonctionnement d’ATA, mettez à jour toutes les passerelles.

### Étape 1 : mettre à jour le centre ATA

1.  Sauvegardez votre base de données (facultatif) :

    -   Si le centre ATA s’exécute en tant que machine virtuelle et que vous souhaitez effectuer un point de contrôle, commencez par arrêter la machine virtuelle.

    -   Si le centre ATA s’exécute sur un serveur physique, suivez la procédure recommandée pour [sauvegarder MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Exécutez le fichier d’installation, **Microsoft ATA Center Setup.exe**, puis suivez les instructions à l’écran pour installer la mise à jour.

    -  Dans la page **Bienvenue**, sélectionnez votre langue, puis cliquez sur **Suivant**.

    -  Si vous n’avez pas activé les mises à jour automatiques dans la version 1.6, vous serez invité à configurer ATA pour utiliser Microsoft Update pour ATA pour rester à jour.  Dans la page Microsoft Update, sélectionnez **Utiliser Microsoft Update lorsque je recherche des mises à jour (recommandé)**.
    ![Image montrant comment maintenir ATA à jour](media/ata_ms_update.png) Ainsi, Windows est configuré de manière à récupérer les mises à jour des autres produits Microsoft (y compris ATA), comme illustré ci-après. 
     ![Image de mise à jour automatique de Windows](media/ata_installupdatesautomatically.png)

    -  Dans l’écran **Migration des données**, indiquez si vous souhaitez migrer tout ou une partie des données. Si vous choisissez de migrer uniquement des données partielles, vos profils de comportement et de trafic réseau capturés précédemment ne seront pas migrés. Cela signifie qu’il faudra trois semaines avant que la détection d’un comportement anormal ait un profil complet pour activer la détection d’activité anormale. Pendant ces trois semaines, toutes les autres détections ATA fonctionneront correctement. L’installation de la migration des données **Partielle** prend beaucoup moins de temps. Si vous sélectionnez la migration des données **Complète**, l’installation peut prendre beaucoup plus de temps. La durée estimée et l’espace disque requis, qui sont répertoriés dans l’écran **Migration des données**, dépendent de la quantité de trafic de réseau capturée, précédemment enregistrée dans les versions précédentes d’ATA. Avant de sélectionner **Partielle** ou **Complète**, veillez à vérifier ces exigences.  
    
    ![Migration des données ATA](media/migration data migration.png)

    -  Cliquez sur **Mettre à jour**. Une fois que vous avez cliqué sur Mettre à jour, ATA passe en mode hors connexion jusqu’à la fin de la mise à jour.

4.  Une fois la mise à jour du centre ATA terminée, cliquez sur **Lancer** pour afficher l’écran **Mettre à jour** dans la console ATA pour les passerelles ATA.
    ![Écran de réussite de mise à jour](media/migration center success.png)

5.  Dans l’écran **Mises à jour**, si vous avez déjà configuré vos passerelles ATA pour une mise à jour automatique, elles seront mises à jour à ce stade. Sinon, cliquez sur **Mettre à jour** en regard de chaque passerelle ATA.
  ![Image de mise à jour des passerelles](media/migration update gw.png)

  
> [!IMPORTANT] 
> Pour assurer le bon fonctionnement d’ATA, mettez à jour toutes les passerelles.
> Le port d’écoute Syslog configuré sur toutes les passerelles sera modifié : il s’agira du port 514.
 
    > [!NOTE] 
    > To install new ATA Gateways, go the **Gateways** screen and click **Download Gateway Setup** to get the ATA 1.7 installation package and follow the instructions for new Gateway installation as described in [Step 4. Install the ATA Gateway](/advanced-threat-analytics/deploy-use/install-ata-step4) .



## Voir aussi

- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Oct16_HO1-->

