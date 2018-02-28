---
title: "Examen des attaques par chemins de mouvement latéral avec Azure ATP | Microsoft Docs"
description: "Cet article décrit comment détecter des attaques par chemins de mouvement latéral avec Azure - Protection avancée contre les menaces (ATP)."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: de15c920-8904-4124-8bdc-03abd9f667cf
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7deeec2c2ee2c2d964b6495921eba0fa378bd8ee
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2018
---
*S’applique à : Azure - Protection avancée contre les menaces version 1.9*

# <a name="investigating-lateral-movement-paths-with-azure-atp"></a>Examen des chemins de mouvement latéral avec Azure ATP

Azure ATP peut vous aider à empêcher les attaques qui utilisent des chemins de mouvement latéral. Même si vous faites de votre mieux pour protéger les utilisateurs sensibles (les administrateurs ont des mots de passe complexes qu’ils changent fréquemment, leurs ordinateurs sont sécurisés de manière renforcée et leurs données sont stockées en toute sécurité), des attaquants peuvent quand même utiliser des chemins de mouvement latéral et se déplacer sur votre réseau entre les utilisateurs et les ordinateurs jusqu’à ce qu’ils touchent le gros lot en matière de sécurité virtuelle : les informations d’identification sensibles de votre compte d’administrateur.

## <a name="what-is-a-lateral-movement-path"></a>Qu’est-ce qu’un chemin de mouvement latéral ?

Il est question de mouvement latéral quand un attaquant utilise de façon proactive des comptes non sensibles pour accéder à des comptes sensibles. Il peut utiliser l’une des méthodes décrites dans le [Guide des activités suspectes](suspicious-activity-guide.md) pour obtenir le mot de passe non sensible initial, puis employer un outil tel que Bloodhound afin d’identifier les administrateurs de votre réseau et les ordinateurs auxquels ils accèdent. Il peut ensuite tirer parti des données accessibles aux attaquants sur vos contrôleurs de domaine pour savoir qui a quels comptes et accès à quels fichiers et ressources, et voler les informations d’identification d’autres utilisateurs (parfois sensibles) stockées sur les ordinateurs auxquels ils ont déjà accédé, puis se déplacer latéralement vers de plus en plus d’utilisateurs et de ressources jusqu’à ce qu’il obtienne des privilèges d’administrateur sur votre réseau. 

Azure ATP vous permet de prendre des mesures préemptives sur votre réseau pour empêcher les attaquants de réussir tout mouvement latéral.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Détection de vos comptes sensibles à risque

Pour détecter les comptes sensibles de votre réseau qui sont vulnérables en raison de leur connexion à des comptes ou des ressources non sensibles, effectuez les étapes suivantes. Pour sécuriser votre réseau contre les attaques par mouvement latéral, Azure ATP fonctionne à partir de la fin et vers l’arrière, ce qui signifie qu’il vous donne un mappage qui commence au niveau de vos comptes privilégiés, puis affiche les utilisateurs et appareils se trouvant sur le chemin latéral de ces utilisateurs avec leurs informations d’identification.

1. Dans le menu du portail de l’espace de travail Azure ATP, cliquez sur l’icône Rapports ![Icône Rapports](./media/atp-report-icon.png).

2. Sous **Chemins d’accès de mouvement latéral pour les comptes sensibles**, en l’absence de chemins de mouvement latéral, le rapport est grisé. S’il existe des chemins de mouvement latéral, les dates du rapport sélectionnent automatiquement la première date avec des données pertinentes. Le rapport des chemins de mouvement latéral contient des données pour les 60 derniers jours.

 ![rapports](./media/reports.png)

3. Cliquez sur **Télécharger**.

3. Le fichier Excel qui est créé vous fournit plus d’informations sur les comptes sensibles qui présentent des risques. L’onglet **Résumé** propose des graphes qui décrivent en détail le nombre de comptes sensibles, les ordinateurs et les moyennes pour les ressources à risque. L’onglet **Détails** présente une liste des comptes sensibles dont vous devez vous soucier.

