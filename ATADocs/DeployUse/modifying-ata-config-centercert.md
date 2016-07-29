---
title: Modifier la configuration ATA - Certificat du centre ATA | Microsoft ATA
description: "Décrit le processus en deux étapes pour renouveler ou remplacer le certificat dans le magasin de l’ordinateur local sur le serveur du centre ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: c8855287-de3b-4cdd-be8f-2128f48a6f27
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 5ae9f13c417459e73d85cce3ebbb0293c3e08f83


---

# Modifier la configuration ATA - Certificat du centre ATA

>[!div class="step-by-step"]
[« Adresse IP du serveur du centre ATA](modifying-ata-config-centerip.md)
[Adresse IP de la console ATA »](modifying-ata-config-consoleip.md)

## Modifier le certificat du centre ATA
Si vos certificats expirent et doivent être renouvelés ou remplacés après avoir installé le nouveau certificat dans le magasin de l’ordinateur local sur le serveur du centre ATA, remplacez le certificat en suivant ce processus en deux étapes :

-   Première étape. Mettez à jour le certificat que le service du centre ATA doit utiliser. À ce stade, le service du centre ATA est toujours lié au certificat d’origine. Quand les passerelles ATA synchronisent leur configuration, elles disposent de deux certificats potentiels qui sont valides pour une authentification mutuelle. Tant que la passerelle ATA peut se connecter avec le certificat d’origine, elle n’essaie pas le nouveau.

-   Deuxième étape. Une fois que toutes les passerelles ATA sont synchronisées avec la configuration mise à jour, vous pouvez activer le nouveau certificat auquel est lié le service du centre ATA. Quand vous activez le nouveau certificat, le service du centre ATA est lié à ce certificat. Les passerelles ATA ne sont pas en mesure de procéder à une authentification mutuelle correcte avec le service du centre ATA et tentent d’authentifier le deuxième certificat. Après la connexion au service du centre ATA, la passerelle ATA télécharge la configuration la plus récente et dispose d’un seul certificat pour le centre ATA, sauf si vous avez relancé le processus.

> [!NOTE]
> -   Si une passerelle ATA était hors connexion lors de la première étape et n’a jamais reçu la configuration mise à jour, vous devez manuellement mettre à jour le fichier JSON de configuration sur la passerelle ATA.
> -   Le certificat que vous utilisez doit être approuvé par les passerelles ATA.
> -   Si vous devez déployer une nouvelle passerelle ATA après avoir activé le nouveau certificat, vous devez télécharger une nouvelle fois le package d’installation de la passerelle ATA.

1.  Ouvrez la console ATA.

2.  Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône des paramètres de configuration ATA](media/ATA-config-icon.JPG)

3.  Sélectionnez **Centre ATA**.

4.  Sous **Certificat**, sélectionnez l’un des certificats dans la liste.

5.  Cliquez sur **Enregistrer**.

6.  Vous voyez une notification du nombre de passerelles ATA synchronisées avec la configuration la plus récente.

7.  Une fois que toutes les passerelles ATA sont synchronisées, cliquez sur **Activer** pour activer le nouveau certificat.
    >[!IMPORTANT]
    >Avant d’activer la nouvelle configuration, vérifiez que toutes les passerelles ATA sont synchronisées avec la configuration la plus récente. L’activation de la nouvelle configuration avant que toutes les passerelles ATA ne soient synchronisées peut engendrer un dysfonctionnement de la passerelle ATA. Si une des passerelles ATA n’est pas synchronisée, vous obtenez cette erreur quand vous cliquez sur Activer :
    >
    >    ![Erreur de synchronisation de la passerelle ATA](media/ataGW-not-synced.png)

8.  Vérifiez que toutes les passerelles ATA sont en mesure de synchroniser leur configuration après l’activation de la modification.

>[!div class="step-by-step"]
[« Adresse IP du serveur du centre ATA](modifying-ata-config-centerip.md)
[Adresse IP de la console ATA »](modifying-ata-config-consoleip.md)

## Voir aussi
- [Utilisation de la console ATA](working-with-ata-console.md)
- [Installer ATA](install-ata.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->


