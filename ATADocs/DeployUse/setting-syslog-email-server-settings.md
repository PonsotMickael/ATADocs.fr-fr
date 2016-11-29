---
title: "Configuration des paramètres de messagerie | Microsoft Docs"
description: "Décrit comment faire en sorte qu’ATA vous avertisse (par courrier électronique ou transfert d’événements ATA) quand il détecte des activités suspectes"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: bff20bf7-8b53-49da-81e5-b818a1c3b24e
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: fca7f1b2b8260cad6e0ce32aad1c9e1b53fc0ad5
ms.openlocfilehash: d967cbf2674c5f561e63f66b64640ac08daad6c0


---

*S’applique à : Advanced Threat Analytics version 1.7*



## <a name="provide-ata-with-up-your-email-server-settings"></a>Fournir à ATA les paramètres de votre serveur de messagerie
ATA peut vous avertir quand il détecte une activité suspecte. Pour qu’ATA puisse envoyer des notifications par courrier électronique, vous devez d’abord configurer les **paramètres du serveur de messagerie**.

1.  Sur le serveur du centre ATA, cliquez sur l’icône **Microsoft Advanced Threat Analytics Management**(Gestion de Microsoft Advanced Threat Analytics) sur le Bureau.

2.  Entrez votre nom d’utilisateur et votre mot de passe, puis cliquez sur **Se connecter**.

3.  Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône des paramètres de configuration ATA](media/ATA-config-icon.JPG)

4.  Dans la section **Notifications** sous **Serveur de messagerie**, entrez les informations suivantes :

    |Champ|Description|Valeur|
    |---------|---------------|---------|
    |Point de terminaison du serveur SMTP (obligatoire)|Entrez le nom de domaine complet de votre serveur SMTP et modifiez éventuellement le numéro de port (par défaut, 25).|Exemple :<br />smtp.contoso.com|
    |SSL|Activez/désactivez SSL si le serveur SMTP exigeait SSL. **Remarque :** si vous activez SSL, vous devez également modifier le numéro de port.|La valeur par défaut est désactivée|
    |Authentification|Activez l’authentification si votre serveur SMTP l’exige. **Remarque :** si vous activez l’authentification, vous devez fournir le nom d’utilisateur et le mot de passe d’un compte de messagerie qui a l’autorisation de se connecter au serveur SMTP.|La valeur par défaut est désactivée|
    |Envoyer depuis (obligatoire)|Entrez une adresse de messagerie à partir de laquelle le courrier sera envoyé.|Exemple :<br />ATA@contoso.com|
    ![Image des paramètres du serveur de messagerie ATA](media/ATA-email-server-1.7.png)

## <a name="provide-ata-with-your-syslog-server-settings"></a>Fournir à ATA les paramètres de votre serveur Syslog
ATA peut vous avertir quand il détecte une activité suspecte en envoyant la notification à votre serveur Syslog. Si vous activez les notifications Syslog, vous pouvez définir les éléments associés suivants.

1.  Avant de configurer les notifications Syslog, collaborez avec votre administrateur SIEM pour connaître les informations suivantes :

    -   Nom de domaine complet ou adresse IP du serveur SIEM

    -   Port sur lequel écoute le serveur SIEM

    -   Mode de transport à utiliser : UDP, TCP ou TLS (Syslog sécurisé)

    -   Format sous lequel envoyer les données, RFC 3164 ou 5424

2.  Sur le serveur du centre ATA, cliquez sur l’icône **Microsoft Advanced Threat Analytics Management**(Gestion de Microsoft Advanced Threat Analytics) sur le Bureau.

3.  Entrez votre nom d’utilisateur et votre mot de passe, puis cliquez sur **Se connecter**.

4.  Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône des paramètres de configuration ATA](media/ATA-config-icon.JPG)

5.  Dans la section Notifications, sélectionnez **Serveur Syslog** et entrez les informations suivantes :

    |Champ|Description|
    |---------|---------------|
    |Point de terminaison du serveur Syslog|Nom de domaine complet du serveur Syslog et modifiez éventuellement le numéro de port (par défaut, 514)|
    |Transport|Peut être UDP, TCP ou TLS (Syslog sécurisé)|
    |Format|Il s’agit du format utilisé par ATA pour envoyer des événements au serveur SIEM : RFC 5424 ou 3164.|

 ![Image des paramètres du serveur Syslog ATA](media/ata-syslog-server-settings-1.7.png)



## <a name="see-also"></a>Voir aussi
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Nov16_HO3-->