4. Pour obtenir des instructions sur la configuration de vos serveurs afin d’autoriser Azure ATP à effectuer les opérations SAM-R nécessaires pour la détection des chemins de mouvement latéral, [configurez SAM-R](install-atp-step8-samr.md).

## <a name="investigate"></a>Investiguer

Maintenant que vous avez identifié les comptes sensibles qui présentent des risques, vous pouvez vous plonger dans Azure ATP pour en savoir plus et prendre des mesures préventives.

1. Dans le portail de l’espace de travail Azure ATP, examinez l’utilisateur dont le compte est répertorié comme vulnérable dans le rapport **Chemins d’accès de mouvement latéral pour les comptes sensibles**, par exemple Samira Abbasi. Vous pouvez également rechercher le badge de mouvement latéral qui est ajouté au profil d’entité quand l’entité figure sur un chemin de mouvement latéral ![icône de mouvement latéral](./media/lateral-movement-icon.png) ou ![icône de chemin](./media/paths-icon.png). Cette opération est possible si un mouvement latéral s’est produit dans les deux derniers jours. 

2. Dans la page de profil utilisateur qui s’ouvre, cliquez sur l’onglet **Chemins d’accès de mouvement latéral**. 

3. Le diagramme qui s’affiche vous fournit un mappage des chemins possibles pour votre utilisateur sensible. Comme le graphe affiche les connexions qui ont été établies au cours des deux derniers jours, l’exposition aux risques est récente. Si aucune activité n’est détectée au cours des deux derniers jours, le graphe n’apparaît pas, mais le [rapport des chemins de mouvement latéral](reports.md) vous fournit toujours des informations sur les chemins de mouvement latéral au cours des 60 derniers jours.

4. Examinez le graphe pour voir si vous pouvez en savoir plus sur l’exposition aux risques des informations d’identification de l’utilisateur sensible. Par exemple, dans ce mappage lié à Samira Abbasi, vous pouvez suivre les flèches grises **Connecté par** pour voir où Samira s’est connectée avec ses informations d’identification privilégiées. Dans ce cas, les informations d’identification sensibles de Samira ont été enregistrées sur l’ordinateur REDMOND-WA-DEV. Ensuite, identifiez quels autres utilisateurs connectés à quels ordinateurs ont généré le plus de risques et de vulnérabilité. Pour ce faire, examinez les flèches noires **Administrateur de** afin de savoir qui possède des privilèges d’administrateur sur la ressource. Dans cet exemple, chaque membre du groupe Contoso All a la possibilité d’accéder aux informations d’identification d’utilisateur à partir de cette ressource.  

 ![chemins de mouvement latéral du profil utilisateur](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Bonnes pratiques de prévention

- La meilleure façon d’empêcher un mouvement latéral consiste à vérifier que les utilisateurs sensibles utilisent leurs informations d’identification d’administrateur uniquement lors de la connexion aux ordinateurs sécurisés de manière renforcée. Dans l’exemple, assurez-vous que si l’administrateur Samira doit accéder à REDMOND-WA-DEV, elle se connecte avec un nom d’utilisateur et un mot de passe autres que ses informations d’identification d’administrateur.

- Il est également recommandé de vérifier que personne ne dispose d’autorisations d’administration inutiles. Dans l’exemple, vous devez vérifier si tous les membres du groupe Contoso All ont réellement besoin des droits d’administrateur sur REDMOND-WA-DEV.

- Il est toujours judicieux de s’assurer que les utilisateurs ont uniquement accès aux ressources nécessaires. Comme vous pouvez le voir dans l’exemple, Oscar Posada augmente considérablement les risques de Samira. Est-il nécessaire que l’utilisateur soit inclus dans Contoso All ? Avez-vous la possibilité de créer des sous-groupes pour minimiser les risques ?


## <a name="see-also"></a>Voir aussi

- [Configurer les autorisations requises SAM-R](install-atp-step8-samr.md)
- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consultez le forum ATP !](https://aka.ms/azureatpcommunity)