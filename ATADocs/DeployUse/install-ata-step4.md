---
title: "Installer ATA - Étape 4 | Microsoft ATA"
description: "La quatrième étape de la procédure d’installation d’ATA vous aide à installer la passerelle ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 6052a911c12f8dbb757ab8445f9e0c6ec09b530e


---

# Installer ATA - Étape 4

>[!div class="step-by-step"]
[« Étape 3](install-ata-step3.md)
[Étape 5 »](install-ata-step5.md)

## Étape 4. Installer la passerelle ATA

Avant d’installer la passerelle ATA sur un serveur dédié, vérifiez que la mise en miroir des ports est correctement configurée et que la passerelle ATA peut voir le trafic à destination et en provenance des contrôleurs de domaine. Pour plus d’informations, consultez [Valider la mise en miroir des ports](validate-port-mirroring.md).


> [!IMPORTANT]
> Vérifiez que le correctif [KB2919355](http://support.microsoft.com/kb/2919355/) a été installé.  Exécutez l’applet de commande PowerShell suivante pour vérifier si le correctif est installé :
>
> `Get-HotFix -Id kb2919355`

Effectuez les opérations suivantes sur le serveur de la passerelle ATA.

1.  Extrayez les fichiers à partir du fichier zip. 
> [!NOTE] 
> L’installation directe à partir du fichier zip est vouée à l’échec.

2.  À partir d’une invite de commandes avec élévation de privilèges, exécutez **Microsoft ATA Gateway Setup.exe**, puis suivez les instructions de l’Assistant Installation.

3.  Dans la page **Bienvenue**, sélectionnez votre langue, puis cliquez sur **Suivant**.

4.  Sous **Configuration de la passerelle ATA**, entrez les informations suivantes en fonction de votre environnement :

    ![Image de la configuration de la passerelle ATA](media/ATA-Gateway-Configuration.JPG)

    |Champ|Description|Commentaires|
    |---------|---------------|------------|
    |Chemin d’installation|Il s’agit de l’emplacement où est installée la passerelle ATA. L’emplacement par défaut est le suivant : %programfiles%\Microsoft Advanced Threat Analytics\Gateway.|Conservez la valeur par défaut.|
    |Certificat SSL du service de la passerelle ATA|Il s’agit du certificat utilisé par la passerelle ATA.|Utilisez un certificat auto-signé pour les environnements lab uniquement.|
    |Enregistrement de la passerelle ATA|Entrez le nom d’utilisateur et le mot de passe de l’administrateur ATA.|Pour enregistrer la passerelle ATA auprès du centre ATA, entrez le nom d’utilisateur et le mot de passe de l’utilisateur qui a installé le centre ATA. Cet utilisateur doit être membre de l’un des groupes locaux suivants sur le centre ATA.<br /><br />- Administrateurs<br />- Administrateurs Microsoft Advanced Threat Analytics **Remarque :** ces informations d’identification sont utilisées uniquement à des fins d’enregistrement et ne sont pas stockées dans ATA.|
    Les composants suivants sont installés et configurés pendant l’installation de la passerelle ATA :

    -   KB3047154

        > [!IMPORTANT]
        > -   N’installez pas le correctif KB 3047154 sur un hôte de virtualisation (l’hôte responsable de la virtualisation, que vous pouvez exécuter sur une machine virtuelle), car cela pourrait nuire au bon fonctionnement de la mise en miroir des ports. 
        > -   N’installez pas l’Analyseur de message, Wireshark ou tout autre logiciel de capture réseau sur la passerelle ATA. Si vous souhaitez capturer le trafic réseau, installez et utilisez le Moniteur réseau Microsoft version 3.4.

    -   Service de passerelle ATA

    -   Microsoft Visual C++ 2013 Redistributable

    -   Jeu d’éléments de collecte de données de l’Analyseur de performances personnalisé

5.  Une fois l’installation terminée : pour la passerelle ATA, cliquez sur **Lancer** pour ouvrir votre navigateur et vous connecter à la console ATA ; pour la passerelle légère ATA, cliquez sur **Terminer**.


>[!div class="step-by-step"]
[« Étape 3](install-ata-step3.md)
[Étape 5 »](install-ata-step5.md)

## Voir aussi

- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurer la collecte d’événements](configure-event-collection.md)
- [Conditions préalables au déploiement d’ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jul16_HO4-->


