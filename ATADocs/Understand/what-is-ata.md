---
title: "Qu’est-ce que Microsoft Advanced Threat Analytics (ATA) ? | Microsoft ATA"
description: "Explique ce qu’est Microsoft Advanced Threat Analytics (ATA) et quels types d’activités suspectes il peut détecter"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 58afbae96bce0075f0a58be648e82744ce279997


---


## Qu’est-ce qu’ATA ?
Microsoft Advanced Threat Analytics (ATA) est une solution de pointe dans le domaine de l’analyse du comportement des utilisateurs et des entités qui permet aux professionnels de la sécurité informatique de protéger leur entreprise contre les attaques ciblées avancées et les menaces internes. En analysant, détectant et identifiant automatiquement les comportements normaux et anormaux des entités (utilisateurs, appareils et ressources) au moyen d’une technologie d’apprentissage automatique avancée, ATA facilite l’identification des attaques connues, ainsi que des problèmes et des risques de sécurité. Grâce à une intelligence et à une analyse de sécurité de pointe, cette technologie innovante est conçue pour aider les entreprises à se concentrer sur l’identification des failles de sécurité avant qu’elles ne causent des dommages.

## Que fait ATA ?
ATA détecte :

  - Les menaces persistantes avancées (APT) au début du processus « kill-chain », avant qu’elles ne puissent causer des dommages

  - Les menaces internes

ATA vous permet de distinguer les activités suspectes réelles des fausses menaces, pour que vous puissiez vous concentrer sur le plus important.

Le moteur de détection d’ATA utilise l’apprentissage automatique, l’inspection approfondie des paquets en fonction de l’entité, l’analyse des journaux et les informations Active Directory (AD) pour analyser le comportement des utilisateurs et des entités.

ATA exécute une analyse approfondie du trafic de votre entreprise et utilise l’apprentissage automatique pour générer une carte des activités, des utilisations et du trafic considérés comme normaux au sein de votre entreprise. Ensuite, ATA surveille les activités et vous avertit quand des événements anormaux se produisent. Cette opération est effectuée en exécutant la technologie d’inspection approfondie des paquets de Microsoft (DPI), qui permet l’inspection des paquets en fonction de l’entité pour une analyse plus approfondie du trafic réseau. ATA peut ainsi analyser tous les niveaux de votre trafic réseau.

ATA collecte également les événements pertinents provenant des contrôleurs de domaine et des systèmes SIEM. Après l’analyse, ATA génère une vue dynamique et mise à jour en continu des personnes, des appareils et des ressources de votre entreprise. Grâce à cette vue d’ensemble, ATA est en mesure de détecter les attaques connues telles que les attaques de type Pass-the-Hash, Pass-the-Ticket, Reconnaissance, etc., ainsi que de rechercher les anomalies dans le comportement des entités de votre réseau.

Quand une activité suspecte est détectée, ATA déclenche une alerte en réduisant le nombre de faux positifs grâce à des algorithmes avancés d’agrégation et de vérification du contexte.



## Quelles sont les menaces que recherche ATA ?

ATA fournit une fonctionnalité de détection pour les différentes phases d’une attaque avancée : reconnaissance, compromission des informations d’identification, mouvement latéral, élévation des privilèges, contrôle du domaine, etc. Les attaques avancées et les menaces internes peuvent ainsi être détectées avant de pouvoir causer des dommages pour votre entreprise.

Chaque type de détection correspond à un ensemble d’activités suspectes liées à la phase en question, chacune de ces activités correspondant elle-même à différents types d’attaques possibles.

### Reconnaissance
ATA fournit plusieurs outils de détection de reconnaissance. Ces détections sont les suivantes :

-   **Reconnaissance à l’aide de l’énumération de compte**<br>Détecte les tentatives d’attaques à l’aide du protocole Kerberos afin de vérifier si un utilisateur existe réellement, même si l’activité n’a pas été enregistrée comme événement dans le contrôleur de domaine.
-   **Énumération de sessions Net**<br>
Dans le cadre de la phase de reconnaissance, les attaquants peuvent interroger le contrôleur de domaine pour identifier toutes les sessions SMB actives sur le serveur, ce qui leur permet d’accéder à l’ensemble des utilisateurs et des adresses IP associés à ces sessions SMB. L’énumération de sessions SMB peut être utilisée par des attaquants pour cibler des comptes sensibles et leur permettre de se déplacer latéralement sur le réseau.
-   **Reconnaissance à l’aide de DNS**<br>
Les informations DNS sur le réseau cible sont souvent des informations de reconnaissance très utiles. Les informations DNS contiennent la liste de tous les serveurs et souvent de tous les clients, ainsi que le mappage à leurs adresses IP. La consultation des informations DNS peut fournir aux attaquants une vue détaillée de ces entités dans votre environnement, leur permettant de concentrer leurs efforts sur les entités pertinentes pour la campagne.

