---
title: "Définition des notifications ATA | Microsoft ATA"
description: "Décrit comment définir des alertes ATA afin d’être averti quand des activités suspectes sont détectées."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 35fa7afeb673ec2b1aa295e576865cdd5c073c85
ms.openlocfilehash: a5787be5a5a0df96651b3be8e056bcdd4340df94


---

*S’applique à : Advanced Threat Analytics version 1.7*



# Définition des notifications ATA
ATA peut vous avertir quand il détecte une activité suspecte, par courrier électronique ou en utilisant le transfert d’événements ATA et en transférant l’événement à votre serveur SIEM/syslog. Avant de sélectionner les notifications à recevoir, vous devez [configurer votre serveur de messagerie et votre serveur Syslog](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   Les notifications par courrier électronique incluent un lien qui dirige l’utilisateur directement vers l’activité suspecte qui a été détectée. La partie nom d’hôte du lien provient du paramètre de l’URL de la console ATA dans la page Centre ATA. Par défaut, l’URL de la console ATA est l’adresse IP sélectionnée pendant l’installation du centre ATA.  Si vous envisagez de configurer des alertes par courrier électronique, nous vous recommandons d’utiliser un nom de domaine complet comme URL de la console ATA.
> -   Les notifications sont envoyées à partir du centre ATA vers le serveur SMTP ou le serveur Syslog.

## Notifications par e-mail
Pour recevoir des notifications par e-mail, procédez comme suit :


1. Dans la console ATA, sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.
![Icône des paramètres de configuration ATA](media/ATA-config-icon.JPG)

2. Dans la section **Notifications**, sélectionnez **Paramètres**.
3. Sous **Destinataires du courrier**, spécifiez les destinataires qui recevront les notifications par e-mail.

    [!Remarque :]Les alertes par e-mail pour les activités suspectes sont envoyées uniquement au moment de la création de l’activité suspecte.

4. Sous **Notifier quand**, utilisez les boutons bascule pour sélectionner les notifications à envoyer :

    - Une nouvelle activité suspecte est détectée
    - Un nouveau problème d’intégrité a été détecté
    - Une mise à jour logicielle est disponible

5. Cliquez sur **Enregistrer**.

![Image des paramètres de notification par e-mail ATA](media/ATA-mail-notification-settings-1.7.png)


## Notification Syslog

Pour recevoir les notifications Syslog, procédez comme suit :


1. Dans la console ATA, sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.
![Icône des paramètres de configuration ATA](media/ATA-config-icon.JPG)

2. Dans la section **Notifications**, sélectionnez **Paramètres**.
3. Sous **Notifications Syslog**, utilisez les bascules pour sélectionner les notifications à envoyer :


    - Une nouvelle activité suspecte est détectée
    - Une activité suspecte est mise à jour
    - Un nouveau problème d’intégrité a été détecté
5. Cliquez sur **Enregistrer**.
![Image des paramètres de notification ATA](media/ATA-syslog-notification-settings-1.7.png)




## Voir aussi
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->


