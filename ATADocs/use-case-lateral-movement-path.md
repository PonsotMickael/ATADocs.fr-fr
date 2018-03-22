---
title: Investigation des attaques par chemins de mouvement latéral avec ATA | Microsoft Docs
description: Cet article décrit comment détecter des attaques par chemins de mouvement latéral avec Advanced Threat Analytics (ATA).
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 710f01bd-c878-4406-a7b2-ce13f98736ea
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: dc03cfe1719541dac0f8509c0f8f22987ecb96bb
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/22/2018
---
*S’applique à : Advanced Threat Analytics version 1.9*

# <a name="investigating-lateral-movement-paths-with-ata"></a>Investigation des chemins de mouvement latéral avec ATA

Même si vous faites de votre mieux pour protéger vos utilisateurs sensibles, que les administrateurs ont des mots de passe complexes qu’ils changent fréquemment, que leurs ordinateurs sont renforcés et que le stockage de leurs données est sécurisé, des attaquants peuvent malgré tout utiliser des chemins de mouvement latéral pour accéder aux comptes sensibles. Dans les attaques par mouvement latéral, l’attaquant tire parti d’instances quand les utilisateurs sensibles se connectent à une machine où un utilisateur non sensible a des droits locaux. Les attaquants peuvent ensuite se déplacer latéralement, accéder à l’utilisateur moins sensible, puis se déplacer au sein de l’ordinateur pour se procurer les informations d’identification de l’utilisateur sensible. 

## <a name="what-is-a-lateral-movement-path"></a>Qu’est-ce qu’un chemin de mouvement latéral ?

Il est question de mouvement latéral quand un attaquant utilise de façon proactive des comptes non sensibles pour accéder à des comptes sensibles. Il peut utiliser l’une des méthodes décrites dans le [Guide des activités suspectes](suspicious-activity-guide.md) pour obtenir le mot de passe non sensible initial, puis employer un outil tel que Bloodhound afin d’identifier les administrateurs de votre réseau et les ordinateurs auxquels ils accèdent. Il peut ensuite accéder aux données sur vos contrôleurs de domaine pour savoir qui a quels comptes et accès à quels fichiers et ressources, et voler les informations d’identification d’autres utilisateurs (parfois sensibles) qui sont stockées sur les ordinateurs auxquels ils ont déjà accédé, puis se déplacer latéralement parmi les utilisateurs et les ressources jusqu’à obtenir des privilèges d’administrateur sur votre réseau. 

ATA vous permet de prendre des mesures préemptives sur votre réseau pour empêcher les attaquants de réussir tout mouvement latéral.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Détection de vos comptes sensibles à risque

Pour détecter les comptes sensibles de votre réseau qui sont vulnérables en raison de leur connexion à des comptes ou des ressources non sensibles, effectuez les étapes suivantes. Pour sécuriser votre réseau contre les attaques par mouvement latéral, ATA part de la fin, ce qui signifie qu’il vous donne une carte qui commence par vos comptes privilégiés, puis vous montre les utilisateurs et les appareils qui se trouvent sur le chemin latéral de ces utilisateurs avec leurs informations d’identification.

1. Dans le menu de la console ATA, cliquez sur l’icône Rapports ![Icône Rapports](./media/ata-report-icon.png).

2. Sous **Chemins d’accès de mouvement latéral pour les comptes sensibles**, en l’absence de chemins de mouvement latéral, le rapport est grisé. S’il existe des chemins de mouvement latéral, les dates du rapport sélectionnent automatiquement la première date avec des données pertinentes. 

 ![rapports](./media/reports.png)

3. Cliquez sur **Télécharger**.

3. Le fichier Excel qui est créé vous fournit plus d’informations sur les comptes sensibles qui présentent des risques. L’onglet **Résumé** propose des graphes qui décrivent en détail le nombre de comptes sensibles, les ordinateurs et les moyennes pour les ressources à risque. L’onglet **Détails** présente une liste des comptes sensibles dont vous devez vous soucier.


## <a name="investigate"></a>Étudier

Maintenant que vous avez identifié les comptes sensibles qui présentent des risques, vous pouvez vous plonger dans ATA pour en savoir plus et prendre des mesures préventives.

1. Dans la console ATA, examinez l’utilisateur dont le compte est répertorié comme vulnérable dans le rapport **Chemins d’accès de mouvement latéral pour les comptes sensibles**, par exemple Samira Abbasi. Vous pouvez également rechercher le badge de mouvement latéral qui est ajouté au profil d’entité quand l’entité figure sur un chemin de mouvement latéral ![icône de mouvement latéral](./media/lateral-movement-icon.png) ou ![icône de chemin](./media/paths-icon.png).

2. Dans la page de profil utilisateur qui s’ouvre, cliquez sur l’onglet **Chemins d’accès de mouvement latéral**.

3. Le diagramme qui s’affiche vous fournit une carte des chemins possibles pour votre utilisateur sensible. Comme le graphe affiche les connexions qui ont été établies au cours des deux derniers jours, l’exposition aux risques est récente.

4. Examinez le graphe pour voir si vous pouvez en savoir plus sur l’exposition aux risques des informations d’identification de l’utilisateur sensible. Par exemple, dans cette carte de Samira Abbasi, vous pouvez suivre les flèches grises **Connecté par** pour voir où Samira s’est connectée avec ses informations d’identification privilégiées. Dans ce cas, les informations d’identification sensibles de Samira ont été enregistrées sur l’ordinateur REDMOND-WA-DEV. Ensuite, identifiez quels autres utilisateurs connectés à quels ordinateurs ont généré le plus de risques et de vulnérabilité. Pour ce faire, examinez les flèches noires **Administrateur de** afin de savoir qui possède des privilèges d’administrateur sur la ressource. Dans cet exemple, chaque membre du groupe Contoso All a la possibilité d’accéder aux informations d’identification d’utilisateur à partir de cette ressource.  

 ![chemins de mouvement latéral du profil utilisateur](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Bonnes pratiques de prévention

- La meilleure façon d’empêcher un mouvement latéral consiste à vérifier que les utilisateurs sensibles utilisent leurs informations d’identification d’administrateur uniquement quand ils se connectent aux ordinateurs renforcés où aucun utilisateur non sensible n’a de droits d’administration sur le même ordinateur. Dans l’exemple, vérifiez que si Samira doit accéder à REDMOND-WA-DEV, elle se connecte avec un nom d’utilisateur et un mot de passe qui ne sont pas ses informations d’identification d’administrateur, ou supprime le groupe Contoso All du groupe d’administrateurs local sur REDMOND-WA-DEV.

- Il est également recommandé de vérifier que personne ne dispose d’autorisations d’administration locales inutiles. Dans l’exemple, vous devez vérifier si tous les membres du groupe Contoso All ont réellement besoin des droits d’administrateur sur REDMOND-WA-DEV.

- Il est toujours judicieux de s’assurer que les utilisateurs ont uniquement accès aux ressources nécessaires. Comme vous pouvez le voir dans l’exemple, Oscar Posada augmente considérablement les risques de Samira. Est-il nécessaire qu’il soit inclus dans Contoso All ? Avez-vous la possibilité de créer des sous-groupes pour minimiser les risques ?


## <a name="see-also"></a>Voir aussi
- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
