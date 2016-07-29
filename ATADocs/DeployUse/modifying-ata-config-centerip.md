---
title: "Modifier la configuration ATA - Adresse IP du centre ATA | Microsoft ATA"
description: "Décrit comment modifier l’adresse IP, le port ou le certificat de votre centre ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 4eb552b9f7d42895abf08ec4cd9216b5204c5e0b


---

# Modifier la configuration ATA - Adresse IP du centre ATA

>[!div class="step-by-step"]
[Certificat du centre ATA »](modifying-ata-config-centercert.md)

Après le déploiement initial, les modifications doivent être apportées avec soin au centre ATA. Utilisez les procédures suivantes lors de la mise à jour de l’adresse IP et du port ou du certificat.

## Modifier l’adresse IP utilisée par le serveur du centre ATA
Si vous devez modifier l’adresse IP et le port ou le certificat du centre ATA, tenez compte des éléments suivants.

Les passerelles ATA stockent localement l’adresse IP du centre ATA auquel elles doivent se connecter. Elles se connectent régulièrement au centre ATA et téléchargent les modifications de configuration. La modification du mode de connexion des passerelles ATA au centre ATA est effectuée en deux étapes.

-   Première étape. Mettez à jour l’adresse IP et le port que le service du centre ATA doit utiliser. À ce stade, le centre ATA écoute toujours sur l’adresse IP d’origine et, la prochaine fois que la passerelle ATA synchronise sa configuration, elle aura deux adresses IP pour le centre ATA. Tant que la passerelle ATA peut se connecter avec l’adresse IP d’origine (la première), elle n’essaie pas la nouvelle adresse IP ni le port.

-   Deuxième étape. Une fois que toutes les passerelles ATA sont synchronisées avec la configuration mise à jour, activez la nouvelle adresse IP et le port sur lequel écoute le centre ATA. Quand vous activez la nouvelle adresse IP, le service du centre ATA est lié à cette adresse. Les passerelles ATA ne sont pas en mesure de se connecter à l’adresse d’origine et tentent maintenant de se connecter avec la deuxième adresse IP (la nouvelle) dont elles disposent pour le centre ATA. Après la connexion au centre ATA avec la nouvelle adresse IP, la passerelle ATA télécharge la configuration la plus récente et dispose d’une seule adresse IP pour le centre ATA, sauf si vous avez relancé le processus.

> [!NOTE]
> -   Si une passerelle ATA était hors connexion lors de la première étape et n’a jamais reçu la configuration mise à jour, vous devez manuellement mettre à jour le fichier JSON de configuration sur la passerelle ATA.
> -   Si la nouvelle adresse IP est installée sur le serveur du centre ATA, vous pouvez la sélectionner dans la liste des adresses IP lors de la modification. Toutefois si, pour une raison quelconque, vous ne pouvez pas installer l’adresse IP sur le serveur du centre ATA, vous pouvez sélectionner une adresse IP personnalisée et l’ajouter manuellement. Vous ne serez pas en mesure d’activer la nouvelle adresse IP tant que l’adresse IP n’est pas installée sur le serveur.
> -   Si vous devez déployer une nouvelle passerelle ATA après avoir activé la nouvelle adresse IP, vous devez télécharger une nouvelle fois le package d’installation de la passerelle ATA.

1.  Ouvrez la console ATA.

2.  Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône des paramètres de configuration ATA](media/ATA-config-icon.JPG)

3.  Sélectionnez **Général**.

4.  Sous **Adresse IP du service du centre ATA : port**, sélectionnez l’une des adresses IP existantes ou **Ajouter une adresse IP personnalisée** et entrez une adresse IP.

5.  Cliquez sur **Enregistrer**.

6.  Vous voyez une notification du nombre de passerelles ATA synchronisées avec la configuration la plus récente.

    ![Image de passerelles synchronisées du centre ATA](media/ATA-chge-IP-after-clicking-save.png)

    >[!IMPORTANT]
    >Avant d’activer la nouvelle configuration, vérifiez que toutes les passerelles ATA sont synchronisées avec la configuration la plus récente. L’activation de la nouvelle configuration avant que toutes les passerelles ATA ne soient synchronisées peut engendrer un dysfonctionnement de la passerelle ATA. Si une des passerelles ATA n’est pas synchronisée, vous obtenez cette erreur quand vous cliquez sur Activer :
    >
    >    ![Erreur de synchronisation de la passerelle ATA](media/ataGW-not-synced.png)


7.  Une fois que toutes les passerelles ATA sont synchronisées, cliquez sur **Activer** pour activer la nouvelle adresse IP.

    > [!NOTE]
    > Si vous avez entré une adresse IP personnalisée, vous ne serez pas en mesure de cliquer sur **Activer** tant que vous n’avez pas installé l’adresse IP sur le centre ATA.

8.  Vérifiez que toutes les passerelles ATA sont en mesure de synchroniser leur configuration après l’activation de la modification. La barre de notification indique le nombre de passerelles ATA qui ont correctement synchronisé leur configuration.

>[!div class="step-by-step"]
[Modifier le certificat du centre ATA »](modifying-ata-config-centercert.md)


## Voir aussi
- [Utilisation de la console ATA](working-with-ata-console.md)
- [Installer ATA](install-ata.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->


