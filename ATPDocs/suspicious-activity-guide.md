---
title: "Guide Azure ATP des activités suspectes | Microsoft Docs"
d|Description: This article provides a list of the suspicious activities Azure ATP can detect and steps for remediation.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ee8e45b6ef2da2d8866a1795bdab3987180acefe
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2018
---
*S’applique à : Azure - Protection avancée contre les menaces*


# <a name="azure-advanced-threat-protection-suspicious-activity-guide"></a>Guide Azure - Protection avancée contre les menaces (ATP) des activités suspectes

Après avoir examiné une activité suspecte, vous pouvez la classer comme :

-   **Vrai positif** : action malveillante détectée par Azure ATP.

-   **Vrai positif sans gravité** : action détectée par Azure ATP qui est réelle, mais pas malveillante, comme un test de pénétration.

-   **Faux positif** : fausse alerte. L’activité n’a pas eu lieu.

Pour plus d’informations sur la gestion des alertes Azure ATP, consultez [Gestion des activités suspectes](working-with-suspicious-activities.md).


## <a name="abnormal-sensitive-group-modification"></a>Modification anormale de groupes sensibles


**Description**

Des attaquants ajoutent des utilisateurs à des groupes avec des privilèges élevés. Leur but est d’accéder à davantage de ressources et d’obtenir un accès persistant. La détection s’appuie sur le profilage des activités de modification des utilisateurs d’un groupe et déclenche une alerte quand un ajout anormal à un groupe sensible est observé. ATP effectue un profilage en continu. La période minimale avant le déclenchement d’une alerte est d’un mois pour chaque contrôleur de domaine.

Pour obtenir la définition des groupes sensibles dans Azure ATP, consultez [Gestion des comptes sensibles](sensitive-accounts.md).


La détection s’appuie sur les [événements audités sur les contrôleurs de domaine](configure-event-collection.md).
Pour vous assurer que vos contrôleurs de domaine effectuent l’audit des événements requis.

**Examen**

1. La modification du groupe est-elle légitime ? </br>Une modification de groupe légitime qui est peu fréquente ou qui n’a pas été classée comme « normale » pendant l’apprentissage peut déclencher une alerte. Considérez cette alerte comme un vrai positif sans gravité.

2. Si l’objet ajouté est un compte d’utilisateur, déterminez les actions que ce compte a effectuées après son ajout au groupe d’administration. Consultez la page de l’utilisateur dans Azure ATP pour obtenir plus de contexte. D’autres activités suspectes associées au compte ont-elles été effectuées avant ou après l’ajout ? Téléchargez le rapport **Modifications des groupes sensibles** pour examiner toutes les autres modifications effectuées au cours de la même période et déterminer les auteurs de ces modifications.

**Correction**

Réduisez le nombre d’utilisateurs autorisés à modifier les groupes sensibles.

Installez [Privileged Access Management pour les services de domaine Active Directory](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services), si cela est approprié.


## <a name="brute-force-attack-using-ldap-simple-bind"></a>Attaque par force brute par le biais d’une liaison simple LDAP

**Description**

>[!NOTE]
> La principale différence entre les **échecs d’authentification suspects** et cette détection est que celle-ci permet à Azure ATP de déterminer si des mots de passe différents ont été utilisés.

Dans une attaque par force brute, un attaquant tente de s’authentifier en essayant plusieurs mots de passe pour différents comptes jusqu’à ce qu’il trouve le bon mot de passe de l’un des comptes. Une fois qu’il a deviné le mot de passe d’un compte, l’attaquant utilise ce compte pour se connecter au réseau.

Dans cette détection, une alerte est déclenchée quand Azure ATP détecte un nombre massif d’authentifications de liaison simple. L’attaque peut être *horizontale* avec un petit nombre de mots de passe possibles pour de nombreux utilisateurs, *verticale* avec un grand nombre de mots de passe pour seulement quelques utilisateurs, ou à la fois horizontale et verticale.

**Examen**

1. Si de nombreux comptes sont concernés, cliquez sur **Télécharger les détails** pour afficher la liste complète dans une feuille de calcul Excel.

2. Cliquez sur l’alerte pour accéder à la page associée. Déterminez si des tentatives de connexion ont donné lieu à une authentification. Les tentatives s’affichent en tant que **Comptes devinés** à droite des données graphiques. Si des comptes devinés sont affichés, font-ils partie des **comptes devinés** normalement utilisés à partir de l’ordinateur source ? Si c’est le cas, **supprimez** l’activité suspecte.

