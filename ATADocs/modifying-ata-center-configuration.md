---
title: Modifier la configuration du centre ATA (Advanced Threat Analytics) | Microsoft Docs
description: "Décrit comment changer l’adresse IP, le port, l’URL de la console ou le certificat de votre centre ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1e9fa2d104c52087746e7c03fea27e3cb596adf0
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
*S’applique à : Advanced Threat Analytics version 1.8*



# <a name="modifying-the-ata-center-configuration"></a>Modification de la configuration du centre ATA


Après le déploiement initial, les modifications doivent être apportées avec soin au centre ATA. Utilisez les procédures suivantes lors de la mise à jour de l’adresse IP et du port, de l’URL de la console et du certificat.

## <a name="the-ata-center-ip-address"></a>Adresse IP du centre ATA

Les passerelles ATA stockent localement l’adresse IP du centre ATA auquel elles doivent se connecter. Elles se connectent régulièrement au centre ATA et téléchargent les modifications de configuration. La modification du mode de connexion des passerelles ATA au centre ATA est effectuée en deux étapes.

-   Première étape. Mettez à jour l’adresse IP et le port que le service du centre ATA doit utiliser. À ce stade, le centre ATA écoute toujours sur l’adresse IP d’origine et, la prochaine fois que la passerelle ATA synchronise sa configuration, elle aura deux adresses IP pour le centre ATA. Tant que la passerelle ATA peut se connecter avec l’adresse IP d’origine (la première), elle n’essaie pas la nouvelle adresse IP ni le port.

-   Deuxième étape. Une fois que toutes les passerelles ATA sont synchronisées avec la configuration mise à jour, activez la nouvelle adresse IP et le port sur lequel écoute le centre ATA. Quand vous activez la nouvelle adresse IP, le service du centre ATA est lié à cette adresse. Les passerelles ATA ne sont pas en mesure de se connecter à l’adresse d’origine et tentent maintenant de se connecter avec la deuxième adresse IP (la nouvelle) dont elles disposent pour le centre ATA. Après la connexion au centre ATA avec la nouvelle adresse IP, la passerelle ATA télécharge la configuration la plus récente et dispose d’une seule adresse IP pour le centre ATA, sauf si vous avez relancé le processus.

> [!NOTE]
> -   Si une passerelle ATA était hors connexion lors de la première étape et n’a jamais reçu la configuration mise à jour, vous devez manuellement mettre à jour le fichier JSON de configuration sur la passerelle ATA.
> -   Si la nouvelle adresse IP est installée sur le serveur du centre ATA, vous pouvez la sélectionner dans la liste des adresses IP lors de la modification. Toutefois si, pour une raison quelconque, vous ne pouvez pas installer l’adresse IP sur le serveur du centre ATA, vous pouvez sélectionner une adresse IP personnalisée et l’ajouter manuellement. Vous ne serez pas en mesure d’activer la nouvelle adresse IP tant que l’adresse IP n’est pas installée sur le serveur.
> -   Si vous devez déployer une nouvelle passerelle ATA après avoir activé la nouvelle adresse IP, vous devez télécharger une nouvelle fois le package d’installation de la passerelle ATA.

## <a name="the-console-url"></a>URL de la console

L’URL est utilisée dans les scénarios suivants :

-   Installation de passerelles ATA : quand une passerelle ATA est installée, elle s’inscrit auprès du centre ATA. Ce processus d’inscription est effectué par la connexion à la console ATA. Si vous entrez un nom de domaine complet pour l’URL de la console ATA, vous devez vérifier que la passerelle ATA peut résoudre le nom de domaine complet en adresse IP à laquelle la console ATA est liée.

-   Alertes : quand ATA envoie une alerte par courrier électronique ou SIEM, il inclut un lien vers l’activité suspecte. La partie hôte du lien est le paramètre URL de la console ATA.

-   Si vous avez installé un certificat de votre autorité de certification interne, vous souhaiterez probablement faire correspondre l’URL au nom d’objet du certificat pour que les utilisateurs ne reçoivent pas de message d’avertissement lors de la connexion à la console ATA.

-   L’utilisation d’un nom de domaine complet pour l’URL de la console ATA vous permet de modifier l’adresse IP utilisée par la console ATA sans annuler les alertes qui ont été envoyées précédemment ni avoir à retélécharger le package de la passerelle ATA. Vous devez uniquement mettre à jour le DNS avec la nouvelle adresse IP.

