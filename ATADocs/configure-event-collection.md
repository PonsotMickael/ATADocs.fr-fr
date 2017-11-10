---
title: "Configurer le transfert des événements Windows dans Advanced Threat Analytics | Microsoft Docs"
description: "Décrit les options de configuration du transfert des événements Windows avec ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 482b16462d115c7bcc2854d30c2ef19fce37f2c0
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/07/2017
---
*S’applique à : Advanced Threat Analytics version 1.8*



# <a name="configuring-windows-event-forwarding"></a>Configuration du transfert d’événements Windows

> [!NOTE]
> Pour les versions 1.8 et ultérieures d’ATA, la configuration de la collecte d’événements n’est plus nécessaire pour les passerelles légères ATA. La passerelle légère ATA peut désormais lire les événements localement, sans qu’il soit nécessaire de configurer le transfert d’événements.


Pour améliorer les capacités de détection, ATA a besoin des événements Windows suivants : 4776, 4732, 4733, 4728, 4729, 4756, 4757. Ils peuvent être lus automatiquement par la passerelle légère ATA ou, si la passerelle légère ATA n’est pas déployée, ils peuvent être transférés à la passerelle ATA de deux manières : en configurant la passerelle ATA afin qu’elle reste à l’écoute des événements SIEM ou en configurant le transfert d’événements Windows.



### <a name="wef-configuration-for-ata-gateways-with-port-mirroring"></a>Configuration WEF pour la passerelle ATA avec mise en miroir de ports

Une fois que vous avez configuré la mise en miroir des ports des contrôleurs de domaine sur la passerelle ATA, suivez les instructions ci-dessous pour configurer Windows Event Forwarding à l’aide de la configuration Initialisation par la source. Il s’agit de l’une des façons de configurer Windows Event Forwarding. 

**Étape 1 : ajouter le compte service réseau au groupe Lecteurs des journaux d’événements du domaine** 

Dans ce scénario, nous partons du principe que la passerelle ATA est un membre du domaine.

1.  Ouvrez Utilisateurs et ordinateurs Active Directory, accédez au dossier **BuiltIn** et double-cliquez sur **Lecteurs des journaux d’événements**. 
2.  Sélectionnez **Membres**.
4.  Si **Service réseau** ne figure pas dans la liste, cliquez sur **Ajouter** et tapez **Service réseau** dans le champ **Entrez les noms d’objets à sélectionner**. Ensuite, cliquez sur **Vérifier les noms** et cliquez deux fois sur **OK**. 

Après avoir ajouté le **Service réseau** au groupe **Lecteurs des journaux d’événements**, redémarrez les contrôleurs de domaine pour que la modification prenne effet.

**Étape 2 : créer une stratégie sur les contrôleurs de domaine pour définir le paramètre Configurer le Gestionnaire d’abonnements cible.** 
> [!Note] 
> Vous pouvez créer une stratégie de groupe pour ces paramètres et appliquer la stratégie de groupe à chaque contrôleur de domaine surveillé par la passerelle ATA. Les étapes ci-dessous modifient la stratégie locale du contrôleur de domaine.     

1.  Exécutez la commande suivante sur chaque contrôleur de domaine : *winrm quickconfig*
2.  Sur la ligne de commande, tapez *gpedit.msc*.
3.  Développez **Configuration ordinateur > Modèles d’administration > Composants Windows > Transfert d’événements**.

 ![Image de l’éditeur de groupe de stratégie locale](media/wef 1 local group policy editor.png)

4.  Double-cliquez sur **Configurer le Gestionnaire d’abonnements cible**.
   
    1.  Sélectionnez **Activé**.
    2.  Sous **Options**, cliquez sur **Afficher**.
    3.  Sous **SubscriptionManagers**, entrez la valeur suivante et cliquez sur **OK** : *Server=http://<fqdnATAGateway>:5985/wsman/SubscriptionManager/WEC,Refresh=10* (par exemple : Server=http://atagateway9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10)
 
   ![Configurer l’image d’abonnement cible](media/wef 2 config target sub manager.png)
   
    5.  Cliquez sur **OK**.
    6.  À partir d’une invite de commandes avec élévation de privilèges, tapez *gpupdate /force*. 

**Étape 3 : effectuer les opérations suivantes sur la passerelle ATA** 

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
        2. Dans le champ **Inclut/exclut l’ID d’événement**, tapez le numéro d’événement puis cliquez sur **OK**. Par exemple, tapez 4776, comme dans l’exemple suivant.

 ![Image de filtre de requête](media/wef 4 query filter.png)

   5.   Cliquez avec le bouton droit sur l’abonnement créé et sélectionnez **État d’exécution** pour voir s’il existe des problèmes avec l’état. 
   6.   Après quelques minutes, vérifiez que les événements que vous avez configurés pour être transférés apparaissent dans les événements transférés sur la passerelle ATA.


Pour plus d’informations, consultez [Configurer les ordinateurs pour transférer et recueillir les événements](https://technet.microsoft.com/library/cc748890)

## <a name="see-also"></a>Voir aussi
- [Installer ATA](install-ata-step1.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