3. S’il n’y a pas de **comptes devinés** affichés, s’agit-il de **comptes attaqués** normalement utilisés à partir de l’ordinateur source ? Si c’est le cas, **supprimez** l’activité suspecte.

**Correction**

Les [mots de passe longs et complexes](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) assurent le niveau minimum de sécurité nécessaire contre les attaques par force brute.

## <a name="encryption-downgrade-activity"></a>Passage à une version antérieure du chiffrement

**Description**

Le passage à une version antérieure du chiffrement est une méthode visant à affaiblir Kerberos en abaissant le niveau de chiffrement de différents champs du protocole qui sont généralement chiffrés à l’aide du niveau de chiffrement le plus élevé. Un champ au chiffrement affaibli peut être plus vulnérable à des attaques de force brute en mode hors connexion. Plusieurs méthodes d’attaque exploitent les codes faibles de chiffrement Kerberos. Dans cette détection, Azure ATP examine les types de chiffrement Kerberos utilisés par les ordinateurs et les utilisateurs, et déclenche des alertes quand un chiffrement plus faible est utilisé : (1) qui est inhabituel pour l’ordinateur source et/ou l’utilisateur ; et (2) qui correspond à une technique d’attaque connue.

Il existe trois types de détection :

1.  Skeleton Key. Ce programme malveillant s’exécute sur les contrôleurs de domaine et autorise l’authentification sur le domaine de n’importe quel compte sans connaître son mot de passe. Il utilise souvent des algorithmes de chiffrement plus faibles pour hacher les mots de passe de l’utilisateur sur le contrôleur de domaine. Dans le cadre de cette détection, la méthode de chiffrement du message KRB_ERR adressé par le contrôleur de domaine au compte demandant un ticket a été abaissée par rapport au comportement appris.

