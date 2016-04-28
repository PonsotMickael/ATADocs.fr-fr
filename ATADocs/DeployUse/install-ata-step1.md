---
# required metadata

title: Installer ATA - Étape 1 | Microsoft Advanced Threat Analytics
description: La première étape de la procédure d’installation d’ATA consiste à télécharger le centre ATA et à l’installer sur le serveur de votre choix.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Installer ATA - Étape 1

>[!div class="step-by-step"]
[« Pré-installation](install-ata-preinstall.md)
[Étape 2 »](install-ata-step2.md)

## Étape 1. Télécharger et installer le centre ATA
Après avoir vérifié que le serveur répond à la configuration requise, vous pouvez passer à l’installation du centre ATA.

Effectuez les opérations suivantes sur le serveur du centre ATA.

1.  Téléchargez ATA à partir du [Centre d’évaluation TechNet](http://www.microsoft.com/en-us/evalcenter/).

2.  Connectez-vous en tant qu’utilisateur membre du groupe d’administrateurs local.

3.  À partir d’une invite de commandes avec élévation de privilèges, exécutez Microsoft ATA Center Setup.EXE, puis suivez les instructions de l’Assistant Installation.

4.  Dans la page **Bienvenue**, sélectionnez votre langue, puis cliquez sur **Suivant**.

5.  Lisez le Contrat de Licence Utilisateur Final et, si vous en acceptez les termes, cliquez sur **Suivant**.

6.  Dans la page **Configuration du centre**, entrez les informations suivantes en fonction de votre environnement :

    |Champ|Description|Commentaires|
    |---------|---------------|------------|
    |Chemin d’installation|Il s’agit de l’emplacement où est installé le centre ATA. L’emplacement par défaut est le suivant : %programfiles%\Microsoft Advanced Threat Analytics\Center.|Conservez la valeur par défaut.|
    |Chemin d’accès des données de la base de données|Il s’agit de l’emplacement dans lequel les fichiers de la base de données MongoDB sont enregistrés. L’emplacement par défaut est le suivant : %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data.|Modifiez cette valeur pour pointer vers un emplacement capable de prendre en charge l’évolution de vos besoins en matière de redimensionnement. **Remarque :** <ul><li>Dans les environnements de production, vous devez utiliser un lecteur avec suffisamment d'espace (tel que déterminé par la planification de la capacité).</li><li>Pour les déploiements volumineux, la base de données doit figurer sur un disque physique distinct.</li></ul>Pour plus d’informations sur le redimensionnement, consultez [Planification de la capacité ATA](/advanced-threat-analytics/PlanDesign/ata-capacity-planning).|
    |Chemin d’accès du journal de base de données|Il s’agit de l’emplacement dans lequel les fichiers journaux de la base de données sont enregistrés. L’emplacement par défaut est le suivant : %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data\journal.|Pour les déploiements volumineux, le journal de base de données doit se trouver sur un disque physique distinct de la base de données et du lecteur système. Modifiez cette valeur pour pointer vers un emplacement avec suffisamment de place pour prendre en charge votre journal de base de données.|
    |Adresse IP du service du centre ATA : port|Il s’agit de l’adresse IP sur laquelle le service du centre ATA écoute les communications en provenance des passerelles ATA.<br /><br />**Port par défaut :** 443|Cliquez sur la flèche vers le bas pour sélectionner l’adresse IP à utiliser par le service du centre ATA.<br /><br />L’adresse IP et le port du service du centre ATA ne peuvent pas être identiques à ceux de la console ATA. Veillez à modifier le port de la console ATA.|
    |Certificat SSL du service du centre ATA|Il s’agit du certificat utilisé par le service du centre ATA.|Cliquez sur l’icône en forme de clé pour sélectionner un certificat installé ou cochez la case Créer un certificat auto-signé lors du déploiement dans un environnement lab.|
    |Adresse IP de la console ATA|Il s’agit de l’adresse IP utilisée par IIS pour la console ATA.|Cliquez sur la flèche vers le bas pour sélectionner l’adresse IP utilisée par la console ATA. **Remarque :** notez cette adresse IP pour faciliter l’accès à la console ATA à partir de la passerelle ATA.|
    |Certificat SSL de la console ATA|Il s’agit du certificat à utiliser par IIS.|Cliquez sur l’icône en forme de clé pour sélectionner un certificat installé ou cochez la case Créer un certificat auto-signé lors du déploiement dans un environnement lab.|
    ![Image de la configuration du centre ATA](media/ATA-Center-Configuration.JPG)

7.  Cliquez sur **Installer** pour installer ATA et ses composants, et créer la connexion entre le centre ATA et la console ATA.

8.  Une fois l’installation terminée, cliquez sur **Lancer** pour vous connecter à la console ATA.

    Les composants suivants sont installés et configurés pendant l’installation du centre ATA :

    -   Internet Information Services (IIS)

    -   MongoDB

    -   Service du centre ATA et site IIS de la console ATA

    -   Jeu d’éléments de collecte de données de l’Analyseur de performances personnalisé

    -   Certificats auto-signés (s’ils ont été sélectionnés pendant l’installation)

> [!NOTE]
> Pour faciliter la résolution des problèmes et l’amélioration du produit, nous vous recommandons d’installer MongoVue et tout autre complément MongoDB (ou tout autre outil tiers de votre choix). MongoVue nécessite l’installation du .NET Framework 3.5.

### Valider l’installation

1.  Vérifiez que le service Microsoft Advanced Threat Analytics Center est en cours d’exécution.

2.  Sur le Bureau, cliquez sur le raccourci Microsoft Advanced Threat Analytics pour vous connecter à la console ATA. Connectez-vous avec les mêmes informations d’identification utilisateur que celles que vous avez utilisées pour installer le centre ATA. Quand vous vous connectez à la console ATA pour la première fois, la page **Paramètres de connectivité du domaine** s’affiche automatiquement pour vous permettre de poursuivre la configuration et le déploiement des passerelles ATA.

3.  Passez en revue le fichier d’erreurs dans le fichier **Microsoft.Tri.Center-Errors.log** qui se trouve par défaut à l’emplacement suivant : %programfiles%\Microsoft Advanced Threat Analytics\Center\Logs.

>[!div class="step-by-step"]
[« Pré-installation](install-ata-preinstall.md)
[Étape 2 »](install-ata-step2.md)

## Voir aussi

- [Pour obtenir de l’aide, consultez notre forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurer la collecte d’événements](/advanced-threat-analytics/plandesign/configure-event-collection)
- [Conditions préalables au déploiement d’ATA](/advanced-threat-analytics/plandesign/ata-prerequisites)


<!--HONumber=Apr16_HO2-->


