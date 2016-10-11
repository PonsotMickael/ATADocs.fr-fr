---
title: "Configurer la collecte d’événements | Microsoft ATA"
description: "Décrit les options de configuration disponibles pour collecter des événements avec ATA"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 09/28/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d2c1c00ff649557c1a0a16385e025c9d597c3bbf
ms.openlocfilehash: 91ce3a3fef27673712a708aa1e92c32298cedd84


---

*S’applique à : Advanced Threat Analytics version 1.6 et 1.7*



# Configurer la collecte d’événements
Pour améliorer les fonctionnalités de détection, ATA a besoin de l’ID de journal des événements Windows 4776. Les événements peuvent être transférés à la passerelle ATA de deux manières : soit en configurant la passerelle ATA de façon à écouter les événements SIEM, soit en [configurant le transfert d’événements Windows](#configuring-windows-event-forwarding).

## Collecte d’événements
Outre la collecte et l’analyse du trafic réseau à destination et en provenance des contrôleurs de domaine, ATA peut utiliser l’événement Windows 4776 pour optimiser la détection d’attaques Pass-the-Hash. Vous pouvez soit recevoir cet événement de votre serveur SIEM, soit définir le transfert d’événements Windows à partir de votre contrôleur de domaine. Les événements collectés fournissent à ATA des informations supplémentaires qui ne sont pas accessibles par le biais du trafic réseau du contrôleur de domaine.

### SIEM/Syslog
Pour qu’ATA puisse consommer des données provenant d’un serveur Syslog, vous devez effectuer les opérations suivantes :

-   Configurez vos serveurs de passerelle ATA pour écouter et accepter les événements transférés à partir du serveur SIEM/Syslog.

-   Configurez votre serveur SIEM/Syslog de façon à transférer des événements spécifiques à la passerelle ATA.

> [!IMPORTANT]
> -   Ne transférez pas toutes les données Syslog vers la passerelle ATA.
> -   ATA prend en charge le trafic UDP provenant du serveur SIEM/Syslog.

Pour plus d’informations sur la façon de configurer le transfert d’événements spécifiques vers un autre serveur, consultez la documentation produit de votre serveur SIEM/Syslog. 

### Transfert d’événements Windows
Si vous n’utilisez pas un serveur SIEM/Syslog, vous pouvez configurer vos contrôleurs de domaine Windows de façon à transférer l’événement Windows associé à l’ID 4776 pour qu’il soit collecté et analysé par ATA. L’événement Windows associé à l’ID 4776 fournit des données relatives aux authentifications NTLM.

## Configuration de la passerelle ATA pour écouter les événements SIEM

1.  Dans la configuration ATA, sous l’onglet « Événements », activez **Syslog** et cliquez sur **Enregistrer**.

    ![Image de l’activation du protocole UDP de l’écouteur syslog](media/ATA-enable-siem-forward-events.png)

2.  Configurez votre serveur SIEM ou Syslog pour transférer l’événement Windows associé à l’ID 4776 vers l’adresse IP de l’une des passerelles ATA. Pour plus d’informations sur la configuration de votre serveur SIEM, consultez l’aide en ligne de SIEM ou explorez les options de support technique à votre disposition pour obtenir les formats à respecter pour chaque serveur SIEM.

### Prise en charge de SIEM
ATA prend en charge les événements SIEM aux formats suivants :  

#### RSA Security Analytics
&lt;Syslog Header&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   L’en-tête syslog est facultatif.

-   Le séparateur de caractère « \n » est obligatoire entre tous les champs.

-   Les champs, dans l’ordre, sont les suivants :

    1.  Constante RsaSA (doit être indiquée).

    2.  Horodateur de l’événement réel (vérifiez qu’il ne s’agit pas de l’horodateur de l’arrivée au serveur SIEM ou de l’envoi à ATA). De préférence avec une précision de l’ordre de la milliseconde (ceci est très important).

    3.  ID de l’événement Windows.

    4.  Nom du fournisseur d’événements Windows.

    5.  Nom du journal des événements Windows.

    6.  Nom de l’ordinateur recevant l’événement (ici, le contrôleur de domaine).

    7.  Nom de l’utilisateur qui s’authentifie.

    8.  Nom de l’hôte source.

    9. Code de résultat de NTLM.

-   L’ordre est important, et rien d’autre ne doit figurer dans le message.

#### HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|Le contrôleur de domaine a tenté de valider les informations d’identification d’un compte.|Low| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Reason or Error Code

-   Doit être conforme à la définition du protocole.

-   Aucun en-tête syslog.

-   La partie en-tête, séparée par une barre verticale, doit exister (comme indiqué dans le protocole).

-   Les clés suivantes dans la partie _Extension_ doivent être présentes dans l’événement :

    -   externalId = ID de l’événement Windows.

    -   rt = horodateur de l’événement réel (vérifiez qu’il ne s’agit pas de l’horodateur de l’arrivée au serveur SIEM ou de l’envoi à Microsoft). De préférence avec une précision de l’ordre de la milliseconde (ceci est très important).

    -   cat = nom du journal des événements Windows.

    -   shost = nom de l’hôte source.

    -   dhost = nom de l’ordinateur recevant l’événement (ici, le contrôleur de domaine).

    -   duser = utilisateur qui s’authentifie.

-   L’ordre de la partie _Extension_ n’est pas important.

-   Vous devez avoir une clé personnalisée et un libellé dé clé pour les deux champs suivants :

    -   « EventSource »

    -   « Reason or Error Code » = code de résultat de NTLM

#### Splunk
&lt;En-tête Syslog&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

L’ordinateur a tenté de valider les informations d’identification d’un compte.

Package d’authentification : MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

Compte d’ouverture de session : Administrateur

Station de travail source : SIEM

Code d’erreur : 0x0

-   L’en-tête syslog est facultatif.

-   Le séparateur de caractère « \r\n » est utilisé entre tous les champs obligatoires.

-   Les champs sont au format clé = valeur.

-   Les clés suivantes doivent exister et avoir une valeur :

    -   EventCode = ID de l’événement Windows.

    -   Logfile = nom du journal des événements Windows.

    -   SourceName = nom du fournisseur d’événements Windows.

    -   TimeGenerated = horodateur de l’événement réel (vérifiez qu’il ne s’agit pas de l’horodateur de l’arrivée au serveur SIEM ou de l’envoi à ATA). Le format doit être aaaaMMjjHHmmss.FFFFFF, avec de préférence une précision de l’ordre de la milliseconde (ceci est très important).

    -   ComputerName = nom de l’hôte source.

    -   Message = texte de l’événement Windows d’origine.

-   La clé et la valeur du message DOIVENT figurer en dernier.

-   L’ordre n’est pas important pour les paires clé=valeur.

#### QRadar
QRadar permet la collecte d’événements par le biais d’un agent. Si les données sont recueillies au moyen d’un agent, le format de l’heure est collecté sans les données des millisecondes. ATA nécessitant les données des millisecondes, vous devez définir QRadar pour qu’il utilise la collecte d’événements de Windows sans agent. Pour plus d’informations, consultez [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Agentless Windows Events Collection using the MSRPC Protocol (Collecte des événements Windows sans agent à l’aide du protocole MSRPC)").

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

Les champs requis sont les suivants :

- Type d’agent pour la collecte
- Nom du fournisseur de journaux des événements Windows
- Source du journal des événements Windows
- Nom de domaine complet du contrôleur de domaine
- ID de l’événement Windows.

TimeGenerated représente l’horodateur de l’événement réel (vérifiez qu’il ne s’agit pas de l’horodateur de l’arrivée au serveur SIEM ou de l’envoi à ATA). Le format doit être aaaaMMjjHHmmss.FFFFFF, avec de préférence une précision de l’ordre de la milliseconde (ceci est très important).

Message représente le texte de l’événement Windows d’origine.

Assurez-vous que \t sépare les paires clé/valeur.

>[!NOTE] 
> Utiliser WinCollect pour la collecte des événements Windows n’est pas pris en charge.

## Configuration du transfert d’événements Windows

### Configuration WEF pour la passerelle ATA avec mise en miroir de ports

Une fois que vous avez configuré la mise en miroir des ports des contrôleurs de domaine sur la passerelle ATA, suivez les instructions ci-dessous pour configurer Windows Event Forwarding à l’aide de la configuration Initialisation par la source. Il s’agit de l’une des façons de configurer Windows Event Forwarding. 

**Étape 1 : Ajouter le compte service réseau au groupe Lecteurs des journaux d’événements du domaine.** 

Dans ce scénario, nous partons du principe que la passerelle ATA est un membre du domaine.

1.  Ouvrez Utilisateurs et ordinateurs Active Directory, accédez au dossier **Builtin** et double-cliquez sur **Lecteurs des journaux d’événements**. 
2.  Sélectionnez **Membres**.
4.  Si **Service réseau** ne figure pas dans la liste, cliquez sur **Ajouter** et tapez **Service réseau** dans le champ **Entrez les noms d’objets à sélectionner**. Ensuite, cliquez sur **Vérifier les noms** et cliquez deux fois sur **OK**. 

**Étape 2 : Créer une stratégie sur les contrôleurs de domaine pour définir le paramètre Configurer le Gestionnaire d’abonnements cible.** 
> [!Note] 
> Vous pouvez créer une stratégie de groupe pour ces paramètres et appliquer la stratégie de groupe à chaque contrôleur de domaine surveillé par la passerelle ATA. Les étapes ci-dessous modifient la stratégie locale du contrôleur de domaine.     

1.  Exécutez la commande suivante sur chaque contrôleur de domaine : *winrm quickconfig*
2.  Sur la ligne de commande, tapez *gpedit.msc*.
3.  Développez **Configuration ordinateur > Modèles d’administration > Composants Windows > Transfert d’événements**.

 ![Image de l’éditeur de groupe de stratégie locale](media/wef 1 local group policy editor.png)

4.  Double-cliquez sur **Configurer le Gestionnaire d’abonnements cible**.
   
    1.  Sélectionnez **Activé**.
    2.  Sous **Options**, cliquez sur **Afficher**.
    3.  Sous **SubscriptionManagers**, entrez la valeur suivante et cliquez sur **OK** :  *Server=http://<fqdnATAGateway>:5985/wsman/SubscriptionManager/WEC,Refresh=10* (par exemple : Server=http://atagateway9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10)
 
   ![Configurer l’image d’abonnement cible](media/wef 2 config target sub manager.png)
   
    5.  Cliquez sur **OK**.
    6.  À partir d’une invite de commandes avec élévation de privilèges, tapez *gpupdate /force*. 

**Étape 3 : Effectuer les opérations suivantes sur la passerelle ATA** 

1.  Ouvrez une invite de commandes avec élévation de privilèges et tapez *wecutil qc*.
2.  Ouvrez l’**Observateur d’événements**. 
3.  Cliquez avec le bouton droit sur **Abonnements** et sélectionnez **Créer un abonnement**. 

   1.   Entrez un nom et une description pour l’abonnement. 
   2.   Pour **Journal de destination**, vérifiez que **Événements transférés** est sélectionné. Pour qu’ATA lise les événements, le journal de destination doit être **Événements transférés**. 
   3.   Sélectionnez **Initialisation par l’ordinateur source** et cliquez sur **Sélectionner les groupes d’ordinateurs**.
        1.  Cliquez sur **Ajouter un ordinateur de domaine**.
        2.  Entrez le nom du contrôleur de domaine dans le champ **Entrer le nom de l’objet à sélectionner**. Ensuite, cliquez sur **Vérifier les noms**, puis sur **OK**. 
       
        ![Image de l’Observateur d’événements](media/wef3 event viewer.png)
   
        
        3.  Cliquez sur **OK**.
   4.   Cliquez sur **Sélectionner des événements**.

        1. Cliquez sur **Par journal** et sélectionnez **Sécurité**.
        2. Dans le champ **Inclut/exclut l’ID d’événement**, tapez **4776**, puis cliquez sur **OK**. 

 ![Image de filtre de requête](media/wef 4 query filter.png)

   5.   Cliquez avec le bouton droit sur l’abonnement créé et sélectionnez **État d’exécution** pour voir s’il existe des problèmes avec l’état. 
   6.   Après quelques minutes, vérifiez que l’événement 4776 s’affiche dans les événements transférés sur la passerelle ATA.


### Configuration WEF pour la passerelle légère ATA
Quand vous installez la passerelle légère ATA sur vos contrôleurs de domaine, vous pouvez configurer vos contrôleurs de domaine pour qu’ils se transfèrent les événements à eux-mêmes. Procédez comme suit pour configurer Window Event Forwarding lors de l’utilisation de la passerelle légère ATA. Il s’agit de l’une des façons de configurer Windows Event Forwarding.  

**Étape 1 : Ajouter le compte service réseau au groupe Lecteurs des journaux d’événements du domaine** 

1.  Ouvrez Utilisateurs et ordinateurs Active Directory, accédez au dossier **Builtin** et double-cliquez sur **Lecteurs des journaux d’événements**. 
2.  Sélectionnez **Membres**.
3.  Si **Service réseau** ne figure pas dans la liste, cliquez sur **Ajouter** et tapez **Service réseau** dans le champ **Entrez les noms d’objets à sélectionner**. Ensuite, cliquez sur **Vérifier les noms** et cliquez deux fois sur **OK**. 

**Étape 2 : Effectuer les étapes suivantes sur le contrôleur de domaine après l’installation de la passerelle légère ATA** 

1.  Ouvrez une invite de commandes avec élévation de privilèges et tapez *winrm quickconfig* et *wecutil qc*. 
2.  Ouvrez l’**Observateur d’événements**. 
3.  Cliquez avec le bouton droit sur **Abonnements** et sélectionnez **Créer un abonnement**. 

   1.   Entrez un nom et une description pour l’abonnement. 
   2.   Pour **Journal de destination**, vérifiez que **Événements transférés** est sélectionné. Pour qu’ATA lise les événements, le journal de destination doit être Événements transférés.

        1.  Sélectionnez **Initialisation par le collecteur** et cliquez sur **Sélectionner les ordinateurs**. Ensuite, cliquez sur **Ajouter un ordinateur de domaine**.
        2.  Entrez le nom du contrôleur de domaine dans le champ **Entrer le nom de l’objet à sélectionner**. Ensuite, cliquez sur **Vérifier les noms**, puis sur **OK**.

            ![Image des propriétés d’abonnement](media/wef 5 sub properties computers.png)

        3.  Cliquez sur **OK**.
   3.   Cliquez sur **Sélectionner des événements**.

        1.  Cliquez sur **Par journal** et sélectionnez **Sécurité**.
        2.  Dans le champ **Inclut/exclut l’ID d’événement**, tapez *4776*, puis cliquez sur **OK**. 

![Image de filtre de requête](media/wef 4 query filter.png)


  4.    Cliquez avec le bouton droit sur l’abonnement créé et sélectionnez **État d’exécution** pour voir s’il existe des problèmes avec l’état. 

> [!Note] 
> Vous devrez peut-être redémarrer le contrôleur de domaine pour que le paramètre soit pris en compte. 

Après quelques minutes, vérifiez que l’événement 4776 s’affiche dans les événements transférés sur la passerelle ATA.



Pour plus d’informations, consultez [Configurer les ordinateurs pour transférer et recueillir les événements](https://technet.microsoft.com/library/cc748890).

## Voir aussi
- [Installer ATA](install-ata.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Sep16_HO4-->