> [!NOTE]
> Après avoir modifié l’URL de la console ATA, vous devez télécharger le package d’installation de la passerelle ATA avant d’installer de nouvelles passerelles ATA.

## <a name="the-ata-center-certificate"></a>Certificat du centre ATA
Si votre certificat est sur le point d’expirer et doit être renouvelé ou remplacé après l’installation du nouveau certificat dans le magasin de l’ordinateur local sur le serveur du centre ATA, remplacez le certificat en suivant ce processus en deux étapes :

-   Première étape. Mettez à jour le certificat que le service du centre ATA doit utiliser. À ce stade, le service du centre ATA est toujours lié au certificat d’origine. Quand les passerelles ATA synchronisent leur configuration, elles disposent de deux certificats potentiels qui sont valides pour une authentification mutuelle. Tant que la passerelle ATA peut se connecter avec le certificat d’origine, elle n’essaie pas le nouveau.

-   Deuxième étape. Une fois que toutes les passerelles ATA sont synchronisées avec la configuration mise à jour, vous pouvez activer le nouveau certificat auquel est lié le service du centre ATA. Quand vous activez le nouveau certificat, le service du centre ATA est lié à ce certificat. Les passerelles ATA ne sont pas en mesure de procéder à une authentification mutuelle correcte avec le service du centre ATA et tentent d’authentifier le deuxième certificat. Après la connexion au service du centre ATA, la passerelle ATA télécharge la configuration la plus récente et dispose d’un seul certificat pour le centre ATA, sauf si vous avez relancé le processus.

> [!NOTE]
> -   Si une passerelle ATA était hors connexion lors de la première étape et n’a jamais reçu la configuration mise à jour, vous devez manuellement mettre à jour le fichier JSON de configuration sur la passerelle ATA.
> -   Le certificat que vous utilisez doit être approuvé par les passerelles ATA.
> -   Le certificat étant également utilisé pour la console ATA, il doit correspondre à l’adresse de la console ATA pour éviter les avertissements dans le navigateur.
> -   Si vous devez déployer une nouvelle passerelle ATA après avoir activé le nouveau certificat, vous devez télécharger une nouvelle fois le package d’installation de la passerelle ATA.

## <a name="changing-the-ata-center-configuration"></a>Modification de la configuration du centre ATA

1.  Ouvrez la console ATA.

2.  Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône des paramètres de configuration ATA](media/ATA-config-icon.png)

3.  Sélectionnez **Centre**.

  ![Modifier la configuration ATA](media/change-center-config.png)

4.  Sous **URL**, sélectionnez **Ajouter une adresse IP ou un nom DNS personnalisé**, et spécifiez le nouveau DNS ou la nouvelle adresse IP, ou bien, sous **Certificat**, sélectionnez le nouveau certificat.

5.  Cliquez sur **Enregistrer**.

6.  Vous voyez une notification du nombre de passerelles ATA synchronisées avec la configuration la plus récente.

    >[!IMPORTANT]
    >Avant d’activer la nouvelle configuration, vérifiez que toutes les passerelles ATA sont synchronisées avec la configuration la plus récente. L’activation de la nouvelle configuration avant que toutes les passerelles ATA ne soient synchronisées peut engendrer un dysfonctionnement de la passerelle ATA. Si une des passerelles ATA n’est pas synchronisée, vous obtenez cette erreur quand vous cliquez sur Activer :


7.  Une fois que toutes les passerelles ATA sont synchronisées, cliquez sur **Activer** pour activer la nouvelle adresse IP ou le nouveau certificat.

    > [!NOTE]
    > Si vous avez entré une adresse IP personnalisée, vous ne serez pas en mesure de cliquer sur **Activer** tant que vous n’avez pas installé l’adresse IP sur le centre ATA.

8.  Vérifiez que toutes les passerelles ATA sont en mesure de synchroniser leur configuration après l’activation de la modification. La barre de notification indique le nombre de passerelles ATA qui ont correctement synchronisé leur configuration.




## <a name="see-also"></a>Voir aussi
- [Utilisation de la console ATA](working-with-ata-console.md)
- [Consultez le forum ATA !](https://aka.ms/ata-forum)
