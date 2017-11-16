---
title: "Guide ATA des activités suspectes | Microsoft Docs"
d|Description: This article provides a list of the suspicious activities ATA can detect and steps for remediation.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1fe5fd6f-1b79-4a25-8051-2f94ff6c71c1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: bff477a66b837d82bb10a43a0dad7d36c6542d9f
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/07/2017
---
*S’applique à : Advanced Threat Analytics version 1.8*


# <a name="advanced-threat-analytics-suspicious-activity-guide"></a>Guide ATA (Advanced Threat Analytics) des activités suspectes

Après avoir examiné une activité suspecte, vous pouvez la classer comme :

-   **Vrai positif** : action malveillante détectée par ATA.

-   **Vrai positif sans gravité** : action détectée par ATA qui est réelle, mais pas malveillante, comme un test de pénétration.

-   **Faux positif** : fausse alerte. L’activité n’a pas eu lieu.

Pour plus d’informations sur la gestion des alertes ATA, consultez [Gestion des activités suspectes](working-with-suspicious-activities.md).

Si vous avez des questions ou des commentaires à ce sujet, contactez l'équipe ATA à l’adresse [ATAEval@microsoft.com](mailto:ATAEval@microsoft.com).

## <a name="abnormal-sensitive-group-modification"></a>Modification anormale de groupes sensibles


**Description**

Des attaquants ajoutent des utilisateurs à des groupes avec des privilèges élevés. Leur but est d’accéder à davantage de ressources et d’obtenir un accès persistant. La détection s’appuie sur le profilage des activités de modification des utilisateurs d’un groupe et déclenche une alerte quand un ajout anormal à un groupe sensible est observé. ATA effectue le profilage en continu. La période minimale avant le déclenchement d’une alerte est d’un mois pour chaque contrôleur de domaine.

