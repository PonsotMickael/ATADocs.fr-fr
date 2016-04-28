---
# required metadata

title: Modifier la configuration ATA - Nom de la carte réseau de capture | Microsoft Advanced Threat Analytics
description: Décrit comment modifier le nom de la carte réseau qui est configurée comme une carte réseau de capture sans mettre fin à la connectivité de la passerelle ATA
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 3225a81e-0395-43ca-9a48-0cbe7171e5de

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Modifier la configuration ATA - Nom de la carte réseau de capture

>[!div class="step-by-step"]
[« Mot de passe de connectivité de domaine](modifying-ata-config-dcpassword.md)

## Modifier le nom de la carte réseau de capture de la passerelle ATA
Si vous modifiez le nom de la carte réseau qui est actuellement configurée en tant que carte réseau de capture, le serveur de la passerelle ATA ne démarre pas. Pour modifier correctement le nom sans mettre fin à la connectivité de la passerelle ATA, procédez comme suit :

1.  Dans la page Configuration de la passerelle ATA, désélectionnez la carte réseau à renommer et sélectionnez une autre carte réseau en tant que carte réseau de capture à la place. Il peut s’agir d’une carte réseau temporaire ou même de la carte réseau de gestion. Pendant ce temps, ATA ne capture pas le trafic du port en miroir du contrôleur de domaine. Enregistrez la nouvelle configuration.

2.  Sur la passerelle ATA, renommez la carte réseau, en ouvrant le Panneau de configuration et en sélectionnant Connexions réseau.

3.  Revenez ensuite à la page Configuration de la passerelle ATA de la console ATA Il est possible que vous deviez actualiser la page pour afficher la carte réseau avec le nouveau nom dans la liste. Désélectionnez la carte que vous avez sélectionnée à l’étape 1, puis sélectionnez la carte nouvellement nommée. Enfin, enregistrez la nouvelle configuration.

Si vous avez renommé votre carte réseau sans suivre ce processus, votre passerelle ATA ne démarre pas et vous obtenez cette erreur dans le fichier journal Microsoft.Tri.Gateway-Errors.log sur la passerelle ATA. Dans l’exemple ci-dessous, **Capture** est le nom d’origine de la carte réseau que vous définissez :

`Error [NetworkListener] Microsoft.Tri.Infrastructure.ExtendedException: Unavailable network adapters [UnavailableCaptureNetworkAdapterNames=Capture]`

Pour résoudre ce problème, réaffectez à la carte réseau le nom défini à d’origine lors de la configuration d’ATA et suivez le processus décrit ci-dessus pour modifier le nom.

>[!div class="step-by-step"]
[« Mot de passe de connectivité de domaine](modifying-ata-config-dcpassword.md)


## Voir aussi
- [Utilisation de la console ATA](/advanced-threat-analytics/understand/working-with-ata-console)
- [Installer ATA](install-ata.md)
- [Pour obtenir de l’aide, consultez notre forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


