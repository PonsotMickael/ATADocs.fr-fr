---
title: "Récupération d’urgence pour Advanced Threat Analytics | Microsoft Docs"
description: "Décrit comment vous pouvez récupérer rapidement les fonctionnalités ATA après un sinistre"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 02/28/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7620e171-76d5-4e3f-8b03-871678217a3a
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: e315e9731fa9715c3b41b9292349ee5aca13fbce
ms.sourcegitcommit: 4f5927f30089655e3984d69623ea4439b7c36845
translationtype: HT
---
*S’applique à : Advanced Threat Analytics version 1.7*



# <a name="ata-disaster-recovery"></a>Récupération d’urgence d’ATA
Cet article décrit comment récupérer rapidement votre centre ATA et restaurer les fonctionnalités ATA quand le centre ATA a cessé de fonctionner, mais que les passerelles ATA fonctionnent encore. 

>[!NOTE]
> Le processus décrit ne récupère pas les activités suspectes détectées précédemment, mais rétablit le fonctionnement intégral du centre ATA. En outre, la période d’apprentissage nécessaire pour certaines détections de comportements redémarre, la majeure partie de la détection offerte par ATA étant néanmoins opérationnelle une fois le centre ATA restauré. 

## <a name="back-up-your-ata-center-configuration"></a>Sauvegarder votre configuration du centre ATA

1. La configuration du centre ATA est sauvegardée dans un fichier toutes les heures. Recherchez la dernière copie de sauvegarde de la configuration du centre ATA et enregistrez-la sur un ordinateur distinct. Pour obtenir une explication complète de la localisation de ces fichiers, consultez [Exporter et importer la configuration ATA](/advanced-threat-analytics/deploy-use/ata-configuration-file). 
2. Exportez le certificat du centre ATA.
    1. Dans le Gestionnaire de certificats (`certlm.msc`), accédez à **Certificats (ordinateur local)** -> **Personnel** ->**Certificats**, puis sélectionnez **Centre ATA**.
    2. Cliquez avec le bouton droit sur **Centre ATA** et sélectionnez **Toutes les tâches** puis **Exportation**. 
     ![Certificat du centre ATA](media/ata-center-cert.png)
    3. Suivez les instructions pour exporter le certificat, en veillant à exporter également la clé privée.
    4. Sauvegardez le fichier de certificat exporté sur un ordinateur distinct.

  > [!NOTE] 
  > Si vous ne pouvez pas exporter la clé privée, vous devez créer un nouveau certificat et le déployer sur ATA, comme décrit dans [Changer le certificat du centre ATA](/advanced-threat-analytics/deploy-use/modifying-ata-config-centercert), puis l’exporter. 

## <a name="recover-your-ata-center"></a>Récupérer votre centre ATA

1. Créez un ordinateur Windows Server en utilisant la même adresse IP et le même nom d’ordinateur que l’ordinateur du centre ATA précédent.
4. Importez le certificat que vous avez sauvegardé à l’étape précédente sur le nouveau serveur.
5. Suivez les instructions pour [déployer le centre ATA](/advanced-threat-analytics/deploy-use/install-ata-step1) sur le serveur Windows qui vient d’être créé. Veillez à sélectionner la même adresse IP et le même port que sur l’ancien centre. Il est inutile de redéployer les passerelles ATA. Lorsque vous êtes invité à fournir un certificat, fournissez le certificat que vous avez exporté lors de la sauvegarde de la configuration du centre ATA. 
![Restauration du centre ATA](media/ata-center-restore.png)
6. Importez la configuration sauvegardée du centre ATA :
    1. Supprimez le document du profil système du centre ATA par défaut dans MongoDB : 
        1. Accédez à **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**. 
        2. Exécutez `mongo.exe ATA` 
        3. Exécutez cette commande pour supprimer le profil système par défaut : `db.SystemProfile.remove({})`
    2. Exécutez la commande : `mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert` en utilisant le fichier de sauvegarde de l’étape 1.</br>
    Pour obtenir une explication complète de la localisation et de l’importation des fichiers de sauvegarde, consultez [Exporter et importer la configuration ATA](/advanced-threat-analytics/deploy-use/ata-configuration-file). 
    3. Après l’importation, exécutez cette commande pour supprimer une partie des profils système par défaut (pour les réinitialiser pour le nouvel environnement) : `db.SystemProfile.remove({$or:[{"_t":"DetectorProfile"}, "_t":"DirectoryServicesSystemProfile"}]}) `
    4. Ouvrez la console ATA. Vous devez normalement voir toutes les passerelles ATA liées sous l’onglet Configuration/Passerelles. 
    5. Veillez à définir un [**utilisateur des services d’annuaire**](/advanced-threat-analytics/deploy-use/install-ata-step2) et à choisir un [**synchronisateur de contrôleur de domaine**](/advanced-threat-analytics/deploy-use/install-ata-step5). 






## <a name="see-also"></a>Voir aussi
- [Prérequis au déploiement d’ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planification de la capacité d’ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurer la collecte d’événements](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configuration du transfert d’événements Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