### Informations d’identification compromises

Pour détecter la compromission des informations d’identification, ATA utilise une analyse comportementale basée sur l’apprentissage automatique, ainsi que la détection des attaques et techniques connues.

Grâce à l’apprentissage automatique et à l’analyse comportementale, ATA peut détecter les activités suspectes, telles que les connexions suspectes, les accès anormaux aux ressources et les heures de travail anormales pouvant indiquer une compromission des informations d’identification.
Pour protéger les informations d’identification, ATA détecte les attaques et techniques connues suivantes :

 - **Force brute** <br>Pendant les attaques par force brute, les attaquants tentent de deviner les informations d’identification des utilisateurs en essayant de faire correspondre des utilisateurs et des mots de passe. Les attaquants utilisent souvent des algorithmes complexes ou des dictionnaires pour essayer autant de valeurs que le permet le système.

- **Compte sensible exposé par l’authentification en texte brut**<br>
Si les informations d’identification d’un compte avec privilèges élevés sont envoyées en texte brut, ATA vous en avertit pour que vous puissiez mettre à jour la configuration de l’ordinateur.

- **Service exposant des comptes par l’authentification en texte brut** <br>
Si un service présent sur un ordinateur envoie plusieurs informations d’identification de compte en texte brut, ATA vous en avertit pour que vous puissiez mettre à jour la configuration du service.

- **Activités suspectes liées à un compte honeytoken**<br>
Les comptes honeytoken sont des comptes factices destinés à piéger, identifier et suivre les activités malveillantes qui tentent d’utiliser ces comptes factices. ATA vous signale toutes les activités dans ces comptes honeytoken.
-   **Implémentation de protocole inhabituelle**<br>
Les demandes d’authentification (Kerberos ou NTLM) sont généralement effectuées à l’aide d’un ensemble normal de protocoles et méthodes. Toutefois, pour s’authentifier, la demande doit simplement respecter un ensemble spécifique d’exigences. Des attaquants peuvent implémenter ces protocoles avec des écarts mineurs par rapport à l’implémentation normale dans l’environnement. Ces écarts peuvent indiquer une tentative en cours ou réussie d’exploitation d’informations d’identification compromises.
-   **Demande d’information privée de protection contre les données malveillantes**<br>
L’API de protection des données (DPAPI) est un service de protection des données basé sur un mot de passe. Ce service de protection est utilisé par diverses applications qui stockent les secrets des utilisateurs, comme les mots de passe de sites web et les informations d’identification de partage de fichiers. Pour prendre en charge les scénarios de perte du mot de passe, les utilisateurs peuvent déchiffrer des données protégées à l’aide d’une clé de récupération qui ne fait pas appel à leur mot de passe. Dans un environnement de domaine, des attaquants peuvent voler à distance la clé de récupération et l’utiliser pour déchiffrer des données protégées sur tous les ordinateurs joints au domaine.
-   **Comportement anormal**<br>
Souvent, en cas de menaces internes et de menaces avancées, les informations d’identification de compte peuvent être compromises à l’aide de méthodes d’ingénierie sociale ou de méthodes et techniques nouvelles qui ne sont pas encore connues. ATA peut détecter ces types de compromission en analysant le comportement de l’entité et en détectant et signalant les anomalies des opérations effectuées par celle-ci.

### Mouvement latéral
Pour détecter le mouvement latéral, acte par lequel un utilisateur se sert d’informations d’identification permettant d’accéder à certaines ressources dans le but d’accéder à des ressources auxquelles il n’est pas autorisé à accéder, ATA utilise une analyse comportementale basée sur l’apprentissage automatique, ainsi que la détection des attaques et techniques connues.

Grâce à l’analyse comportementale et à l’apprentissage automatique, ATA détecte les accès anormaux aux ressources, les utilisations anormales d’appareils, ainsi que d’autres indicateurs de mouvements latéraux.

En outre, ATA peut repérer un mouvement latéral grâce à la détection des techniques utilisées par les pirates pour effectuer un mouvement latéral, par exemple :

