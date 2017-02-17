---
title: "Définir des notifications Advanced Threat Analytics | Microsoft Docs"
description: "Décrit comment définir des alertes ATA afin d’être averti quand des activités suspectes sont détectées."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 782c066e6a7ef8a5da9e2b8ceb16742da6f52506


---

*S’applique à : Advanced Threat Analytics version 1.7*



# <a name="set-ata-notifications"></a>Définir des notifications ATA
ATA peut vous avertir quand il détecte une activité suspecte par e-mail ou en utilisant le transfert d’événements ATA et en transférant l’événement à votre serveur SIEM/syslog. Avant de sélectionner les notifications à recevoir, vous devez [configurer votre serveur de messagerie et votre serveur Syslog](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   Les notifications par e-mail incluent un lien qui dirige l’utilisateur directement vers l’activité suspecte qui a été détectée. La partie nom d’hôte du lien provient du paramètre de l’URL de la console ATA dans la page Centre ATA. Par défaut, l’URL de la console ATA est l’adresse IP sélectionnée pendant l’installation du centre ATA.  Si vous envisagez de configurer des alertes par e-mail, nous vous recommandons d’utiliser un nom de domaine complet comme URL de la console ATA.
> -   Les notifications sont envoyées à partir du centre ATA vers le serveur SMTP ou le serveur Syslog.

## <a name="mail-notifications"></a>Notifications par e-mail
Pour recevoir des notifications par e-mail, procédez comme suit :


1. Dans la console ATA, sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.
![Icône des paramètres de configuration ATA](media/ATA-config-icon.JPG)

2. Dans la section **Notifications**, sélectionnez **Paramètres**.
3. Sous **Destinataires du courrier**, spécifiez les destinataires qui recevront les notifications par e-mail.
>   [!NOTE]
>   Les alertes par e-mail pour les activités suspectes sont envoyées uniquement lors de la création de l’activité suspecte.

4. Sous **Notifier quand**, utilisez les boutons bascule pour sélectionner les notifications à envoyer :
  - Une nouvelle activité suspecte est détectée
  - Un nouveau problème d’intégrité a été détecté
  - Une mise à jour logicielle est disponible

5. Cliquez sur **Enregistrer**.

![Image des paramètres de notification par e-mail ATA](media/ATA-mail-notification-settings-1.7.png)


## <a name="syslog-notification"></a>Notification Syslog

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




## <a name="see-also"></a>Voir aussi
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO1-->


