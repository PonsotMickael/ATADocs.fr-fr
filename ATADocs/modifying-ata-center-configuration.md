---
title: Modifier la configuration du centre ATA (Advanced Threat Analytics) | Microsoft Docs
description: "Décrit comment changer l’adresse IP, le port, l’URL de la console ou le certificat de votre centre ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 8/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e9fa0b9162aabdaa9a42c532cf69af37decf3e05
ms.sourcegitcommit: 7bc04eb4d004608764b3ded1febf32bc4ed020be
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/02/2017
---
*S’applique à : Advanced Threat Analytics version 1.8*



# <a name="modifying-the-ata-center-configuration"></a>Modification de la configuration du centre ATA


Après le déploiement initial, les modifications doivent être apportées avec soin au centre ATA. Utilisez les procédures suivantes lors de la mise à jour de l’URL de la console et du certificat.

## <a name="the-ata-console-url"></a>URL de la console ATA

L’URL est utilisée dans les scénarios suivants :

-   Il s’agit de l’URL utilisée par les passerelles ATA pour communiquer avec le centre ATA.

- Installation de passerelles ATA : quand une passerelle ATA est installée, elle s’inscrit auprès du centre ATA. Ce processus d’inscription est effectué par la connexion à la console ATA. Si vous entrez un nom de domaine complet pour l’URL de la console ATA, vérifiez que la passerelle ATA peut résoudre le nom de domaine complet en adresse IP à laquelle la console ATA est liée.

-   Alertes : quand ATA envoie une alerte par courrier électronique ou SIEM, il inclut un lien vers l’activité suspecte. La partie hôte du lien est le paramètre URL de la console ATA.

-   Si vous avez installé un certificat à partir de votre autorité de certification interne, faites correspondre l’URL au nom du sujet du certificat. Ainsi, les utilisateurs ne reçoivent pas un message d’avertissement lors de la connexion à la console ATA.

-   L’utilisation d’un nom de domaine complet pour l’URL de la console ATA vous permet de modifier l’adresse IP utilisée par la console ATA sans annuler les alertes précédentes ni retélécharger le package de la passerelle ATA. Vous devez uniquement mettre à jour le DNS avec la nouvelle adresse IP.

1. Assurez-vous que la nouvelle URL que vous souhaitez utiliser correspond à l’adresse IP de la console ATA.

2. Dans les paramètres ATA, sous **Centre**, entrez la nouvelle URL. À ce stade, le service du centre ATA utilise toujours l’URL d’origine. 

 ![Modifier la configuration ATA](media/change-center-config.png)

  > [!NOTE]
  > Si vous avez entré une adresse IP personnalisée, vous ne pouvez pas cliquer sur **Activer** tant que vous n’avez pas installé l’adresse IP sur le centre ATA.
    
3. Attendez que les passerelles ATA se synchronisent. Elles disposent désormais de deux URL potentielles permettant d’accéder à la console ATA. Tant que la passerelle ATA peut se connecter avec l’URL d’origine, elle n’essaie pas la nouvelle.

4. Une fois toutes les passerelles ATA synchronisées avec la configuration mise à jour, activez la nouvelle URL. Lorsque vous activez la nouvelle URL, les passerelles ATA utilisent la nouvelle URL pour accéder au centre ATA. Après la connexion au service du centre ATA, la passerelle ATA télécharge la configuration la plus récente et dispose uniquement de la nouvelle URL pour la console ATA. 

> [!NOTE]
> -   Si une passerelle ATA était hors connexion lorsque vous avez activé la nouvelle URL et n’a jamais reçu la configuration mise à jour, vous devez manuellement mettre à jour le fichier JSON de configuration sur la passerelle ATA.
> -   Si vous devez déployer une nouvelle passerelle ATA après avoir activé la nouvelle URL, vous devez télécharger une nouvelle fois le package d’installation de la passerelle ATA.


## <a name="the-ata-center-certificate"></a>Certificat du centre ATA

> [!WARNING]
> - Le processus de renouvellement d’un certificat existant n’est pas pris en charge. La seule façon de renouveler un certificat consiste à créer un certificat et à configurer ATA pour qu’il utilise le nouveau certificat.


Procédez comme suit pour remplacer le certificat :

1. Avant l’expiration du certificat actuel, créez un certificat et vérifiez qu’il est installé sur le serveur du centre ATA. 

2. Dans les paramètres ATA, sous **Centre**, sélectionnez ce certificat nouvellement créé. À ce stade, le service du centre ATA est toujours lié au certificat d’origine. 

 ![Modifier la configuration ATA](media/change-center-config.png)

3. Attendez que les passerelles ATA se synchronisent. Elles disposent désormais de deux certificats potentiels valides pour l’authentification mutuelle. Tant que la passerelle ATA peut se connecter avec le certificat d’origine, elle n’essaie pas le nouveau.

4. Une fois que toutes les passerelles ATA sont synchronisées avec la configuration mise à jour, activez le nouveau certificat auquel est lié le service du centre ATA. Quand vous activez le nouveau certificat, le service du centre ATA est lié à ce certificat. Les passerelles ATA utilisent désormais le nouveau certificat pour s’authentifier auprès du centre ATA. Après la connexion au service du centre ATA, la passerelle ATA télécharge la configuration la plus récente et dispose uniquement du nouveau certificat pour le centre ATA. 

> [!NOTE]
> -   Si une passerelle ATA était hors connexion lorsque vous avez activé le nouveau certificat et n’a jamais reçu la configuration mise à jour, vous devez manuellement mettre à jour le fichier JSON de configuration sur la passerelle ATA.
> -   Le certificat que vous utilisez doit être approuvé par les passerelles ATA.
> -   Le certificat étant également utilisé pour la console ATA, il doit correspondre à l’adresse de la console ATA pour éviter les avertissements dans le navigateur.
> -   Si vous devez déployer une nouvelle passerelle ATA après avoir activé le nouveau certificat, vous devez télécharger une nouvelle fois le package d’installation de la passerelle ATA.



 
## <a name="see-also"></a>Voir aussi
- [Utilisation de la console ATA](working-with-ata-console.md)
- [Consultez le forum ATA !](https://aka.ms/ata-forum)
