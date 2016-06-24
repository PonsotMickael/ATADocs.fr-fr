---
# required metadata

title: Qu’est-ce que Microsoft Advanced Threat Analytics (ATA) ? | Microsoft Advanced Threat Analytics
description: Explique ce qu’est Microsoft Advanced Threat Analytics (ATA) et quels types d’activités suspectes il peut détecter
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


## Qu’est-ce qu’ATA ?
Microsoft Advanced Threat Analytics (ATA) est une solution de sécurité qui permet aux professionnels de la sécurité informatique de protéger leur entreprise contre les attaques ciblées avancées et les menaces internes. ATA analyse, détecte et identifie automatiquement les comportements normaux et anormaux des entités (utilisateurs, appareils et ressources) pour identifier les attaques connues, ainsi que les problèmes et les risques de sécurité. Grâce à une intelligence et à une analyse de sécurité de pointe, cette technologie innovante est conçue pour aider les entreprises à se concentrer sur l’identification des failles de sécurité avant qu’elles ne causent des dommages.

## Que fait ATA ?
ATA détecte :

  - Les menaces persistantes avancées (APT) au début du processus « kill-chain », avant qu’elles ne puissent causer des dommages

  - Les menaces internes

  ATA permet également de distinguer les menaces réelles des fausses menaces pour que vous puissiez vous concentrer sur le plus important.

ATA a un moteur de détection qui utilise l’apprentissage automatique, l’inspection approfondie des paquets en fonction de l’entité, l’analyse des journaux et les informations Active Directory (AD) afin d’analyser le comportement des utilisateurs et des entités.
ATA analyse le trafic en profondeur et utilise l’apprentissage automatique pour générer une carte des activités, des utilisations et du trafic considérés comme normaux au sein de votre entreprise. Ensuite, ATA surveille les activités et vous avertit quand des événements anormaux se produisent. Pour cela, vous devez exécuter la technologie d’inspection approfondie des paquets de Microsoft (DPI). Cette technologie permet l’inspection des paquets en fonction de l’entité pour une analyse plus approfondie du trafic réseau. ATA peut ainsi analyser tous les niveaux de votre trafic réseau.

ATA collecte également les événements pertinents provenant des contrôleurs de domaine et des systèmes SIEM. Après l’analyse, ATA génère une vue dynamique et mise à jour en continu des personnes, des appareils et des ressources de votre entreprise. Grâce à cette vue d’ensemble, ATA est en mesure de détecter les attaques connues telles que les attaques de type Pass-the-Hash, Pass-the-Ticket, Reconnaissance, etc. ATA recherche également les anomalies dans le comportement des entités de votre réseau.  

Quand une activité suspecte est détectée, ATA déclenche une alerte en réduisant le nombre de faux positifs grâce à des algorithmes avancés d’agrégation et de vérification du contexte.


## Quelles sont les menaces que recherche ATA ?

ATA fournit une fonctionnalité de détection pour les différentes phases d’une attaque avancée : reconnaissance, compromission des informations d’identification, mouvement latéral, élévation des privilèges, contrôle du domaine, etc. Les attaques avancées et les menaces internes peuvent ainsi être détectées avant de pouvoir nuire à votre entreprise.

Chaque type de détection correspond à un ensemble d’activités suspectes liées à la phase en question. Chaque activité suspecte correspond à différents types d’attaques possibles.


### Reconnaissance
ATA fournit plusieurs outils de détection de reconnaissance. Par exemple, l’activité suspecte **Reconnaissance à l’aide de l’énumération de compte** détecte les tentatives d’attaques à l’aide du protocole Kerberos afin de vérifier si un utilisateur existe réellement, même si l’activité n’a pas été enregistrée comme un événement dans le contrôleur de domaine.

### Compromission des informations d’identification

Pour détecter la compromission des informations d’identification, ATA utilise une analyse comportementale basée sur l’apprentissage automatique, ainsi que la détection des attaques et techniques connues.  

Grâce à l’apprentissage automatique et à l’analyse comportementale, ATA peut détecter les activités suspectes, telles que les connexions suspectes, les accès anormaux aux ressources et les heures de travail anormales. Ces activités suspectes indiquent une possible compromission des informations d’identification.

Pour protéger les informations d’identification, ATA détecte les attaques et techniques connues suivantes :

 - **Attaque par force brute** : lors des attaques par force brute, les attaquants tentent de deviner les informations d’identification des utilisateurs en essayant de faire correspondre des utilisateurs et des mots de passe. Les attaquants utilisent souvent des algorithmes complexes ou des dictionnaires pour essayer autant de valeurs que le permet le système.