- **Pass-the-Ticket** <br>
Dans les attaques de type Pass-the-Ticket, les attaquants volent un ticket Kerberos sur un ordinateur et l’utilisent pour accéder à un autre ordinateur en empruntant l’identité d’une entité de votre réseau.
- **Pass-the-Hash** <br>
Dans les attaques de type Pass-the-Hash, les attaquants volent le code de hachage NTLM d’une entité et l’utilisent pour s’authentifier auprès de NTLM et emprunter l’identité de cette entité pour accéder aux ressources de votre réseau.
- **Overpass-the-Hash**<br>
Dans les attaques de type Overpass-the-Hash, l’attaquant utilise un code de hachage NTLM volé pour s’authentifier auprès de Kerberos et obtenir un ticket Kerberos TGT valide, qu’il utilise ensuite pour s’authentifier en tant qu’utilisateur valide et accéder aux ressources de votre réseau.
-   **Comportement anormal**<br>
Le mouvement latéral est une technique qu’utilise souvent un attaquant pour se déplacer d’un appareil et d’une zone à l’autre du réseau de la victime afin d’accéder à des informations d’identification dotées de privilèges ou à des informations sensibles qui présentent un intérêt particulier. ATA peut détecter un mouvement latéral en analysant le comportement des utilisateurs, des appareils et leurs relations à l’intérieur du réseau d’entreprise, et repérer tout modèle d’accès anormal pouvant indiquer un mouvement latéral effectué par un attaquant.

### Élévation des privilèges
ATA détecte les attaques par élévation des privilèges tentées et réussies, dans lesquelles les attaquants essaient d’élever leurs privilèges existants et les utilisent à plusieurs reprises pour prendre le contrôle total de l’environnement de la victime. 

ATA permet de détecter l’élévation des privilèges en combinant des analyses comportementales pour détecter un comportement anormal des comptes dotés de privilèges, ainsi qu’en détectant les attaques et techniques connues qui sont souvent utilisées pour élever les privilèges, par exemple :

- **Code malveillant exploitant une faille de sécurité MS14-068 (faux PAC)**<br>
Les faux PAC sont des attaques au cours desquelles l’attaquant intègre des données d’autorisation à un ticket TGT valide sous la forme d’un en-tête d’autorisation falsifié, obtenant ainsi des autorisations supplémentaires qui ne lui ont pas été accordées par l’entreprise. Dans ce scénario, l’attaquant exploite des informations d’identification précédemment compromises ou récoltées au cours d’opérations de mouvement latéral.
- **Code malveillant exploitant une faille de sécurité MS11-013 (Silver PAC)**<br>
Les attaques exploitant une faille de sécurité MS11-013 indiquent une vulnérabilité avec élévation de privilèges dans Kerberos, pouvant entraîner la falsification de certains aspects d’un ticket de service Kerberos. Si un utilisateur malveillant ou un attaquant parvient à exploiter cette vulnérabilité, il peut obtenir un jeton avec des privilèges élevés sur le contrôleur de domaine. Dans ce scénario, l’attaquant exploite des informations d’identification précédemment compromises ou récoltées au cours d’opérations de mouvement latéral.

### Contrôle du domaine
ATA détecte les attaques en cours ou réussies de domination et de prise de contrôle total de l’environnement de la victime en repérant des techniques connues utilisées par les pirates, notamment :

- **Programme malveillant Skeleton Key**<br>
Dans les attaques de type Skeleton Key, un programme malveillant est installé sur votre contrôleur de domaine afin de permettre aux attaquants de s’authentifier comme n’importe quel utilisateur, tout en permettant aux utilisateurs légitimes d’ouvrir une session.
- **Golden Ticket**<br>
Dans les attaques par Golden Ticket, un attaquant vole des informations d’identification d’un KBTGT, le Golden Ticket Kerberos. Ce ticket permet à l’attaquant de créer un ticket TGT hors connexion et de l’utiliser pour accéder aux ressources du réseau.
- **Exécution à distance**<br>
Les attaquants peuvent tenter de contrôler votre réseau en exécutant du code à distance sur votre contrôleur de domaine.
-   **Demandes de réplication malveillantes** Dans les environnements Active Directory (AD), la réplication se produit régulièrement entre contrôleurs de domaine. Un attaquant peut usurper une demande de réplication AD (parfois en empruntant l’identité d’un contrôleur de domaine), ce qui lui permet de récupérer les données stockées dans AD, notamment les codes de hachage de mot de passe, sans utiliser des techniques plus contraignantes telles que les clichés instantanés de volume.

## Étapes suivantes

-   Pour plus d’informations sur la façon dont ATA s’intègre à votre réseau, consultez [Architecture ATA](/advanced-threat-analytics/plan-design/ata-architecture).

-   Pour commencer le déploiement d’ATA, consultez [Installer ATA](/advanced-threat-analytics/deploy-use/install-ata).

## Voir aussi
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


