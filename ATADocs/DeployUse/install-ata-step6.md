---
# required metadata

title: Installer ATA | Microsoft Advanced Threat Analytics
description: Lors de l’étape finale de l’installation d’ATA, vous configurez les sous-réseaux du bail à court terme et l’utilisateur Honeytoken.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Installer ATA - Étape 6

>[!div class="step-by-step"]
[« Étape 5](install-ata-step5.md)

## Étape 6. Configurer les sous-réseaux du bail à court terme et l’utilisateur Honeytoken
Les sous-réseaux du bail à court terme sont des sous-réseaux dans lesquels l’attribution d’adresses IP change très rapidement, en quelques secondes ou minutes, par exemple les adresses IP utilisées pour vos réseaux privés virtuels (VPN ) et les adresses IP Wi-Fi. Pour entrer la liste des sous-réseaux du bail à court terme utilisés dans votre organisation, procédez comme suit :

1.  Dans la console ATA de la machine de la passerelle ATA, cliquez sur l’icône des paramètres et sélectionnez **Configuration**.

    ![Paramètres de configuration ATA](media/ATA-config-icon.JPG)

2.  Sous **Détection**, entrez ce qui suit pour les sous-réseaux du bail à court terme. Entrez les sous-réseaux du bail à court terme sous un format de notation de barre oblique, par exemple `192.168.0.0/24`, et cliquez sur le signe plus.

3.  Pour les SID de compte Honeytoken, entrez le SID du compte d’utilisateur sans aucune activité réseau, puis cliquez sur le signe plus. Par exemple : `S-1-5-21-72081277-1610778489-2625714895-10511`.

    > [!NOTE]
    > Pour rechercher le SID d’un utilisateur, exécutez l’applet de commande Windows PowerShell suivante, `Get-ADUser UserName`.

4.  Configurer les exclusions : vous pouvez configurer des adresses IP à exclure d’activités suspectes spécifiques. Pour plus d’informations, consultez [Gestion des paramètres de la détection ATA](working-with-detection-settings.md).

5.  Cliquez sur **Enregistrer**.

![Enregistrer les modifications](media/ATA-VPN-Subnets.JPG)

Félicitations, vous avez correctement déployé Microsoft Advanced Threat Analytics !

Vérifiez la chronologie des attaques pour afficher les activités suspectes détectées et rechercher des utilisateurs ou des ordinateurs, puis afficher leurs profils.

Gardez à l’esprit qu’ATA nécessite au minimum trois semaines pour créer des profils de comportements : vous ne verrez donc aucune activité au comportement suspect pendant les trois premières semaines.


>[!div class="step-by-step"]
[« Étape 5](install-ata-step5.md)


## Voir aussi

- [Pour obtenir de l’aide, consultez notre forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurer la collecte d’événements](/advanced-threat-analytics/plandesign/configure-event-collection)
- [Configuration requise pour ATA](/advanced-threat-analytics/plandesign/ata-prerequisites)


<!--HONumber=Apr16_HO2-->