- **Compte sensible exposé par l’authentification en texte brut** : si les informations d’identification d’un compte avec privilèges élevés sont envoyées en texte brut, ATA vous en avertit pour que vous puissiez modifier la configuration de l’ordinateur.

- **Service exposant des comptes par l’authentification en texte brut** : si un service présent sur un ordinateur envoie plusieurs informations d’identification en texte brut, ATA vous en avertit pour que vous puissiez modifier la configuration du service.

- **Activités suspectes liées à un compte honeytoken** : les comptes honeytoken sont des comptes factices destinés à piéger, identifier et suivre les activités malveillantes qui tentent d’utiliser ces comptes factices.

### Mouvement latéral
On appelle « mouvement latéral » l’acte par lequel un utilisateur se sert d’informations d’identification permettant d’accéder à certaines ressources dans le but d’accéder à d’autres ressources auxquelles il n’est pas autorisé à accéder. Pour détecter les mouvements latéraux, ATA utilise une analyse comportementale basée sur l’apprentissage automatique, ainsi que la détection des attaques et techniques connues.  

ATA détecte les accès anormaux aux ressources, les utilisations anormales d’appareils, ainsi que d’autres indicateurs de mouvements latéraux. En outre, ATA peut repérer un mouvement latéral grâce à la détection des techniques utilisées par les pirates pour effectuer un mouvement latéral, par exemple :
- **Pass-the-Ticket** : lors des attaques de type Pass-the-Ticket, les attaquants volent un ticket Kerberos sur un ordinateur et l’utilisent pour accéder à un autre ordinateur en empruntant l’identité d’une entité de votre réseau.
- **Pass-the-Hash** : lors des attaques de type Pass-the-Hash, les attaquants volent le code de hachage NTLM d’une entité et l’utilisent pour s’authentifier auprès de NTLM et emprunter l’identité de l’entité pour accéder aux ressources de votre réseau.
- **Overpass-the-Hash** : lors des attaques de type Overpass-the-Hash, l’attaquant utilise un code de hachage NTLM volé pour s’authentifier auprès de Kerberos et obtenir un ticket Kerberos TGT valide, qu’il utilise ensuite pour s’authentifier en tant qu’utilisateur valide et accéder aux ressources de votre réseau.

### Élévation des privilèges
Une attaque par élévation des privilèges se produit quand des attaquants tentent d’élever leurs privilèges existants et les utilisent à plusieurs reprises pour prendre le contrôle total de l’environnement de la victime. ATA détecte les attaques par élévation de privilèges et les tentatives de telles attaques. ATA utilise l’analyse comportementale pour détecter les comportements anormaux parmi les comptes à privilèges élevés. ATA détecte également les attaques et techniques connues qui sont souvent utilisées pour élever les privilèges, par exemple :
- **Code malveillant exploitant une faille de sécurité MS14-068 (faux PAC)** : les faux PAC sont des attaques au cours desquelles l’attaquant intègre des données d’autorisation à un ticket TGT valide sous la forme d’un en-tête d’autorisation falsifié. Grâce à cette technique, l’attaquant obtient des autorisations qui ne lui ont pas été accordées par l’entreprise.
- Utilisation d’informations d’identification précédemment compromises ou récoltées au cours d’opérations de mouvement latéral.

### Contrôle du domaine
Lors d’une attaque de contrôle de domaine, les attaquants tentent ou réussissent à obtenir le contrôle total de l’environnement de la victime. ATA détecte ces tentatives en recherchant les techniques connues utilisées par les attaquants, notamment :
- **Programme malveillant Skeleton Key** : lors des attaques de type Skeleton Key, un programme malveillant est installé sur votre contrôleur de domaine afin de permettre aux attaquants de s’authentifier comme n’importe quel utilisateur, tout en permettant aux utilisateurs légitimes d’ouvrir une session.
- **Golden Ticket** : lors des attaques par Golden Ticket, un attaquant vole des informations d’identification d’un KBTGT, le Golden Ticket Kerberos. Ce ticket permet à l’attaquant de créer un ticket TGT hors connexion et de l’utiliser pour accéder aux ressources du réseau.
- **Exécution à distance** : les attaquants peuvent tenter de contrôler votre réseau en exécutant du code à distance sur votre contrôleur de domaine.


## Quelle est l'étape suivante ?

-   Pour plus d’informations sur la façon dont ATA s’intègre à votre réseau, voir [Architecture ATA](ata-architecture.md).

-   Pour commencer le déploiement d’ATA, voir [Installer ATA](/advanced-threat-analytics/DeployUse/install-ata).

## Voir aussi
[Pour obtenir de l’aide sur ATA, consultez notre forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


