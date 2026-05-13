---
title: Visionneuses simultanées de médias
description: Découvrez le tableau de bord des visionneuses simultanées de médias utilisé pour afficher les visionneuses simultanées pendant une journée. Les données peuvent être filtrées par contenu, type d’appareil ou pays.
uuid: e61c50e5-8196-4538-b67c-ebc01c6e6ba7
exl-id: 2c679c1a-a4bd-44fc-8e11-173c8544ab06
feature: Streaming Media, Workspace Basics
role: User, Admin
TQID: https://experienceleague.adobe.com/8pqoGpVCRXvovD-cNPNOvFQFvJco3sWUq3SuXEOVeJI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e38cbddc-1633-4cd5-bed5-9f289f2a6029
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 299
ht-degree: 91%

---

# Rapports des visionneuses simultanées de médias {#media-concurrent-viewers}

Le tableau de bord des visionneuses simultanées de médias affiche les visiteurs simultanés pendant une journée. Les données peuvent être filtrées par contenu, type d’appareil ou pays.

>[!TIP]
>
> Ce rapport est basé sur des sessions de médias actives simultanées.  Pour afficher les observateurs simultanés par visiteur unique, avec les fonctionnalités supplémentaires d’application d’un segment, de ventilation et de comparaison, utilisez le [Panneau Observateurs simultanés de médias dans Analysis Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers.html?lang=fr).
>

![](assets/video-concurrent-viewers.png)

## Fonctionnalités du rapport {#report-features}

Voici quelques caractéristiques de ce rapport :

* Il n’est pas en temps réel. Il présente une latence normale dans Adobe Analytics.
* Le rapport couvre une période de 24 heures. L’axe X est l’heure de la journée en fonction du fuseau horaire de la suite de rapports.
* Cette option affiche les vues simultanées avec une granularité par minute.
* Il existe un rapport *Visionneuses simultanées de médias* qui montre le nombre de visiteurs qui regardent ou écoutent tout le contenu.
* Le rapport *Détails du média* contient un rapport Visionneuses simultanées qui indique le nombre de visiteurs qui regardent ou écoutent un élément multimédia spécifique.
* Le rapport ne fonctionne que sur une seule journée.
* Le client peut examiner les rapports de visionneuses simultanées historiques (limités à un seul jour).

## Limites {#limitations}

Voici quelques limites de ce rapport :

* Aucune donnée ne s’affiche si l’intervalle sélectionné n’est pas un jour entier.
* Vous ne pouvez pas exporter les données, telles que ReportBuilder.
* Vous ne pouvez pas présenter les données sous forme de tableau.
* Vous ne pouvez pas envoyer de rapport par email.
* Même si vous n’effectuez pas le suivi des publicités, vous devez réactiver le suivi des médias et sélectionner le module Media Ad.
* Cette fonctionnalité fournit des données précises lors de l’utilisation d’une bibliothèque de pulsations dotée de fonctionnalités de suivi Pause.
