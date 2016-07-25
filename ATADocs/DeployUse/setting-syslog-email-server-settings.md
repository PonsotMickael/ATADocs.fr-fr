---
title: "Définition des notifications ATA | Microsoft ATA"
description: "Décrit comment faire en sorte qu’ATA vous avertisse (par courrier électronique ou transfert d’événements ATA) quand il détecte des activités suspectes"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 5864070fe3ad5aedf1ff79d8386caba4b6a79adc


---

## Fournir à ATA les paramètres de votre serveur de messagerie
ATA peut vous avertir quand il détecte une activité suspecte. Pour qu’ATA puisse envoyer des notifications par courrier électronique, vous devez d’abord configurer les **paramètres du serveur de messagerie**.

1.  Sur le serveur du centre ATA, cliquez sur l’icône **Microsoft Advanced Threat Analytics Management**(Gestion de Microsoft Advanced Threat Analytics) sur le Bureau.

2.  Entrez votre nom d’utilisateur et votre mot de passe, puis cliquez sur **Se connecter**.

3.  Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône des paramètres de configuration ATA](media/ATA-config-icon.JPG)

4.  Sous l’onglet **Général**, sous **Serveur de messagerie**, entrez les informations suivantes :

    |Champ|Description|Valeur|
    |---------|---------------|---------|
    |Point de terminaison du serveur SMTP (obligatoire)|Entrez le nom de domaine complet de votre serveur SMTP.|Exemple :<br />smtp.contoso.com|
    |SSL|Activez/désactivez SSL si le serveur SMTP exigeait SSL. **Remarque :** si vous activez SSL, vous devez également modifier le numéro de port.|La valeur par défaut est désactivée|
    |Authentification|Activez l’authentification si votre serveur SMTP l’exige. **Remarque :** si vous activez l’authentification, vous devez fournir le nom d’utilisateur et le mot de passe d’un compte de messagerie qui a l’autorisation de se connecter au serveur SMTP.|La valeur par défaut est désactivée|
    |Envoyer depuis (obligatoire)|Entrez une adresse de messagerie à partir de laquelle le courrier sera envoyé.|Exemple :<br />ATA@contoso.com|
    ![Image des paramètres du serveur de messagerie ATA](media/ATA-email-server.png)

## Fournir à ATA les paramètres de votre serveur Syslog
ATA peut vous avertir quand il détecte une activité suspecte en envoyant la notification à votre serveur Syslog. Si vous activez les notifications Syslog, vous pouvez définir les éléments associés suivants.

1.  Avant de configurer les notifications Syslog, collaborez avec votre administrateur SIEM pour connaître les informations suivantes :

    -   Nom de domaine complet ou adresse IP du serveur SIEM

    -   Port sur lequel écoute le serveur SIEM

    -   Mode de transport à utiliser : UDP, TCP ou TLS (Syslog sécurisé)

    -   Format sous lequel envoyer les données, RFC 3164 ou 5424

2.  Sur le serveur du centre ATA, cliquez sur l’icône **Microsoft Advanced Threat Analytics Management**(Gestion de Microsoft Advanced Threat Analytics) sur le Bureau.

3.  Entrez votre nom d’utilisateur et votre mot de passe, puis cliquez sur **Se connecter**.

4.  Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône des paramètres de configuration ATA](media/ATA-config-icon.JPG)

5.  Sélectionnez **Serveur Syslog** puis entrez les informations suivantes :

    |Champ|Description|
    |---------|---------------|
    |Point de terminaison du serveur Syslog|Nom de domaine complet du serveur Syslog|
    |Transport|Peut être UDC, TCP ou TLS (Syslog sécurisé).|
    |Format|Il s’agit du format utilisé par ATA pour envoyer des événements au serveur SIEM : RFC 5424 ou 3164.|





## Voir aussi
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