Pour avoir une définition des groupes sensibles dans ATA, consultez [Utilisation de la console ATA](working-with-ata-console.md#sensitive-groups).


La détection s’appuie sur les [événements audités sur les contrôleurs de domaine](https://docs.microsoft.com/advanced-threat-analytics/configure-event-collection).
Pour vérifier que vos contrôleurs de domaine auditent les événements souhaités, utilisez l’outil indiqué dans le blog [ATA Auditing (AuditPol, Advanced Audit Settings Enforcement, Lightweight Gateway Service discovery)](https://aka.ms/ataauditingblog).

**Examen**

1. La modification du groupe est-elle légitime ? </br>Une modification de groupe légitime qui est peu fréquente ou qui n’a pas été classée comme « normale » pendant l’apprentissage peut déclencher une alerte. Considérez cette alerte comme un vrai positif sans gravité.

2. Si l’objet ajouté est un compte d’utilisateur, déterminez les actions que ce compte a effectuées après son ajout au groupe d’administration. Consultez la page de l’utilisateur dans ATA pour obtenir plus de contexte. D’autres activités suspectes associées au compte ont-elles été effectuées avant ou après l’ajout ? Téléchargez le rapport **Modifications des groupes sensibles** pour examiner toutes les autres modifications effectuées au cours de la même période et déterminer les auteurs de ces modifications.

**Correction**

Réduisez le nombre d’utilisateurs autorisés à modifier les groupes sensibles.

Installez [Privileged Access Management pour les services de domaine Active Directory](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services), si cela est approprié.

## <a name="broken-trust-between-computers-and-domain"></a>Relation de confiance rompue entre les ordinateurs et le domaine

**Description**

Une relation de confiance rompue signifie que les exigences de sécurité des services de domaine Active Directory ne sont pas respectées pour les ordinateurs concernés. Cela est souvent considéré comme un échec de référence en matière de sécurité et de conformité, et une cible facile pour les attaquants. Cette détection déclenche une alerte si plus de cinq échecs d’authentification Kerberos ont été observés pour le même compte d’ordinateur sur une période de 24 heures.

**Examen**

L’ordinateur en question permet-il aux utilisateurs du domaine de se connecter ? 
- Si c’est le cas, vous pouvez ignorer cet ordinateur dans la procédure de correction.

**Correction**

Rejoignez la machine au domaine, si nécessaire, ou réinitialisez le mot de passe de la machine.

## <a name="brute-force-attack-using-ldap-simple-bind"></a>Attaque par force brute par le biais d’une liaison simple LDAP

**Description**

>[!NOTE]
> La principale différence entre les **échecs d’authentification suspects** et cette détection est que celle-ci permet à ATA de déterminer si des mots de passe différents ont été utilisés.

Dans une attaque par force brute, un attaquant tente de s’authentifier en essayant plusieurs mots de passe pour différents comptes jusqu’à ce qu’il trouve le bon mot de passe de l’un des comptes. Une fois qu’il a deviné le mot de passe d’un compte, l’attaquant utilise ce compte pour se connecter au réseau.

Cette détection déclenche une alerte si ATA détecte que plusieurs mots de passe différents ont été utilisés. L’attaque peut être *horizontale* avec un petit nombre de mots de passe possibles pour de nombreux utilisateurs, *verticale* avec un grand nombre de mots de passe pour seulement quelques utilisateurs, ou à la fois horizontale et verticale.

**Examen**

1. Si de nombreux comptes sont concernés, cliquez sur **Télécharger les détails** pour afficher la liste complète dans une feuille de calcul Excel.

2. Cliquez sur l’alerte pour accéder à la page associée. Déterminez si des tentatives de connexion ont donné lieu à une authentification. Les tentatives s’affichent en tant que **Comptes devinés** à droite des données graphiques. Si des comptes devinés sont affichés, font-ils partie des **comptes devinés** normalement utilisés à partir de l’ordinateur source ? Si c’est le cas, **supprimez** l’activité suspecte.

3. S’il n’y a pas de **comptes devinés** affichés, s’agit-il de **comptes attaqués** normalement utilisés à partir de l’ordinateur source ? Si c’est le cas, **supprimez** l’activité suspecte.

**Correction**

Les [mots de passe longs et complexes](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) assurent le niveau minimum de sécurité nécessaire contre les attaques par force brute.

## <a name="encryption-downgrade-activity"></a>Passage à une version antérieure du chiffrement

**Description**

Plusieurs méthodes d’attaque exploitent les codes faibles de chiffrement Kerberos. Dans cette détection, ATA apprend les types de chiffrement Kerberos utilisés par les ordinateurs et les utilisateurs, et déclenche des alertes quand un code de chiffrement plus faible utilisé : (1) est inhabituel pour l’ordinateur source et/ou l’utilisateur ; et (2) correspond à une technique d’attaque connue.

Il existe trois types de détection :

1.  Skeleton Key. Ce programme malveillant s’exécute sur les contrôleurs de domaine et autorise l’authentification sur le domaine de n’importe quel compte sans connaître son mot de passe. Il utilise souvent des algorithmes de chiffrement plus faibles pour chiffrer les mots de passe de l’utilisateur sur le contrôleur de domaine. Cette détection a déterminé que la méthode de chiffrement du message KRB_ERR reçu de l’ordinateur source a été passée à une version antérieure par rapport au comportement appris.

2.  Golden Ticket. Dans une alerte [Golden Ticket](#golden-ticket), la méthode de chiffrement du champ TGT du message TGS_REQ (demande de service) reçu de l’ordinateur source a été passée à une version antérieure par rapport au comportement appris. Cette détection n’est pas basée sur une anomalie de temps (contrairement à l’autre détection Golden Ticket). De plus, ATA n’a pas détecté de demande d’authentification Kerberos associée à la demande de service précédente.

3.  Overpass-the-Hash. Le type de chiffrement du message AS_REQ reçu de l’ordinateur source a été passé à une version antérieure par rapport au comportement appris (l’ordinateur utilisait l’algorithme AES).

**Examen**

Lisez d’abord la description de l’alerte pour déterminer de quel type de détection il s’agit entre les trois types de détection ci-dessus.

1.  Skeleton Key : déterminez si Skeleton Key a affecté vos contrôleurs de domaine à l’aide de [l’analyseur écrit par l’équipe ATA](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73).
    Si l’analyseur détecte la présence d’un logiciel malveillant sur un ou plusieurs de vos contrôleurs de domaine, l’alerte est un vrai positif.

2.  Golden Ticket : il peut arriver qu’une application personnalisée rarement utilisée s’authentifie à l’aide d’un code de chiffrement plus faible. Déterminez si de telles applications personnalisées sont installées sur l’ordinateur source. Si c’est le cas, l’alerte est probablement un vrai positif sans gravité et peut être supprimée.

3.  Overpass-the-Hash : dans certains cas, cette alerte est déclenchée quand une connexion interactive par carte à puce est configurée pour des comptes d’utilisateur, et que ce paramètre est désactivé, puis activé. Vérifiez si des changements de ce type ont été apportés pour les comptes concernés. Si c’est le cas, l’alerte est probablement un vrai positif sans gravité et peut être supprimée.

**Correction**

1.  Skeleton Key : supprimez le logiciel malveillant. Pour plus d’informations, consultez l’article [Skeleton Key Malware Analysis](https://www.secureworks.com/research/skeleton-key-malware-analysis) sur le site SecureWorks.

2.  Golden Ticket : suivez les instructions pour les activités suspectes [Golden Ticket](#golden-ticket).   
    De plus, du fait que la création d’un Golden Ticket nécessite des droits d’administrateur de domaine, suivez les [recommandations pour Pass-the-Hash](http://aka.ms/PtH).

3.  Overpass-the-Hash : si le compte concerné n’est pas un compte sensible, réinitialisez son mot de passe. Cela empêche l’attaquant de créer d’autres tickets Kerberos à partir du hachage de mot de passe. Toutefois, les tickets existants resteront utilisables jusqu’à leur expiration. S’il s’agit d’un compte sensible, réinitialisez deux fois le compte KRBTGT comme dans l’activité suspecte Golden Ticket. Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. Nous vous recommandons donc de planifier cette opération. Consultez les conseils fournis dans l’article [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients). Utilisez également [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Dans la mesure où il s’agit d’une technique de mouvement latéral, suivez les bonnes pratiques indiquées dans [Recommandations pour Pass-the-Hash](http://aka.ms/PtH).

## Golden Ticket<a name="golden-ticket"></a>

**Description**

Les attaquants ayant des droits d’administrateur de domaine peuvent compromettre le [compte KRBTGT](https://technet.microsoft.com/library/dn745899(v=ws.11).aspx#Sec_KRBTGT). Ils utilisent ensuite ce compte KRBTGT pour créer un ticket TGT (Ticket Granting Ticket) Kerberos qui fournit une autorisation d’accès à toutes les ressources du réseau, et définir l’heure d’expiration du ticket à la valeur de leur choix. Ce faux ticket TGT appelé « Golden Ticket » permet aux attaquants d’obtenir un accès persistant dans le réseau.

Cette détection déclenche une alerte quand un ticket TGT Kerberos est utilisé depuis plus longtemps que la durée autorisée définie dans la stratégie de sécurité [Durée de vie maximale du ticket utilisateur](https://technet.microsoft.com/library/jj852169(v=ws.11).aspx).

**Examen**

1. Le paramètre **Durée de vie maximale du ticket utilisateur** défini dans la stratégie de sécurité a-t-il été modifié récemment (au cours des dernières heures) ? Si c’est le cas, **fermez** l’alerte, car il s’agit d’un faux positif.

2. La passerelle ATA impliquée dans cette alerte est-elle une machine virtuelle ? Si c’est le cas, son exécution a-t-elle repris à partir d’un état de mise en mémoire ? Si c’est le cas, **fermez** l’alerte.

3. Si vous avez répondu non aux deux questions ci-dessus, considérez l’alerte comme une attaque malveillante.

**Correction**

Changez deux fois le mot de passe du compte KRBTGT en suivant les conseils de l’article [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et en utilisant [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. Nous vous recommandons donc de planifier cette opération.  
De plus, du fait que la création d’un Golden Ticket nécessite des droits d’administrateur de domaine, suivez les [recommandations pour Pass-the-Hash](http://aka.ms/PtH).

## <a name="honeytoken-activity"></a>Activité Honeytoken


**Description**

Les comptes Honeytoken sont des comptes servant de leurre pour identifier et suivre l’activité malveillante qui implique ces comptes. Les comptes Honeytoken doivent rester inutilisés, et avoir un nom évocateur pour attirer et leurrer les attaquants (par exemple, SQL-Admin). Toute activité observée sur ces comptes peut être le signe d’un comportement malveillant.

Pour plus d’informations sur les comptes Honeytoken, consultez [Installer ATA - Étape 7](install-ata-step7.md).

**Examen**

1.  Vérifiez si le propriétaire de l’ordinateur source a utilisé le compte Honeytoken pour s’authentifier, à l’aide de la méthode décrite dans la page de l’activité suspecte (par exemple, Kerberos, LDAP, NTLM).

2.  Accédez à la page du profil de chaque ordinateur source et vérifiez si d’autres comptes se sont authentifiés à partir de ces ordinateurs. Vérifiez auprès des propriétaires de ces comptes s’ils ont utilisé le compte Honeytoken.

3.  Il peut s’agir d’une connexion non interactive. Vous devez donc vérifier si des applications ou des scripts s’exécutent sur les ordinateurs sources.

Si, après avoir effectué les étapes 1 à 3, vous ne pouvez pas déterminer avec certitude que l’attaque est sans gravité, considérez qu’il s’agit d’une attaque malveillante.

**Correction**

Assurez-vous que les comptes Honeytoken sont utilisés uniquement pour leur rôle prévu afin d’éviter la génération de nombreuses alertes.

## <a name="identity-theft-using-pass-the-hash-attack"></a>Usurpation d’identité par attaque Pass-the-Hash

**Description**

Pass-the-Hash est une technique de mouvement latéral par laquelle les attaquants volent le code de hachage NTLM d’un utilisateur sur un ordinateur et utilisent ensuite ce code pour accéder à un autre ordinateur. 

**Examen**

Le code de hachage volé d’un ordinateur est-il détenu ou régulièrement utilisé par l’utilisateur ciblé ? Si c’est le cas, il s’agit d’un faux positif. Si ce n’est pas le cas, il s’agit probablement d’un vrai positif.

**Correction**

1. Si le compte concerné n’est pas un compte sensible, réinitialisez le mot de passe de ce compte. Cela empêche l’attaquant de créer d’autres tickets Kerberos à partir du hachage de mot de passe. Toutefois, les tickets existants resteront utilisables jusqu’à leur expiration. 

2. S’il s’agit d’un compte sensible, réinitialisez deux fois le compte KRBTGT comme dans l’activité suspecte Golden Ticket. Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. Nous vous recommandons donc de planifier cette opération. Consultez les conseils fournis dans l’article [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et utilisez [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Dans la mesure où il s’agit d’une technique de mouvement latéral, suivez les bonnes pratiques indiquées dans [Recommandations pour Pass-the-Hash](http://aka.ms/PtH).

## <a name="identity-theft-using-pass-the-ticket-attack"></a>Usurpation d’identité par attaque Pass-the-Ticket

**Description**

Pass-the-Ticket est une technique de mouvement latéral par laquelle les attaquants volent un ticket Kerberos sur un ordinateur et réutilisent ensuite ce ticket pour accéder à un autre ordinateur. Cette détection vérifie si un ticket Kerberos a été utilisé sur plusieurs ordinateurs différents.

**Examen**

1. Cliquez sur le bouton **Télécharger les détails** pour afficher la liste complète des adresses IP impliquées. L’adresse IP de l’un ou des deux ordinateurs appartient-elle à un sous-réseau alloué à partir d’un pool DHCP de taille insuffisante, par exemple, VPN ou WiFi ? L’adresse IP est-elle partagée ? Par exemple, par un appareil NAT ? Si vous répondez par l’affirmative à l’une de ces questions, il s’agit d’un faux positif.

2. Y a-t-il une application personnalisée qui transfère les tickets pour le compte d’utilisateurs ? Si c’est le cas, il s’agit d’un vrai positif.

**Correction**

1. Si le compte concerné n’est pas un compte sensible, réinitialisez le mot de passe de ce compte. Cela empêche l’attaquant de créer d’autres tickets Kerberos à partir du hachage de mot de passe. Toutefois, les tickets existants resteront utilisables jusqu’à leur expiration.  

2. S’il s’agit d’un compte sensible, réinitialisez deux fois le compte KRBTGT comme dans l’activité suspecte Golden Ticket. Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. Nous vous recommandons donc de planifier cette opération. Consultez les conseils fournis dans l’article [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et utilisez [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).  Dans la mesure où il s’agit d’une technique de mouvement latéral, suivez les bonnes pratiques indiquées dans [Recommandations pour Pass-the-Hash](http://aka.ms/PtH).

## <a name="malicious-data-protection-private-information-request"></a>Demande d’information privée de protection contre les données malveillantes

**Description**

L’API de protection des données (DPAPI) est utilisée par Windows pour protéger les mots de passe enregistrés par les navigateurs, les clés de chiffrement et d’autres données sensibles. Les contrôleurs de domaine détiennent une clé principale de sauvegarde qui peut être utilisée pour déchiffrer tous les secrets chiffrés avec DPAPI sur des machines Windows jointes au domaine. Des attaquants peuvent utiliser cette clé principale pour déchiffrer les secrets protégés avec DPAPI sur toutes les machines jointes au domaine.
Cette détection déclenche une alerte quand DPAPI est utilisé pour récupérer la clé principale de sauvegarde.

**Examen**

1. L’ordinateur source exécute-t-il un scanner de sécurité approuvé par l’organisation dans Active Directory ?

2. Si c’est le cas et si ce comportement est normal, **fermez et excluez** l’activité suspecte.

3. Si c’est le cas, mais que ce comportement n’est pas normal, **fermez** l’activité suspecte.

**Correction**

Pour pouvoir utiliser DPAPI, un attaquant doit avoir les droits d’administrateur de domaine. Suivez les [recommandations pour Pass-the-Hash](http://aka.ms/PtH).

## <a name="malicious-replication-requests"></a>Demandes de réplication malveillantes


**Description**

La réplication Active Directory est le processus par lequel les modifications apportées à un contrôleur de domaine sont synchronisées avec tous les autres contrôleurs de domaine. Quand les attaquants ont les autorisations nécessaires, ils peuvent lancer une demande de réplication dans le but de récupérer ensuite les données stockées dans Active Directory, y compris les hachages de mot de passe.

Dans cette détection, une alerte est déclenchée quand une demande de réplication est lancée à partir d’un ordinateur qui n’est pas un contrôleur de domaine.

**Examen**

1. L’ordinateur en question est-il un contrôleur de domaine ? Par exemple, un contrôleur de domaine récemment promu ayant rencontré des problèmes de réplication. Si c’est le cas, **fermez et excluez** l’activité suspecte.  

2. L’ordinateur en question est-il supposé répliquer des données à partir d’Active Directory ? Par exemple, Azure AD Connect. Si c’est le cas, **fermez et excluez** l’activité suspecte.

**Correction**

Vérifiez les autorisations suivantes : 

- Répliquer les changements d’annuaire   

- Répliquer tous les changements d’annuaire  

Pour plus d’informations, consultez [Accorder des autorisations Active Directory Domain Services pour la synchronisation de profils dans SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).
Vous pouvez utiliser [l’analyseur AD ACL](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) ou créer un script Windows PowerShell pour déterminer qui a ces autorisations dans le domaine.

## <a name="massive-object-deletion"></a>Suppression massive d’objets

**Description**

Dans certains scénarios, les attaquants effectuent une attaque par déni de service (DoS) au lieu de simplement voler des informations. La suppression d’un grand nombre de comptes est une technique d’attaque DoS.

Dans cette détection, une alerte est déclenchée quand plus de 5 % de l’ensemble des comptes sont supprimés. La détection nécessite un accès en lecture sur le conteneur d’objets supprimés.  
Pour plus d’informations sur la configuration des autorisations en lecture seule sur le conteneur d’objets supprimés, consultez la section **Changing permissions on a deleted object container** (Modifier les autorisations sur un conteneur d’objets supprimés) dans [View or Set Permissions on a Directory Object](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) (Afficher ou définir des autorisations sur un objet répertoire).

**Examen**

Passez en revue la liste des comptes supprimés et déterminez si un modèle ou un motif particulier justifie cette suppression massive.

**Correction**

Supprimez les autorisations des utilisateurs qui peuvent supprimer des comptes dans Active Directory. Pour plus d’informations, consultez [View or Set Permissions on a Directory Object](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) (Afficher ou définir des autorisations sur un objet répertoire).

## <a name="privilege-escalation-using-forged-authorization-data"></a>Réaffectation de privilèges à l’aide de données d’autorisation falsifiées

**Description**

Des vulnérabilités connues dans les versions antérieures de Windows Server permettent aux attaquants d’obtenir des privilèges supplémentaires par le biais du certificat PAC (Privileged Attribute Certificate), un champ dans le ticket Kerberos qui contient les données d’autorisation de l’utilisateur (dans Active Directory, il s’agit de l’appartenance au groupe).

**Examen**

1. Cliquez sur l’alerte pour accéder à la page de détails correspondante.

2. Le correctif MS14-068 (contrôleur de domaine) ou MS11-013 (serveur) a-t-il été installé sur l’ordinateur de destination (sous la colonne **ACCESSED**) ? Si c’est le cas, **fermez** l’activité suspecte (c’est un faux positif).

3. Sinon, l’ordinateur source s’exécute (sous la colonne **FROM**) exécute-t-il un système d’exploitation ou une application connu pour modifier le certificat PAC ? Si c’est le cas, **supprimez** l’activité suspecte (c’est un vrai positif sans gravité).

4. Si vous avez répondu non aux deux questions ci-dessus, considérez l’alerte comme une attaque malveillante.

**Correction**

Vérifiez que tous les contrôleurs de domaine avec une version de système d’exploitation antérieure ou égale à Windows Server 2012 R2 sont installés avec [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege) et que tous les serveurs et contrôleurs de domaine membres avec une version antérieure ou égale à 2012 R2 sont à jour avec KB2496930. Pour plus d’informations, consultez [Silver PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) et [faux PAC](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="reconnaissance-using-directory-services-queries"></a>Reconnaissance à l’aide de requêtes de services d’annuaire

**Description**

La reconnaissance des services d’annuaire permet aux attaquants de mapper la structure d’annuaire et de cibler des comptes privilégiés pour les étapes suivantes d’une attaque. Le protocole SAM-R (Security Account Manager Remote) est l’une des méthodes utilisées pour interroger l’annuaire et effectuer ce type de mappage.

Dans cette détection, aucune alerte n’est déclenchée durant le premier mois après le déploiement d’ATA. Pendant cette période d’apprentissage, ATA effectue un profilage des requêtes SAM-R effectuées à partir des ordinateurs, qu’il s’agisse de requêtes d’énumération ou de requêtes individuelles sur des comptes sensibles.

**Examen**

1. Cliquez sur l’alerte pour accéder à la page de détails correspondante. Examinez quels types de requêtes ont été effectuées (par exemple, des requêtes Administrateur entreprise ou Administrateur) et si elles ont réussi ou échoué.

2. Des requêtes de ce type sont-elles censées être effectuées à partir de l’ordinateur source en question ?

3. Si c’est le cas et que l’alerte a été mise à jour, **supprimez** l’activité suspecte.

4. Si c’est le cas, mais que cela ne devrait plus se produire, **fermez** l’activité suspecte.

5. Si vous avez des informations sur le compte impliqué : de telles requêtes sont-elles censées être effectuées par ce compte ou ce compte se connecte-t-il normalement à l’ordinateur source ?

 - Si c’est le cas et que l’alerte a été mise à jour, **supprimez** l’activité suspecte.

 - Si c’est le cas, mais que cela ne devrait plus se produire, **fermez** l’activité suspecte.

 - Si vous avez répondu non à toutes les questions ci-dessus, considérez l’alerte comme une attaque malveillante.

**Correction**

Utilisez [l’outil SAMRi10](https://gallery.technet.microsoft.com/SAMRi10-Hardening-Remote-48d94b5b) pour mieux protéger votre environnement contre cette technique d’attaque.

## <a name="reconnaissance-using-dns"></a>Reconnaissance à l’aide de DNS

**Description**

Votre serveur DNS contient une carte de l’ensemble des ordinateurs, adresses IP et services de votre réseau. Ces informations sont utilisées par les attaquants pour mapper la structure de votre réseau et cibler les ordinateurs intéressants pour les étapes suivantes de l’attaque.

Il existe plusieurs types de requêtes dans le protocole DNS. ATA détecte les demandes de transfert AXFR qui ne proviennent pas de serveurs DNS.

**Examen**

1. La machine source (**En provenance de…**) est-elle un serveur DNS ? Si c’est le cas, il s’agit probablement d’un faux positif. Pour le vérifier, cliquez sur l’alerte pour accéder à la page de détails correspondante. Dans le tableau, sous **Requête**, vérifiez quels domaines ont été interrogés. S’agit-il de domaines existants ? Si c’est le cas, **fermez** l’activité suspecte (c’est un faux positif). De plus, assurez-vous que le port UDP 53 est ouvert entre les passerelles ATA et l’ordinateur source pour éviter les futurs faux positifs.

2. L’ordinateur source exécute-t-il un scanner de sécurité ? Si c’est le cas, **excluez les entités** dans ATA, soit directement en choisissant **Fermer et exclure**, soit via la page **Exclusion**, sous **Configuration** (disponible pour les administrateurs d’ATA).

3. Si vous avez répondu non à toutes les questions ci-dessus, considérez l’alerte comme une attaque malveillante.

**Correction**

La sécurisation d’un serveur DNS interne pour éviter la reconnaissance à l’aide de DNS est possible en désactivant les transferts de zone ou en les limitant uniquement aux adresses IP spécifiées. Pour plus d’informations sur la limitation des transferts de zone, consultez [Restrict Zone Transfers](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx) (Limiter les transferts de zone).
La modification des transferts de zone est l’une des tâches de la liste de contrôle que vous devez suivre pour [sécuriser vos serveurs DNS contre les attaques internes et externes](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx).

## <a name="reconnaissance-using-smb-session-enumeration"></a>Reconnaissance à l’aide de l’énumération de sessions SMB


**Description**

L’énumération SMB (Server Message Block) permet aux attaquants d’obtenir des informations sur les emplacements de connexion récents des utilisateurs. Une fois qu’ils connaissent ces informations, les attaquants peuvent se déplacer de façon latérale dans le réseau pour accéder à un compte sensible spécifique.

Dans cette détection, une alerte est déclenchée quand une énumération de sessions SMB est effectuée sur un contrôleur de domaine, ce qui ne doit pas se produire normalement.

**Examen**

1. Cliquez sur l’alerte pour accéder à la page de détails correspondante. Déterminez quels comptes ont effectué l’opération et quels comptes ont été exposés, le cas échéant.

 - L’ordinateur source exécute-t-il un scanner de sécurité ? Si c’est le cas, **fermez et excluez** l’activité suspecte.

2. Déterminez quels utilisateurs ont effectué l’opération. Sont-ils des utilisateurs qui se connectent normalement à l’ordinateur source ou des administrateurs autorisés à effectuer des actions de ce type ?  

3. Si c’est le cas et que l’alerte a été mise à jour, **supprimez** l’activité suspecte.  

4. Si c’est le cas, mais que cela ne devrait plus se produire, **fermez** l’activité suspecte.

5. Si vous avez répondu non à toutes les questions ci-dessus, considérez l’alerte comme une attaque malveillante.

**Correction**

Utilisez [l’outil Net Cease](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) pour renforcer la protection de votre environnement contre cette attaque.

## <a name="remote-execution-attempt-detected"></a>Tentative d’exécution à distance détectée

**Description**

Les attaquants qui compromettent les informations d’identification d’administration ou qui exploitent une faille de sécurité de type zero-day peuvent exécuter des commandes à distance sur votre contrôleur de domaine. Cela peut servir pour obtenir une persistance, collecter des informations, lancer des attaques par déni de service (DOS) ou toute autre raison. ATA détecte les connexions PSexec et les connexions WMI à distance.

**Examen**

1. Cette situation est fréquente pour les stations de travail d’administration, les membres des équipes informatiques et les comptes de service qui effectuent des tâches d’administration sur les contrôleurs de domaine. Si c’est le cas et que l’alerte a été mise à jour du fait qu’elle est effectuée par le même administrateur et/ou ordinateur, **supprimez** l’alerte.

2. **L’ordinateur** en question est-il autorisé à effectuer cette exécution à distance sur votre contrôleur de domaine ?

 - **Le compte** en question est-il autorisé à effectuer cette exécution à distance sur votre contrôleur de domaine ?

 - Si la réponse à ces deux questions est *oui*, **fermez** l’alerte.

3. Si la réponse à l’une de ces questions est *non*, considérez l’attaque comme un vrai positif.

**Correction**

1. Limitez l’accès à distance aux contrôleurs de domaine à partir d’ordinateurs qui ne sont pas de niveau 0.

2. Implémentez un [accès privilégié](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access) pour autoriser uniquement les machines avec une sécurité renforcée à se connecter aux contrôleurs de domaine pour les administrateurs.

## <a name="sensitive-account-credentials-exposed--services-exposing-account-credentials"></a>Informations d’identification de compte sensible exposées et services qui exposent des informations d’identification de compte

**Description**

Certains services envoient des informations d’identification de compte au format texte brut, y compris pour des comptes sensibles. Les attaquants qui surveillent le trafic réseau peuvent intercepter ces informations d’identification et les réutiliser à des fins malveillantes. L’alerte est déclenchée dès qu’un mot de passe en texte clair est envoyé pour un compte sensible. Pour les comptes non sensibles, elle est déclenchée si les mots de passe en texte clair pour au moins cinq comptes différents sont envoyés à partir de l’ordinateur source. 

**Examen**

Cliquez sur l’alerte pour accéder à la page de détails correspondante. Déterminez quels comptes ont été exposés. Si de nombreux comptes sont concernés, cliquez sur **Télécharger les détails** pour afficher la liste complète dans une feuille de calcul Excel.

En général, il y a une application de script ou héritée sur les ordinateurs sources qui utilise une liaison simple LDAP.

**Correction**

Vérifiez la configuration des ordinateurs sources et que vous n’utilisez pas de liaison simple LDAP. À la place des liaisons simples LDAP, utilisez des liaisons SALS LDAP ou LDAPS.

## <a name="suspicious-authentication-failures"></a>Échecs d’authentification suspects

**Description**

Dans une attaque par force brute, un attaquant tente de s’authentifier en essayant plusieurs mots de passe pour différents comptes jusqu’à ce qu’il trouve le bon mot de passe de l’un des comptes. Une fois qu’il a deviné le mot de passe d’un compte, l’attaquant utilise ce compte pour se connecter au réseau.

Dans cette détection, une alerte est déclenchée après l’échec de nombreuses tentatives d’authentification. L’attaque peut être horizontale avec un petit nombre de mots de passe possibles pour de nombreux utilisateurs, verticale avec un grand nombre de mots de passe pour seulement quelques utilisateurs, ou à la fois horizontale et verticale.

**Examen**

1. Si de nombreux comptes sont concernés, cliquez sur **Télécharger les détails** pour afficher la liste complète dans une feuille de calcul Excel.

2. Cliquez sur l’alerte pour accéder à la page de détails correspondante. Déterminez si des tentatives de connexion ont donné lieu à une authentification. Les tentatives s’affichent en tant que **Comptes devinés** à droite des données graphiques. Si des comptes devinés sont affichés, font-ils partie des **comptes devinés** normalement utilisés à partir de l’ordinateur source ? Si c’est le cas, **supprimez** l’activité suspecte.

3. S’il n’y a pas de **comptes devinés** affichés, s’agit-il de **comptes attaqués** normalement utilisés à partir de l’ordinateur source ? Si c’est le cas, **supprimez** l’activité suspecte.

**Correction**

Les [mots de passe longs et complexes](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) assurent le niveau minimum de sécurité nécessaire contre les attaques par force brute.

## <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>Suspicion d’usurpation d’identité basée sur un comportement inhabituel

**Description**

ATA apprend le comportement de l’entité pour les utilisateurs, les ordinateurs et les ressources sur une période glissante de trois semaines. Le modèle de comportement est basé sur les activités suivantes : les machines auxquelles les entités se sont connectées, les ressources pour lesquelles l’entité a demandé l’accès et la durée de ces opérations. ATA déclenche une alerte quand il y a un écart entre le comportement de l’entité et les algorithmes d’apprentissage de la machine. 

**Examen**

1. L’utilisateur en question est-il supposé effectuer ces opérations normalement ?

2. Considérez les cas suivants comme des faux positifs potentiels : un utilisateur qui rentre de vacances, un membre du service informatique qui a besoin d’accéder à plus de ressources qu’habituellement (par exemple, pour répondre à toutes les demandes de support technique durant un jour ou une semaine donné) et les applications de bureau à distance. Si vous **fermez et excluez** l’alerte, l’utilisateur ne sera plus inclus dans la détection.


**Correction**

En fonction de la cause de ce comportement anormal, vous devez effectuer des actions différentes. Par exemple, si cela est dû à l’analyse du réseau, empêchez la machine source d’accéder au réseau (sauf si elle est approuvée).

## <a name="unusual-protocol-implementation"></a>Implémentation de protocole inhabituelle


**Description**

Les attaquants utilisent des outils qui implémentent différents protocoles (SMB, Kerberos, NTLM) de façon inhabituelle. Ce type de trafic réseau est admis par Windows sans avertissement, mais ATA est capable de reconnaître une activité malveillante potentielle. Le comportement est révélateur de certaines techniques comme l’attaque par force brute ou Over-Pass-the-Hash, ou de l’exploitation des failles de sécurité par de puissants ransomware tels que WannaCry.

**Examen**

Identifiez le protocole inhabituel, à partir de la chronologie des activités suspectes, et cliquez sur l’activité suspecte pour accéder à la page de détails correspondante. Le protocole s’affiche au-dessus de la flèche : Kerberos ou NTLM.

- **Kerberos** : une alerte est souvent déclenchée si un outil de piratage comme Mimikatz a été utilisé dans le cadre d’une attaque potentielle de type Overpass-the-Hash. Vérifiez si l’ordinateur source exécute une application qui implémente sa propre pile Kerberos, de manière non conforme à la RFC Kerberos. Si c’est le cas, il s’agit d’un vrai positif sans gravité. Vous pouvez **fermer** l’alerte. Si l’alerte continue d’être déclenchée et que c’est toujours le cas, **supprimez** l’alerte.

- **NTLM** : une alerte peut être déclenchée si WannaCry ou un outil comme Metasploit, Medusa ou Hydra est utilisé.  

Pour déterminer s’il s’agit d’une attaque WannaCry, effectuez les étapes suivantes :

1. Vérifiez si l’ordinateur source exécute un outil d’attaque tel que Metasploit, Medusa ou Hydra.

2. Si vous ne trouvez aucun outil d’attaque, vérifiez si l’ordinateur source exécute une application qui implémente sa propre pile NTLM ou SMB.

3. Si ce n’est pas le cas, vérifiez si l’alerte est causée par WannaCry, en exécutant un script de scanner WannaCry, par exemple [this scanner](https://github.com/apkjet/TrustlookWannaCryToolkit/tree/master/scanner) sur l’ordinateur source impliqué dans l’activité suspecte. Si le scanner identifie la machine comme infectée ou vulnérable, installez les correctifs appropriés sur la machine et supprimez/bloquez le programme malveillant sur le réseau.

4. Si le script ne détecte pas que la machine est infectée ou vulnérable, cela ne signifie pas qu’elle ne l’est pas. En effet, SMBv1 peut avoir été désactivé ou un correctif peut avoir été installé sur la machine, ce qui fausse l’analyse de l’outil.

**Correction**

Installez tous les correctifs logiciels nécessaires sur les machines, notamment les mises à jour de sécurité.

1. [Désactivez SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/).

2. [Supprimez WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo).

3. WanaKiwi peut déchiffrer les données interceptées par certains ransomware, mais uniquement si l’utilisateur n’a pas redémarré ou éteint l’ordinateur. Pour plus d’informations, consultez [Ransomware WannaCry](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1).

## <a name="related-videos"></a>Vidéos connexes
- [Rejoindre la communauté sur la sécurité](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)


## <a name="see-also"></a>Voir aussi
- [Scénario d’activité suspecte ATA](http://aka.ms/ataplaybook)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Gestion des activités suspectes](working-with-suspicious-activities.md)
