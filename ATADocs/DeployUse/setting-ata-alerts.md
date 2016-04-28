---
# required metadata

title: Configuration des alertes ATA | Microsoft Advanced Threat Analytics
description: Décrit comment faire en sorte qu’ATA vous alerte (par courrier électronique ou transfert d’événements ATA) quand il détecte des activités suspectes 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configuration des alertes ATA
ATA peut vous alerter quand il détecte une activité suspecte, par courrier électronique ou en utilisant le transfert d’événements ATA et en transférant l’événement à votre serveur SIEM/syslog. Si vous activez l’un de ces types d’alertes ou les deux, vous pouvez définir les éléments associés suivants.

> [!NOTE]
> -   Les notifications par courrier électronique incluent un lien qui dirige l’utilisateur directement vers l’activité suspecte qui a été détectée. La partie nom d’hôte du lien provient du paramètre de l’URL de la console ATA dans la page Centre ATA. Par défaut, l’URL de la console ATA est l’adresse IP sélectionnée pendant l’installation du centre ATA.  Si vous allez configurer des alertes par courrier électronique, il est recommandé d’utiliser un nom de domaine complet comme URL de la console ATA.
> -   Les alertes liées à l’intégrité du système sont envoyées uniquement par courrier électronique.
> -   Les alertes sont envoyées à partir du centre ATA vers le serveur SMTP ou le serveur Syslog.
> -   Les alertes par courrier électronique pour les activités suspectes sont envoyées uniquement lors de la création de l’activité suspecte.

## Définition de la langue et de la fréquence
Le paramètre **Langue** s’applique aux notifications envoyées par courrier électronique et aux notifications envoyées au serveur Syslog.

Le paramètre **Fréquence** s’applique uniquement aux notifications envoyées au serveur Syslog.

1.  Ouvrez la console ATA.

2.  Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône des paramètres de configuration ATA](media/ATA-config-icon.JPG)

3.  Sélectionnez **Alertes**.

4.  Sous **Langue**, sélectionnez la langue de votre choix.

5.  Sous **Fréquence**, sélectionnez **Fréquence basse** si vous voulez recevoir une notification brève uniquement quand une alerte est générée. Sélectionnez **Fréquence élevée** si vous voulez recevoir une notification détaillée quand une alerte est générée et quand des alertes existantes sont modifiées.

    ![Image de la configuration du niveau de détail des alertes](media/ATA-alerts-verbosity-language.png)

6.  Cliquez sur **Enregistrer**.

## Configuration des alertes par courrier électronique
ATA peut vous alerter quand il détecte une activité suspecte. Si vous activez les alertes par courrier électronique, vous pouvez définir les éléments associés suivants.

1.  Sur le serveur du centre ATA, cliquez sur l’icône **Microsoft Advanced Threat Analytics Management**(Gestion de Microsoft Advanced Threat Analytics) sur le Bureau.

2.  Entrez votre nom d’utilisateur et votre mot de passe, puis cliquez sur **Se connecter**.

3.  Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône des paramètres de configuration ATA](media/ATA-config-icon.JPG)

4.  Sélectionnez **Alertes**.

5.  Activez **Courrier** pour activer les alertes par courrier électronique et entrez les informations suivantes :

    |Champ|Description|Valeur|
    |---------|---------------|---------|
    |Point de terminaison du serveur SMTP (obligatoire)|Entrez le nom de domaine complet de votre serveur SMTP.|Exemple :<br />smtp.contoso.com|
    |SSL|Activez/désactivez SSL si le serveur SMTP exigeait SSL. **Remarque :** si vous activez SSL, vous devez également modifier le numéro de port.|La valeur par défaut est désactivée|
    |Authentification|Activez l’authentification si votre serveur SMTP l’exige. **Remarque :** si vous activez l’authentification, vous devez fournir le nom d’utilisateur et le mot de passe d’un compte de messagerie qui a l’autorisation de se connecter au serveur SMTP.|La valeur par défaut est désactivée|
    |Envoyer depuis (obligatoire)|Entrez une adresse de messagerie à partir de laquelle le courrier sera envoyé.|Exemple :<br />ATA@contoso.com|
    |Envoyer à (obligatoire)|Entrez les adresses de messagerie des utilisateurs ou des groupes de messagerie qui doivent recevoir des messages électroniques quand ATA détecte une activité suspecte. **Remarque :** entrez une adresse de messagerie à la fois et cliquez sur le signe plus pour l’ajouter.|Exemple :<br />securityteam@contoso.com|

## Configuration du transfert d’événements ATA à SIEM
ATA peut vous alerter quand il détecte une activité suspecte en envoyant l’alerte à votre serveur Syslog. Si vous activez les alertes Syslog, vous pouvez définir les éléments associés suivants.

1.  Avant de configurer les alertes Syslog, collaborez avec votre administrateur SIEM pour connaître les informations suivantes :

    -   Nom de domaine complet ou adresse IP du serveur SIEM

    -   Port sur lequel écoute le serveur SIEM

    -   Mode de transport à utiliser : UDP, TCP ou TCP sécurisé

    -   Format sous lequel envoyer les données, RFC 3164 ou 5424

2.  Sur le serveur du centre ATA, cliquez sur l’icône **Microsoft Advanced Threat Analytics Management**(Gestion de Microsoft Advanced Threat Analytics) sur le Bureau.

3.  Entrez votre nom d’utilisateur et votre mot de passe, puis cliquez sur **Se connecter**.

4.  Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône des paramètres de configuration ATA](media/ATA-config-icon.JPG)

5.  Sélectionnez **Alertes**.

6.  Activez **Syslog** pour permettre l’envoi d’alertes sur les activités suspectes à votre serveur Syslog et entrez les informations suivantes :

    |Champ|Description|
    |---------|---------------|
    |Point de terminaison du serveur Syslog|Nom de domaine complet du serveur Syslog|
    |Transport|Peut être UDP, TCP ou TCP sécurisé|
    |Format|Il s’agit du format utilisé par ATA pour envoyer des événements au serveur SIEM : RFC 5424 ou 3164.|

## Voir aussi
[Pour obtenir de l’aide, consultez notre forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


