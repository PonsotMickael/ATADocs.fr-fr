---
title: "Examen des attaques à l’aide d’un faux PAC | Microsoft Docs"
description: "Cet article décrit l’attaque à l’aide d’un faux PAC et fournit des instructions d’examen quand cette menace est détectée sur votre réseau."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/16/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: f3db435e-9553-40a2-a2ad-278fad4f0ef5
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 437f387815fbbfbe261a192764a428e0d285ef32
ms.sourcegitcommit: 97aced94f47cf3c1b473d25b77d10a300c3f517e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/16/2017
---
*S’applique à : Advanced Threat Analytics version 1.7*

# <a name="investigating-forged-pac-attacks"></a>Examen des attaques à l’aide d’un faux PAC

Microsoft améliore en permanence ses fonctions de détection de sécurité et la possibilité de fournir des renseignements exploitables quasiment en temps réel aux analystes de sécurité. Microsoft ATA (Advanced Threat Analytics) aide à mener à bien ce changement. Si ATA détecte une activité suspecte à l’aide d’un faux PAC sur votre réseau et vous en informe, cet article vous aide à comprendre et examiner cette activité.

## <a name="what-is-a-privileged-access-certificate-pac"></a>Qu’est-ce qu’un certificat PAC (Privilege Attribute Certificate) ?

Le certificat PAC (Privilege Attribute Certificate) est la structure de données dans le ticket Kerberos qui contient les informations d’autorisation, dont les appartenances aux groupes, les identificateurs de sécurité et les informations de profil utilisateur. Dans un domaine Active Directory, il permet de transmettre les données d’autorisation fournies par le contrôleur de domaine à d’autres stations de travail et serveurs membres à des fins d’authentification et d’autorisation. En plus des informations d’appartenance, le certificat PAC inclut des informations d’identification supplémentaires, des informations sur les profils et stratégies ainsi que des métadonnées de sécurité de prise en charge. 

La structure de données du certificat PAC est utilisée par les protocoles d’authentification (protocoles qui vérifient les identités) pour transporter les informations d’autorisation, qui contrôlent l’accès aux ressources.

### <a name="pac-validation"></a>Validation PAC

