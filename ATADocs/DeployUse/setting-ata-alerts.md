---
# required metadata

title: Configuration des notifications ATA | Microsoft Advanced Threat Analytics
description: Décrit comment définir des alertes ATA afin d’être averti quand des activités suspectes sont détectées.
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

# Définition des notifications ATA
ATA peut vous avertir quand il détecte une activité suspecte, par courrier électronique ou en utilisant le transfert d’événements ATA et en transférant l’événement à votre serveur SIEM/syslog. Avant de sélectionner les notifications à recevoir, vous devez [configurer votre serveur de messagerie et votre serveur Syslog](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   Les notifications par courrier électronique incluent un lien qui dirige l’utilisateur directement vers l’activité suspecte qui a été détectée. La partie nom d’hôte du lien provient du paramètre de l’URL de la console ATA dans la page Centre ATA. Par défaut, l’URL de la console ATA est l’adresse IP sélectionnée pendant l’installation du centre ATA.  Si vous envisagez de configurer des alertes par courrier électronique, nous vous recommandons d’utiliser un nom de domaine complet comme URL de la console ATA.
> -   Les notifications sont envoyées à partir du centre ATA vers le serveur SMTP ou le serveur Syslog.

Pour recevoir les notifications par courrier électronique, procédez comme suit :


1. Dans la console ATA, sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.
![Icône des paramètres de configuration ATA](media/ATA-config-icon.JPG)

2. Sélectionnez **Notifications**.
3. Sous **Notifications par courrier électronique**, utilisez les bascules pour sélectionner les notifications à envoyer :


    - Une nouvelle activité suspecte est détectée
    - Un nouveau problème d’intégrité a été détecté
    - Une mise à jour logicielle est disponible

4. Spécifiez les destinataires qui recevront les notifications par courrier électronique.

    [!Remarque :]Les alertes par courrier électronique pour les activités suspectes sont envoyées uniquement au moment de la création de l’activité suspecte.


5. Cliquez sur **Enregistrer**.

Pour recevoir les notifications Syslog, procédez comme suit :


1. Dans la console ATA, sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.
![Icône des paramètres de configuration ATA](media/ATA-config-icon.JPG)

2. Sélectionnez **Notifications**.
3. Sous **Notifications Syslog**, utilisez les bascules pour sélectionner les notifications à envoyer :


    - Une nouvelle activité suspecte est détectée
    - Une activité suspecte est mise à jour
    - Un nouveau problème d’intégrité a été détecté
5. Cliquez sur **Enregistrer**.
![Image des paramètres de notification ATA](media/ATA-notification-settings.png)




## Voir aussi
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Jun16_HO1-->


