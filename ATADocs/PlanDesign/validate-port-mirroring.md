---
# required metadata

title: Validation de la mise en miroir des ports | Microsoft Advanced Threat Analytics
description: Explique comment vérifier que la mise en miroir des ports est configurée correctement
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: ebd41719-c91a-4fdd-bcab-2affa2a2cace

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Valider la mise en miroir des ports
Les étapes suivantes sont conçues pour vous guider dans le processus de validation de la mise en miroir des ports. Pour qu’ATA fonctionne correctement, la passerelle ATA doit pouvoir voir le trafic entrant et sortant du contrôleur de domaine. La principale source de données utilisée par ATA est l’inspection approfondie des paquets du trafic réseau entrant et sortant de vos contrôleurs de domaine. Pour qu’ATA puisse voir le trafic réseau, vous devez configurer la mise en miroir des ports. La mise en miroir des ports copie le trafic d’un port (le port source) vers un autre port (le port de destination).

1.  Installez [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865) ou un autre outil de détection de réseau.

    > [!IMPORTANT]
    > N’installez pas l’analyseur de message Microsoft ou tout autre logiciel de capture du trafic sur la passerelle ATA.

2.  Ouvrez le Moniteur réseau et créez un nouvel onglet de capture.

    1.  Sélectionnez uniquement la carte réseau **Capture** ou celle qui est connectée au port de commutateur qui est configuré comme le port de destination de la mise en miroir.

    2.  Assurez-vous que le mode P est activé.

    3.  Cliquez sur **Nouvelle capture**.

        ![Image de la création d’un nouvel onglet de capture](media/ATA-Port-Mirroring-Capture.jpg)

3.  Dans la fenêtre Filtre d’affichage, entrez le filtre **KerberosV5 OR LDAP**, puis cliquez sur **Appliquer**.

    ![Image de l’application du filtre KerberosV5 or LDAP](media/ATA-Port-Mirroring-filter-settings.jpg)

4.  Pour démarrer la session de capture, cliquez sur **Démarrer**. Si vous ne voyez pas le trafic entrant et sortant du contrôleur de domaine, examinez la configuration de mise en miroir des ports.

    > [!NOTE]
    > Il est important de vous assurer que vous voyez le trafic entrant et sortant des contrôleurs de domaine.
    >
    > ![Image du démarrage de la session de capture](media/ATA-Port-Mirroring-Capture-traffic.jpg)

5.  Si vous voyez uniquement le trafic dans un sens, vous devez résoudre ce problème de configuration de la mise en miroir des ports avec l’aide de l’équipe chargée du réseau ou de la virtualisation.

## Voir aussi

- [Configurer la mise en miroir des ports](configure-port-mirroring.md)
- [Pour obtenir de l’aide, consultez notre forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


