---
title: "Installer ATA - Étape 1 | Microsoft Advanced Threat Analytics"
description: "La première étape de la procédure d’installation d’ATA consiste à télécharger le centre ATA et à l’installer sur le serveur de votre choix."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d6e7d7bef97bfc4ffde07959dd9256f0319d685f
ms.openlocfilehash: c89d4d6f6af58bcc822b9599dcda65d0719a7419


---

# Installer ATA - Étape 1

>[!div class="step-by-step"]

[Étape 2 »](install-ata-step2.md)

Cette procédure d’installation fournit des instructions pour effectuer une nouvelle installation d’ATA 1.6. Pour plus d’informations sur la mise à jour d’un déploiement d’ATA existant à partir d’une version antérieure, consultez le [guide de migration d’ATA pour la version 1.6](/advanced-threat-analytics/understand-explore/ata-update-1.6-migration-guide).

> [!IMPORTANT] 
> Installez la mise à jour KB2934520 sur le serveur du centre ATA et sur les serveurs de passerelle ATA avant de lancer l’installation ; sinon, le programme d’installation d’ATA installera cette mise à jour et nécessitera un redémarrage pendant l’installation d’ATA.

## Étape 1. Télécharger et installer le centre ATA
Après avoir vérifié que le serveur répond à la configuration requise, vous pouvez passer à l’installation du centre ATA.

Effectuez les opérations suivantes sur le serveur du centre ATA.

1.  Téléchargez ATA à partir du [Centre de gestion des licences en volume Microsoft](https://www.microsoft.com/Licensing/servicecenter/default.aspx), du [Centre d’évaluation TechNet](http://www.microsoft.com/evalcenter/) ou de [MSDN](https://msdn.microsoft.com/subscriptions/downloads).

2.  Connectez-vous à l’ordinateur sur lequel vous installez le centre ATA en tant qu’utilisateur membre du groupe Administrateurs local.

3.  Exécutez **Microsoft ATA Center Setup.EXE**, puis suivez les instructions de l’Assistant Installation.

4.  Si Microsoft .Net Framework n’est pas installé, vous êtes invité à l’installer quand vous démarrez l’installation. Vous pouvez être invité à effectuer un redémarrage après avoir installé le .NET Framework.
5.  Dans la page **Bienvenue**, sélectionnez la langue à utiliser pour les écrans d’installation d’ATA et cliquez sur **Suivant**.

6.  Lisez les termes du contrat de licence logiciel Microsoft et, si vous les acceptez, cochez la case, puis cliquez sur **Suivant**.

7.  Nous vous recommandons de définir ATA de manière à ce qu’il se mette à jour automatiquement. Si Windows n’est pas configuré en ce sens sur votre ordinateur, l’écran **Utilisez Microsoft Update pour garder votre ordinateur à jour et en sécurité** apparaît. 
    ![Image montrant comment maintenir ATA à jour](media/ata_ms_update.png)

8. Sélectionnez **Utiliser Microsoft Update lorsque je recherche des mises à jour (recommandé)**. Ainsi, Windows est configuré de manière à récupérer les mises à jour des autres produits Microsoft (y compris ATA), comme illustré ci-après. 
    ![Image de mise à jour automatique de Windows](media/ata_installupdatesautomatically.png)

8.  Dans la page **Configuration du centre ATA**, entrez les informations suivantes en fonction de votre environnement :

    |Champ|Description|Commentaires|
    |---------|---------------|------------|
    |Chemin d’installation|Il s’agit de l’emplacement où est installé le centre ATA. L’emplacement par défaut est le suivant : %programfiles%\Microsoft Advanced Threat Analytics\Center.|Conservez la valeur par défaut.|
    |Chemin d’accès des données de la base de données|Il s’agit de l’emplacement dans lequel les fichiers de la base de données MongoDB sont enregistrés. L’emplacement par défaut est le suivant : %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data.|Modifiez cette valeur pour pointer vers un emplacement capable de prendre en charge l’évolution de vos besoins en matière de redimensionnement. **Remarque :** <ul><li>Dans les environnements de production, vous devez utiliser un lecteur avec suffisamment d'espace (tel que déterminé par la planification de la capacité).</li><li>Pour les déploiements volumineux, la base de données doit figurer sur un disque physique distinct.</li></ul>Pour plus d’informations sur le redimensionnement, consultez [Planification de la capacité ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning).|
    |Adresse IP du service du centre ATA : port|Il s’agit de l’adresse IP sur laquelle le service du centre ATA écoute les communications en provenance des passerelles ATA.<br /><br />**Port par défaut :** 443|Cliquez sur la flèche vers le bas pour sélectionner l’adresse IP à utiliser par le service du centre ATA.<br /><br />L’adresse IP et le port du service du centre ATA ne peuvent pas être identiques à ceux de la console ATA. Veillez à modifier le port de la console ATA.|
    |Certificat SSL du service du centre ATA|Il s’agit du certificat utilisé par le service du centre ATA.|Cliquez sur l’icône en forme de clé pour sélectionner un certificat installé ou cochez la case Créer un certificat auto-signé lors du déploiement dans un environnement lab.|
    |Adresse IP de la console ATA|Il s’agit de l’adresse IP utilisée par IIS pour la console ATA.|Cliquez sur la flèche vers le bas pour sélectionner l’adresse IP utilisée par la console ATA. **Remarque :** notez cette adresse IP pour faciliter l’accès à la console ATA à partir de la passerelle ATA.|
    |Certificat SSL de la console ATA|Il s’agit du certificat à utiliser par IIS.|Cliquez sur l’icône en forme de clé pour sélectionner un certificat installé ou cochez la case Créer un certificat auto-signé lors du déploiement dans un environnement lab.|

    ![Image de la configuration du centre ATA](media/ATA-Center-Configuration.JPG)

10.  Cliquez sur **Installer** pour installer le centre ATA et ses composants.
    Les composants suivants sont installés et configurés pendant l’installation du centre ATA :

    -   Internet Information Services (IIS)

    -   Service du centre ATA et site IIS de la console ATA

    -   MongoDB

    -   Jeu d’éléments de collecte de données de l’Analyseur de performances personnalisé

    -   Certificats auto-signés (s’ils ont été sélectionnés pendant l’installation)

11.  Une fois l’installation terminée, cliquez sur **Lancer** pour vous connecter à la console ATA.
À ce stade, la page de paramètres **Général** s’affiche automatiquement pour vous permettre de poursuivre la configuration et le déploiement des passerelles ATA.
Étant donné que vous vous connectez au site à l’aide d’une adresse IP, vous recevez un avertissement lié au certificat. Ce comportement étant normal, cliquez sur **Poursuivre sur ce site web**.

### Valider l’installation

1.  Vérifiez que le service nommé **Microsoft Advanced Threat Analytics Center** est en cours d’exécution.
2.  Sur le Bureau, cliquez sur le raccourci **Microsoft Advanced Threat Analytics** pour vous connecter à la console ATA. Connectez-vous avec les mêmes informations d’identification utilisateur que celles que vous avez utilisées pour installer le centre ATA.



>[!div class="step-by-step"]
[« Préinstallation](preinstall-ata.md)
[Étape 2 »](install-ata-step2.md)

## Voir aussi

- [Consultez le forum ATA](https://social.technet.microsoft.com/Forums/security/
- home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Conditions préalables au déploiement d’ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jun16_HO4-->


