---
title: "Configurer votre proxy ou pare-feu pour permettre la communication d’Azure ATP avec le capteur | Microsoft Docs"
description: "Décrit comment configurer votre pare-feu ou proxy pour permettre la communication entre le service cloud Azure ATP et les capteurs Azure ATP"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/3/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f077bbd9990affbb6c552c5ad8875fdfebbd70f2
ms.sourcegitcommit: 84556e94a3efdf20ca1ebf89a481550d7f8f0f69
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/08/2018
---
*S’applique à : Azure - Protection avancée contre les menaces*



# <a name="configure-your-proxy-to-allow-communication-between-azure-atp-sensors-and-the-azure-atp-cloud-service"></a>Configurer votre proxy pour permettre la communication entre les capteurs Azure ATP et le service cloud Azure ATP

Pour que vos contrôleurs de domaine communiquent avec le service cloud, vous devez ouvrir le port 443 *.atp.azure.com dans votre pare-feu ou proxy. La configuration doit être effectuée au niveau de l’ordinateur (= compte d’ordinateur) et non pas au niveau du compte d’utilisateur. Vous pouvez tester votre configuration en procédant comme suit :
 
1.  Vérifiez que l’**utilisateur actuel** a accès au point de terminaison de processeur à l’aide d’Internet Explorer, en accédant à l’URL suivante à partir du contrôleur de domaine : https://triprd1wcuse1sensorapi.eastus.cloudapp.azure.com (pour les États-Unis). Vous devez obtenir l’erreur 503 :

 ![service non disponible](./media/service-unavailable.png)
 
2.  Si vous n’obtenez pas l’erreur 503, passez en revue la configuration du proxy, puis réessayez.

3.  Si la configuration du proxy fonctionne pour **CURRENT_USER** (autrement dit, vous voyez l’erreur 503), vérifiez si les paramètres du proxy WinInet sont activés pour le compte **LOCAL_SYSTEM** (utilisé par le service de mise à jour de capteur) en exécutant la commande suivante dans une invite de commandes avec élévation de privilèges :
 
    reg compare "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" "HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" /v DefaultConnectionSettings

Si vous obtenez l’erreur «Erreur : le système n'a pas trouvé la clé ou la valeur de Registre spécifiée. », cela signifie qu’aucun proxy n’a été défini au niveau **LOCAL_SYSTEM**.
 
 ![erreur de système local proxy](./media/proxy-local-system-error.png)

Si le résultat est « Résultat comparé : Différent », cela signifie que le proxy est défini pour **LOCAL_SYSTEM**, mais qu’il n’est pas le même que **CURRENT_USER** :
 
  ![résultat de proxy comparé](./media/proxy-result-compared.png)

5.  Si **LOCAL_SYSTEM** n’a pas les paramètres de proxy appropriés (non configurés ou différents de **CURRENT_USER**), vous pouvez être amené à copier le paramètre de proxy de **CURRENT_USER** pour **LOCAL_SYSTEM**. Veillez à sauvegarder cette clé de Registre avant de la modifier :

 Clé de l’utilisateur actuel : HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings” Clé du système local : HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings”

 
6.  Effectuez les étapes 4 et 5 pour le compte **Local_Service** (il est identique à **Local_System** mais doit être S-1-5-19 au lieu de S-1-5-18).



## <a name="see-also"></a>Voir aussi
- [Configurer le transfert d’événements](configure-event-forwarding.md)
- [Consulter le forum ATP](https://aka.ms/azureatpcommunity)