2.  Golden Ticket. Dans une alerte [Golden Ticket](#golden-ticket), la méthode de chiffrement du champ TGT du message TGS_REQ (demande de service) reçu de l’ordinateur source a été passée à une version antérieure par rapport au comportement appris. Cette détection n’est pas basée sur une anomalie de temps (contrairement à l’autre détection Golden Ticket). De plus, ATP n’a pas détecté de demande d’authentification Kerberos associée à la demande de service précédente.

3.  Overpass-the-Hash. Un intrus peut utiliser un code de hachage faible dérobé pour créer un ticket fort via une demande Kerberos AS. Dans le cadre de cette détection, le type de chiffrement du message AS_REQ reçu de l’ordinateur source a été abaissé par rapport au comportement appris (l’ordinateur utilisait l’algorithme AES).

**Examen**

Lisez d’abord la description de l’alerte pour déterminer de quel type de détection il s’agit entre les trois types de détection ci-dessus.

1.  Skeleton Key : déterminez si Skeleton Key a affecté vos contrôleurs de domaine à l’aide du [scanneur écrit par l’équipe Azure ATP](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73).
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

2. Le capteur autonome Azure ATP impliqué dans cette alerte est-il une machine virtuelle ? Si c’est le cas, son exécution a-t-elle repris à partir d’un état de mise en mémoire ? Si c’est le cas, **fermez** l’alerte.

3. Si vous avez répondu non aux deux questions ci-dessus, considérez l’alerte comme une attaque malveillante.

**Correction**

Changez deux fois le mot de passe du compte KRBTGT en suivant les conseils de l’article [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Scripts de réinitialisation du mot de passe du compte KRBTGT maintenant disponibles pour les clients) et en utilisant [l’outil de réinitialisation du mot de passe/des clés du compte KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Cette double réinitialisation de KRBTGT invalide tous les tickets Kerberos dans ce domaine. Nous vous recommandons donc de planifier cette opération. De plus, du fait que la création d’un Golden Ticket nécessite des droits d’administrateur de domaine, suivez les [recommandations pour Pass-the-Hash](http://aka.ms/PtH).

## <a name="honeytoken-activity"></a>Activité Honeytoken


**Description**

Les comptes Honeytoken sont des comptes servant de leurre pour identifier et suivre l’activité malveillante qui implique ces comptes. Les comptes Honeytoken doivent rester inutilisés, et avoir un nom évocateur pour attirer et leurrer les attaquants (par exemple, SQL-Admin). Toute activité observée sur ces comptes peut être le signe d’un comportement malveillant.

Pour plus d’informations sur les comptes Honeytoken, consultez [Installer Azure ATP - Étape 7](install-atp-step7.md).

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

1. Cliquez sur le bouton **Télécharger les détails** pour afficher la liste complète des adresses IP impliquées. L’adresse IP de l’un ou des deux ordinateurs appartient-elle à un sous-réseau alloué à partir d’un pool DHCP de taille insuffisante, par exemple, VPN ou WiFi ? L’adresse IP est-elle partagée ? Par exemple, par un appareil NAT ? Une ou plusieurs des adresses IP sources sont-elles non résolues par le capteur ? (Cela peut indiquer que les ports appropriés du capteur vers les périphériques ne sont pas correctement ouverts.) Si vous répondez par l’affirmative à l’une de ces questions, il s’agit d’un faux positif.

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

## <a name="reconnaissance-using-account-enumeration"></a>Reconnaissance à l’aide de l’énumération de compte

**Description**

Lors d’une reconnaissance à l’aide de l’énumération de comptes, un attaquant utilise un dictionnaire contenant des milliers de noms d’utilisateurs ou des outils comme KrbGuess pour essayer de deviner des noms d’utilisateur de votre domaine. Il procède à des demandes Kerberos en utilisant ces noms afin de tenter de trouver un nom d’utilisateur valide dans votre domaine. Si l’attaquant parvient à deviner un nom d’utilisateur, il obtient l’erreur Kerberos **Pré-authentification requise** au lieu de **Principal de sécurité inconnu**. 

Dans le cadre de cette détection, Azure ATP peut détecter d'où provient l’attaque, le nombre total de tentatives et combien ont abouti. Si le nombre d’utilisateurs inconnus est trop élevé, Azure ATP détecte cela comme une activité suspecte. 

**Examen**

1. Cliquez sur l’alerte pour accéder à la page de détails correspondante. 

2. Cet ordinateur hôte doit-il interroger le contrôleur de domaine pour savoir si des comptes existent (par exemple, des serveurs Exchange) ? <br></br>
Est-ce qu’un script ou une application s’exécutant sur l’hôte pourrait générer ce comportement ? <br></br>
Si la réponse à l’une de ces questions est oui, **fermez** l’activité suspecte (c’est un vrai positif sans incidence) et excluez cet hôte de l’activité suspecte.

3. Téléchargez les détails de l’alerte dans une feuille de calcul Excel pour voir clairement la liste des tentatives de comptes, avec d’un côté les comptes qui existent et de l’autre ceux qui n’existent pas. Si vous examinez la feuille des comptes qui n’existent pas et que vous pensez les connaître, il s’agit peut-être de comptes désactivés ou d’employés ayant quitté l’entreprise. Dans ce cas, il est peu probable que la tentative provienne d’un dictionnaire. Il s’agit très certainement d’une application ou d’un script qui vérifie les comptes qui existent toujours dans Active Directory, c’est donc un vrai positif sans incidence.

3. Si les noms sont en grande partie inconnus, des tentatives ont-elle abouti à une correspondance à des noms de comptes existants dans Active Directory ? S’il n’y a aucune correspondance, la tentative n’a servi à rien, mais vous devez surveiller l’alerte pour voir si elle est mise à jour au fil du temps.

4. Si des tentatives correspondent à des noms de compte existants, l’attaquant connaît l’existence de comptes dans votre environnement et peut essayer d’utiliser des attaques par force brute pour accéder à votre domaine en utilisant les noms d’utilisateur découverts. Vérifiez les noms de compte trouvés en recherchant d’autres activités suspectes. Regardez si des comptes sensibles se trouvent parmi les comptes trouvés.


**Correction**

Les [mots de passe longs et complexes](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) assurent le niveau minimum de sécurité nécessaire contre les attaques par force brute.


## <a name="reconnaissance-using-directory-services-queries"></a>Reconnaissance à l’aide de requêtes de services d’annuaire

**Description**

La reconnaissance des services d’annuaire permet aux attaquants de mapper la structure d’annuaire et de cibler des comptes privilégiés pour les étapes suivantes d’une attaque. Le protocole SAM-R (Security Account Manager Remote) est l’une des méthodes utilisées pour interroger l’annuaire et effectuer ce type de mappage.

Dans le cadre de cette détection, aucune alerte n’est déclenchée durant le premier mois après le déploiement d’Azure ATP. Pendant cette période d’apprentissage, Azure ATP effectue un profilage des requêtes SAM-R effectuées à partir des ordinateurs, qu’il s’agisse de requêtes d’énumération ou de requêtes individuelles sur des comptes sensibles.

**Examen**

1. Cliquez sur l’alerte pour accéder à la page de détails correspondante. Examinez quels types de requêtes ont été effectuées (par exemple, des requêtes Administrateur entreprise ou Administrateur) et si elles ont réussi ou échoué.

2. Des requêtes de ce type sont-elles censées être effectuées à partir de l’ordinateur source en question ?

3. Si c’est le cas et que l’alerte a été mise à jour, **supprimez** l’activité suspecte.

4. Si c’est le cas, mais que cela ne devrait plus se produire, **fermez** l’activité suspecte.

5. Si vous avez des informations sur le compte impliqué : de telles requêtes sont-elles censées être effectuées par ce compte ou ce compte se connecte-t-il normalement à l’ordinateur source ?

 - Si c’est le cas et que l’alerte a été mise à jour, **supprimez** l’activité suspecte.

 - Si c’est le cas, mais que cela ne devrait plus se produire, **fermez** l’activité suspecte.

 - Si vous avez répondu non à toutes les questions ci-dessus, considérez l’alerte comme une attaque malveillante.

6. En l’absence d’informations sur le compte impliqué, vous pouvez accéder au point de terminaison et vérifier quel compte était connecté au moment de l’alerte.

**Correction**

Protégez mieux votre environnement contre cette technique à l’aide du processus suivant :
1. L’ordinateur exécute-t-il un outil d’analyse des vulnérabilités ?  
2. Vérifiez si les utilisateurs et groupes spécifiques interrogés dans l’attaque sont des comptes avec privilèges ou sensibles (par ex., PDG, directeur financier, direction informatique, etc.).  Si c’est le cas, examinez aussi les autres activités sur le point de terminaison et surveillez les ordinateurs auxquels les comptes interrogés sont connectés, car ils sont probablement la cible d’un mouvement latéral.

## <a name="reconnaissance-using-dns"></a>Reconnaissance à l’aide de DNS

**Description**

Votre serveur DNS contient une carte de l’ensemble des ordinateurs, adresses IP et services de votre réseau. Ces informations sont utilisées par les attaquants pour mapper la structure de votre réseau et cibler les ordinateurs intéressants pour les étapes suivantes de l’attaque.

Il existe plusieurs types de requêtes dans le protocole DNS. Azure ATP détecte les demandes de transfert AXFR provenant de serveurs autres que DNS.

**Examen**

1. La machine source (**En provenance de…**) est-elle un serveur DNS ? Si c’est le cas, il s’agit probablement d’un faux positif. Pour le vérifier, cliquez sur l’alerte pour accéder à la page de détails correspondante. Dans le tableau, sous **Requête**, vérifiez quels domaines ont été interrogés. S’agit-il de domaines existants ? Si c’est le cas, **fermez** l’activité suspecte (c’est un faux positif). De plus, assurez-vous que le port UDP 53 est ouvert entre le capteur autonome Azure ATP et l’ordinateur source pour éviter de futurs faux positifs.

2. L’ordinateur source exécute-t-il un scanner de sécurité ? Si c’est le cas, **excluez les entités** dans ATP, soit directement en choisissant **Fermer et exclure**, soit via la page **Exclusion** (sous **Configuration**, disponible pour les administrateurs d’Azure ATP).

3. Si vous avez répondu non à toutes les questions précédentes, considérez l’alerte comme une attaque malveillante.

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

Les attaquants qui compromettent les informations d’identification d’administration ou qui exploitent une faille de sécurité de type zero-day peuvent exécuter des commandes à distance sur votre contrôleur de domaine. Cela peut servir pour obtenir une persistance, collecter des informations, lancer des attaques par déni de service (DOS) ou toute autre raison. Azure ATP détecte les connexions PSexec et les connexions WMI à distance.

**Examen**

1. Cette situation est fréquente pour les stations de travail d’administration, les membres des équipes informatiques et les comptes de service qui effectuent des tâches d’administration sur les contrôleurs de domaine. Si c’est le cas et que l’alerte a été mise à jour du fait qu’elle est effectuée par le même administrateur et/ou ordinateur, **supprimez** l’alerte.

2. **L’ordinateur** en question est-il autorisé à effectuer cette exécution à distance sur votre contrôleur de domaine ?

 - **Le compte** en question est-il autorisé à effectuer cette exécution à distance sur votre contrôleur de domaine ?

 - Si la réponse à ces deux questions est *oui*, **fermez** l’alerte.

3. Si la réponse à l’une de ces questions est *non*, considérez l’attaque comme un vrai positif.

**Correction**

1. Limitez l’accès à distance aux contrôleurs de domaine à partir d’ordinateurs qui ne sont pas de niveau 0.

2. Implémentez un [accès privilégié](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access) pour autoriser uniquement les machines avec une sécurité renforcée à se connecter aux contrôleurs de domaine pour les administrateurs.

## <a name="suspicious-authentication-failures"></a>Échecs d’authentification suspects

**Description**

Dans une attaque par force brute, un attaquant tente de s’authentifier en essayant plusieurs mots de passe pour différents comptes jusqu’à ce qu’il trouve le bon mot de passe de l’un des comptes. Une fois qu’il a deviné le mot de passe d’un compte, l’attaquant utilise ce compte pour se connecter au réseau.

Dans cette détection, une alerte est déclenchée après l’échec de nombreuses tentatives d’authentification utilisant Kerberos ou NTLM. L’attaque peut être horizontale avec un petit nombre de mots de passe possibles pour de nombreux utilisateurs, verticale avec un grand nombre de mots de passe pour seulement quelques utilisateurs, ou à la fois horizontale et verticale. La période minimale avant le déclenchement d’une alerte est d’une semaine.

**Examen**

1. Si de nombreux comptes sont concernés, cliquez sur **Télécharger les détails** pour afficher la liste complète dans une feuille de calcul Excel.

2. Cliquez sur l’alerte pour accéder à la page de détails correspondante. Déterminez si des tentatives de connexion ont donné lieu à une authentification. Les tentatives s’affichent en tant que **Comptes devinés** à droite des données graphiques. Si des comptes devinés sont affichés, font-ils partie des **comptes devinés** normalement utilisés à partir de l’ordinateur source ? Si c’est le cas, **supprimez** l’activité suspecte.

3. S’il n’y a pas de **comptes devinés** affichés, s’agit-il de **comptes attaqués** normalement utilisés à partir de l’ordinateur source ? Si c’est le cas, **supprimez** l’activité suspecte.

**Correction**

Les [mots de passe longs et complexes](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) assurent le niveau minimum de sécurité nécessaire contre les attaques par force brute.

## <a name="suspicious-service-creation---preview-feature"></a>Création d’un service suspect - fonctionnalité en préversion.

**Description**

Un service suspect a été créé sur un contrôleur de domaine dans votre organisation. Cette alerte s’appuie sur l’événement 7045 afin d’identifier cette activité suspecte sur vos points de terminaison. L’événement 7045 doit être transféré à partir des points de terminaison vers ATP en configurant [WEF (Windows Event Forwarding)](configure-event-forwarding.md) ou en transférant l’événement 7045 vers le serveur SIEM et en [configurant votre serveur SIEM](configure-event-collection.md) comme source de données transférant les événements vers ATP.

**Examen**

1. Si l’ordinateur en question est une station de travail d’administration ou un ordinateur sur lequel les membres de l’équipe informatique et les comptes de service effectuent des tâches d’administration, il peut s’agir d’un faux positif et vous pouvez être amené à **supprimer** l’alerte et à l’ajouter à la liste des exclusions, si nécessaire.

2. Reconnaissez-vous ce service sur cet ordinateur ?

 - Le **compte** en question est-il autorisé à installer ce service ?

 - Si la réponse à ces deux questions est *oui*, **fermez** l’alerte ou ajoutez-la à la liste des exclusions.

3. Si la réponse à l’une de ces questions est *non*, considérez l’attaque comme un vrai positif.

**Correction**

- Implémentez un accès doté de moins de privilèges sur les ordinateurs du domaine pour autoriser uniquement des utilisateurs spécifiques à créer de nouveaux services.

## <a name="unusual-protocol-implementation"></a>Implémentation de protocole inhabituelle


**Description**

Les attaquants utilisent des outils qui implémentent différents protocoles (SMB, Kerberos, NTLM) de façon inhabituelle. Ce type de trafic réseau est admis par Windows sans avertissement, mais Azure ATP est capable de reconnaître une intention potentiellement malveillante. Le comportement est révélateur de certaines techniques comme l’attaque par force brute ou Over-Pass-the-Hash, ou de l’exploitation des failles de sécurité par de puissants ransomware tels que WannaCry.

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


>![NOTE] Pour désactiver une activité suspecte, contactez le support technique.


## <a name="see-also"></a>Voir aussi
- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)
