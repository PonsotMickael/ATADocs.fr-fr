---
# required metadata

title: FAQ technique sur ATA | Microsoft Advanced Threat Analytics
description: Fournit des réponses aux questions les plus fréquentes sur ATA
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# FAQ technique sur ATA
Cet article fournit des éléments d’informations et des réponses aux questions les plus fréquentes sur ATA.

## Forum Aux Questions : ATA

|Question|Réponses|
|------------|-----------------------------------|
|La passerelle ATA ne démarre pas, que dois-je faire ?|Examinez l’erreur la plus récente dans le journal des erreurs actuel (où ATA est installé, sous le dossier « Logs »).|
|Comment puis-je tester ATA ?|Vous pouvez simuler des activités suspectes (test de bout en bout) en effectuant l’une des opérations suivantes :<br /><br />1.  Reconnaissance DNS à l’aide de Nslookup.exe<br />2.  Exécution à distance à l’aide de psexec.exe<br /><br />Ce programme doit s’exécuter sur le contrôleur de domaine surveillé, et non à partir de la passerelle ATA.|
|Comment vérifier le transfert d’événements Windows ?|Vous pouvez exécuter ce qui suit à partir d’une invite de commandes dans le répertoire **\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** :<br /><br />mongo ATA --eval "printjson(db.getCollectionNames())" &#124; find /C "NtlmEvents"`|
|ATA prend-il en charge le trafic chiffré ?|Le trafic chiffré n’est pas analysé (par exemple : LDAPS, ESP IPSEC).|
|ATA fonctionne-t-il avec le blindage Kerberos ?|L’activation du blindage Kerberos (également appelé FAST [Flexible Authentication Secure Tunneling]) est prise en charge par ATA, à l’exception de la détection Overpass-the-Hash qui ne fonctionne pas.|
|De combien de passerelles ATA ai-je besoin ?|Quand vous estimez le nombre de passerelles qu’il vous faut, vous devez prendre en compte les deux éléments suivants :<br /><br />- D’un point de vue des performances, le trafic total généré par vos contrôleurs de domaine détermine le nombre minimum de passerelles ATA dont vous avez besoin pour gérer votre environnement Active Directory.<br />    Pour en savoir plus sur la façon de déterminer le volume de trafic généré par vos contrôleurs de domaine, consultez [Planification de la capacité ATA](/advanced-threat-analytics/PlanDesign/ata-capacity-planning).<br />- Les limites opérationnelles de la mise en miroir des ports affectent aussi le nombre de passerelles ATA dont vous avez besoin pour prendre en charge tous vos contrôleurs de domaine (par exemple : par commutateur, par centre de données ou par région). Chaque environnement a ses propres spécificités.|
|Quelles sont les exigences imposées par ATA en matière d’espace de stockage ?|Pour chaque journée complète produisant en moyenne 1 000 paquets/s, il vous faut 1,5 Go de stockage.<br /><br />Pour plus d’informations, consultez [Planification de la capacité ATA](/advanced-threat-analytics/PlanDesign/ata-capacity-planning).|
|Pourquoi certains comptes sont-ils sensibles ?|Cela arrive quand un compte est membre de certains groupes désignés comme sensibles (par exemple : « Administrateurs du domaine »).<br />Pour comprendre pourquoi un compte est sensible, vous pouvez examiner son appartenance au groupe pour déterminer à quels groupes sensibles il appartient. Le groupe auquel il appartient peut également être sensible en raison d’un autre groupe ; dans ce cas, répétez la procédure jusqu’à ce que vous trouviez le groupe sensible de plus haut niveau.|
|Comment puis-je surveiller un contrôleur de domaine virtuel ?|Vous pouvez avoir une passerelle ATA virtuelle ou physique, comme décrit dans [Configurer la mise en miroir des ports](/advanced-threat-analytics/PlanDesign/configure-port-mirroring).  <br />Le moyen le plus simple consiste à configurer une passerelle ATA virtuelle sur chaque hôte où figure un contrôleur de domaine virtuel.<br />Si vos contrôleurs de domaine virtuels passent d’un hôte à l’autre, vous devez effectuer l’une des opérations suivantes :<br /><br />- Quand le contrôleur de domaine virtuel passe à un autre hôte, préconfigurez la passerelle ATA sur cet hôte pour qu’elle reçoive le trafic du contrôleur de domaine virtuel ayant récemment été déplacé.<br />- Veillez à associer la passerelle ATA virtuelle avec le contrôleur de domaine virtuel. Ainsi, s’il est déplacé, la passerelle ATA est déplacée en même temps.<br />- Certains commutateurs virtuels peuvent envoyer le trafic entre les hôtes.|
|Comment puis-je sauvegarder ATA ?|Il y a deux éléments que vous devez sauvegarder :<br /><br />- La configuration d’ATA, qui est stockée dans la base de données et qui est automatiquement sauvegardée toutes les heures. <br />- Le trafic et les événements enregistrés par ATA, que vous pouvez sauvegarder à l’aide de n’importe quelle procédure de sauvegarde de base de données prise en charge. Pour plus d’informations, consultez [Gestion de la base de données ATA](/advanced-threat-analytics/DeployUse/ata-database-management)|
|Que peut détecter ATA ?|Pour obtenir la liste complète des éléments détectés par ATA, consultez [Qu’est-ce que Microsoft Advanced Threat Analytics ?](/advanced-threat-analytics/Understand/what-is-ata).|
|De quel type de stockage ai-je besoin pour ATA ?|Nous vous recommandons d’utiliser une solution de stockage rapide (pas des disques 7200 tr/min) avec une faible latence (inférieure à 10 ms) et une configuration RAID qui prend en charge des charges d’écriture intensives (pas les niveaux 5/6 de RAID et leurs dérivés).|
|De combien de cartes réseau la passerelle ATA a-t-elle besoin ?|La passerelle ATA a besoin au minimum de deux cartes réseau :<br>1. Une carte réseau pour se connecter au réseau interne et au centre ATA.<br>2. Une carte réseau pour capturer le trafic réseau des contrôleurs de domaine par le biais de la mise en miroir des ports.<br>* Ceci ne s’applique pas à la passerelle légère.|
|De quelle façon ATA s’intègre-t-il aux serveurs SIEM ?|ATA bénéficie d’une intégration bidirectionnelle aux serveurs SIEM, comme suit :<br>
1. Vous pouvez configurer ATA de façon à envoyer une alerte Syslog en cas d’activité suspecte à n’importe quel serveur SIEM prenant en charge le format CEF.<br>2. Vous pouvez configurer ATA de façon à recevoir des messages Syslog pour chaque événement Windows associé à l’ID 4776 à partir de [ces serveurs SIEM](/advanced-threat-analytics/PlanDesign/configure-event-collection#SIEMsupport).|


<!--HONumber=Apr16_HO2-->


