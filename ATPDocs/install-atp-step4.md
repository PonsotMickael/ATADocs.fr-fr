---
title: "Installer Azure - Protection avancée contre les menaces – Étape 4 | Microsoft Docs"
description: "La quatrième étape de la procédure d’installation d’Azure ATP vous permet d’installer le capteur autonome Azure ATP."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 51911e39-76c7-4dcd-bc0b-ec6235d0403f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7b003882f21f22b3427fb95534ca2bde255b14e6
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2018
---
*S’applique à : Azure - Protection avancée contre les menaces*



# <a name="install-azure-atp---step-4"></a>Installer Azure ATP – Étape 4

>[!div class="step-by-step"]
[« Étape 3](install-atp-step3.md)
[Étape 5 »](install-atp-step5.md)

## <a name="step-4-install-the-azure-atp-sensor"></a>Étape 4. Installer le capteur Azure ATP

Avant d’installer le capteur autonome Azure ATP sur un serveur dédié, confirmez que la mise en miroir des ports est correctement configurée et que le capteur autonome Azure ATP peut voir le trafic à destination et en provenance des contrôleurs de domaine. 


> [!IMPORTANT]
>Vérifiez que .NET Framework 4.7 est installé sur l'ordinateur. Si .NET Framework 4.7 n’est pas installé, le package d’installation de capteur Azure ATP l’installe, ce qui nécessite un redémarrage du serveur. Vérifiez que l’ordinateur dispose d’une connectivité au point de terminaison du service cloud Azure ATP : https://triprd1wceuw1sensorapi.atp.azure.com (pour l’Europe) ou https://triprd1wcuse1sensorapi.atp.azure.com (pour les États-Unis).

Effectuez les étapes suivantes sur le contrôleur de domaine ou le serveur du capteur Azure ATP.

1.  Extrayez les fichiers à partir du fichier zip. 
> [!NOTE] 
> L’installation directe à partir du fichier zip est vouée à l’échec.

2.  Exécutez **Azure ATP sensor setup.exe**, puis suivez les instructions de l’Assistant Installation.

3.  Dans la page **Bienvenue**, sélectionnez votre langue, puis cliquez sur **Suivant**.

     ![Langue d’installation du capteur autonome Azure ATP](media/sensor-install-language.png)


4.  L’Assistant Installation vérifie automatiquement si le serveur est un contrôleur de domaine ou un serveur dédié. S’il s’agit d’un contrôleur de domaine, le capteur Azure ATP est installé. S’il s’agit d’un serveur dédié, le capteur autonome Azure ATP est installé. 
    
    Par exemple, pour un capteur autonome Azure ATP, l’écran suivant s’affiche pour vous informer qu’un capteur autonome Azure ATP est installé sur votre serveur dédié :
    
    ![Installation du capteur autonome Azure ATP](media/sensor-install-deployment-type.png)

    Cliquez sur **Suivant**.

    > [!NOTE] 
    > Si le contrôleur de domaine ou le serveur dédié ne dispose pas de la configuration matérielle minimale requise pour l’installation, un avertissement s’affiche. Il ne vous empêche pas de cliquer sur **Suivant** et de procéder à l’installation. Cela peut être le bon choix pour l’installation d’Azure ATP dans un petit environnement de test de laboratoire dans lequel vous n’avez pas besoin d’autant de place pour le stockage des données. Pour les environnements de production, nous vous recommandons vivement de respecter le guide de [planification de la capacité](atp-capacity-planning.md) d’Azure ATP pour vous assurer que vos contrôleurs de domaine ou serveurs dédiés répondent aux conditions requises.

4.  Sous **Configurer le capteur**, entrez le chemin d’installation et la clé d’accès que vous avez copiée à l’étape précédente, en fonction de votre environnement :

    ![Image de configuration du capteur autonome Azure ATP](media/sensor-install-config.png)

      - Chemin d’installation : il s’agit de l’emplacement où le capteur autonome Azure ATP est installé. Par défaut, il s’agit de %programfiles%\Azure Advanced Threat Protection sensor. Conservez la valeur par défaut.

      - Clé d’accès : valeur extraite du portail d’espace de travail à l’étape précédente.
    
5. Cliquez sur **Suivant**. Les composants suivants sont installés et configurés pendant l’installation du capteur Azure ATP :

    -   KB 3047154 (pour Windows Server 2012 R2 uniquement)

        > [!IMPORTANT]
        > -   N’installez pas le correctif KB 3047154 sur un hôte de virtualisation (l’hôte responsable de la virtualisation, que vous pouvez exécuter sur une machine virtuelle), car cela pourrait nuire au bon fonctionnement de la mise en miroir des ports. 
        > -   Si Wireshark est installé sur l’ordinateur du capteur ATP, après avoir exécuté Wireshark, vous devez redémarrer le capteur ATP, car il utilise les mêmes pilotes.

    -   Service de capteur Azure ATP et service de mise à jour du capteur Azure ATP
    -   Microsoft Visual C++ 2013 Redistributable

5.  Une fois l’installation terminée, cliquez sur **Lancer** pour ouvrir votre navigateur et vous connecter au portail d’espace de travail Azure ATP.


>[!div class="step-by-step"]
[« Étape 3](install-atp-step3.md)
[Étape 5 »](install-atp-step5.md)


## <a name="see-also"></a>Voir aussi

- [Outil de dimensionnement Azure ATP](http://aka.ms/aatpsizingtool)

- [Configurer la collecte d’événements](configure-event-collection.md)

- [Prérequis d’Azure ATP](atp-prerequisites.md)

- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)