La validation PAC est une fonctionnalité de sécurité pour empêcher un intrus d’obtenir un accès non autorisé à un système ou ses ressources par une attaque de l’intercepteur (« man in the middle), en particulier dans les applications où l’emprunt d’identité d’utilisateur est utilisé. L’emprunt d’identité implique une identité approuvée, comme un compte de service qui reçoit des privilèges élevés pour accéder aux ressources et exécuter des tâches. La validation PAC renforce un environnement d’autorisation plus sécurisé dans les paramètres d’authentification Kerberos où l’emprunt d’identité se produit. La [validation PAC](https://blogs.msdn.microsoft.com/openspecification/2009/04/24/understanding-microsoft-kerberos-pac-validation/) garantit qu’un utilisateur présente exactement les mêmes données d’autorisation que celles qu’il a reçues dans le ticket Kerberos et que les privilèges du ticket n’ont pas été modifiés.

Lors de la validation PAC, le serveur encode un message de demande qui contient la longueur et le type de signature PAC, puis le transmet au contrôleur de domaine. Le contrôleur de domaine décode la demande et extrait la somme de contrôle serveur ainsi que les valeurs de somme de contrôle du contrôleur de domaine Kerberos (KDC). Si la vérification de la somme de contrôle réussit, le contrôleur de domaine retourne un code de réussite au serveur. Un code de retour d’échec indique que le certificat PAC a été altéré. 

Le contenu du certificat PAC Kerberos est signé à deux reprises : 
- Une fois avec la clé principale du contrôleur KDC pour empêcher des services côté serveur malveillants de modifier les données d’autorisation
- Une fois avec la clé principale de compte du serveur de ressources de destination pour empêcher un utilisateur de modifier le contenu du certificat PAC et d’ajouter ses propres données d’autorisation

### <a name="pac-vulnerability"></a>Vulnérabilité PAC
Les bulletins de sécurité [MS14-068](https://technet.microsoft.com/library/security/MS14-068.aspx) et [MS11-013](https://technet.microsoft.com/library/security/ms11-013.aspx) résolvent des vulnérabilités du contrôleur de domaine Kerberos qui peuvent permettre à un attaquant de manipuler le champ PAC dans un ticket Kerberos valide et de s’octroyer ainsi des privilèges supplémentaires.

## <a name="forged-pac-attack"></a>Attaque à l’aide d’un faux PAC

Une attaque à l’aide d’un faux PAC est une tentative par une personne malveillante de tirer parti de ces vulnérabilités pour élever ses privilèges dans votre domaine ou forêt Active Directory. Pour effectuer cette attaque, l’attaquant doit disposer des éléments suivants :
-    Informations d’identification d’un utilisateur du domaine.
-    Connectivité réseau à un contrôleur de domaine qui peut servir à l’authentification avec les informations d’identification de domaine compromises.
-    Outils appropriés. PyKEK (Python Kerberos Exploitation Kit) est un outil connu qui contrefait les certificats PAC.

Si l’attaquant a la connectivité et les informations d’identification nécessaires, il peut modifier ou contrefaire le certificat PAC d’un jeton d’ouverture de session d’utilisateur Kerberos existant. Il modifie la revendication de l’appartenance au groupe pour inclure un groupe doté de privilèges plus élevés (par exemple, « Administrateurs de domaine » ou « Administrateurs de l’entreprise »). Il inclut ensuite le certificat PAC modifié dans le ticket Kerberos. Ce ticket Kerberos est ensuite utilisé pour demander un ticket de service auprès d’un contrôleur de domaine non corrigé, ce qui accorde à l’attaquant des autorisations élevées dans le domaine et l’autorisation d’exécuter des actions qui lui sont interdites. Un attaquant peut présenter le jeton d’ouverture de session d’utilisateur modifié pour accéder à n’importe quelle ressource dans le domaine en demandant des jetons d’accès aux ressources. Cela signifie qu’il peut contourner toutes les listes de contrôle d’accès aux ressources configurées qui limitent l’accès sur le réseau par usurpation des données d’autorisation pour tous les utilisateurs dans Active Directory.

## <a name="discovering-the-attack"></a>Détection de l’attaque
Quand l’attaquant essaie d’élever ses privilèges, ATA le détecte et marque cette opération comme une alerte d’un niveau de gravité élevé.

![Activité suspecte à l’aide d’un faux PAC](./media/forged-pac.png)

ATA indique dans l’alerte d’activité suspecte si le faux PAC a réussi ou a échoué. Vous devez examiner à la fois les alertes de réussite et d’échec, car les tentatives ayant échoué peuvent toujours indiquer la présence d’un utilisateur malveillant dans votre environnement.

## <a name="investigating"></a>Examen
Après avoir reçu l’alerte d’un faux PAC dans ATA, vous devez déterminer ce qui doit être fait pour atténuer le risque. Pour ce faire, vous devez tout d’abord classer l’alerte comme suit : 
-    Vrai positif : action malveillante détectée par ATA
-    Faux positif : fausse alerte (il ne s’agissait pas en réalité d’un faux PAC, plutôt d’un événement qu’ATA a confondu avec une attaque à l’aide d’un faux PAC)
-    Vrai positif bénin : action détectée par ATA qui est réelle, mais pas malveillante, comme un test de pénétration

Le graphique suivant vous aide à déterminer les étapes à suivre :

![Diagramme de faux PAC](./media/forged-pac-diagram.png)

1. Vérifiez tout d’abord l’alerte dans la chronologie des attaques d’ATA pour voir si la tentative d’autorisation contrefaite a réussi, a échoué ou a été tentée (les attaques tentées sont également des attaques ayant échoué). Les tentatives ayant réussi et échoué peuvent toutes deux aboutir à un vrai positif, mais avec différents niveaux de gravité dans l’environnement.
 
 ![Activité suspecte à l’aide d’un faux PAC](./media/forged-pac-sa.png)


2.    Si l’attaque à l’aide d’un faux PAC détectée a réussi :
    -    Si le contrôleur de domaine sur lequel l’alerte a été déclenchée est correctement corrigé, il s’agit d’un faux positif. Dans ce cas, vous devez ignorer l’alerte et envoyer un e-mail de notification à l’équipe ATA à l’adresse ATAEval@microsoft.com pour que nous puissions améliorer en permanence nos détections. 
    -    Si le contrôleur de domaine dans l’alerte n’est pas correctement corrigé :
        -    Si le service répertorié dans l’alerte n’a pas son propre mécanisme d’autorisation, il s’agit d’un vrai positif et vous devez exécuter le processus de réponse aux incidents de votre organisation. 
        -    Si le service répertorié dans l’alerte a un mécanisme d’autorisation interne qui demande des données d’autorisation, il peut être identifié par erreur comme un faux PAC. 

3.    Si l’attaque détectée a échoué :
    -    Si le système d’exploitation ou l’application est connu pour modifier le certificat PAC, il s’agit probablement d’un vrai positif bénin et vous devez collaborer avec le propriétaire de l’application ou du système d’exploitation pour corriger ce comportement.

    -    Si le système d’exploitation ou l’application n’est pas connu pour modifier le certificat PAC : 

        -    Si le service répertorié n’a pas son propre service d’autorisation, il s’agit d’un vrai positif et vous devez exécuter le processus de réponse aux incidents de votre organisation. Même si l’attaquant n’a pas réussi à élever ses privilèges dans le domaine, vous pouvez supposer qu’une personne malveillante est présente sur votre réseau et vous voulez la localiser aussi rapidement que possible avant qu’elle ne tente d’autres attaques répétées et avancées connues pour élever ses privilèges. 
        -    Si le service répertorié dans l’alerte a son propre mécanisme d’autorisation qui demande des données d’autorisation, il peut être identifié par erreur comme un faux PAC.


Microsoft recommande d’utiliser une équipe IR&R (Incident Response & Recovery) professionnelle, qui peut être contactée via votre équipe des comptes Microsoft, afin de détecter si un attaquant a déployé des méthodes de persistance sur votre réseau. Ces méthodes peuvent avoir été déployées via l’utilisation de logiciel malveillant et par des violations d’identités, comme des informations d’identification volées et des golden tickets.


## <a name="see-also"></a>Voir aussi
- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Modification de la configuration d’ATA](modifying-ata-configuration.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
