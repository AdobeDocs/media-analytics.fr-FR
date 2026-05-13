---
title: Position de l’annonce publicitaire dans la capsule
description: Indique la position de chaque publicité indexée sur zéro à l’intérieur de sa coupure publicitaire parente.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 6%

---


# Position de l’annonce publicitaire dans la capsule

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Position de l’annonce publicitaire dans la capsule**. Consultez [Position de l’annonce publicitaire dans la capsule](/help/implementation/variables/ads/ad-in-pod-position.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Position de l’annonce publicitaire dans la capsule** indique la position à indexation zéro de chaque annonce publicitaire dans sa coupure publicitaire parente. La première publicité d&#39;un pod est `0`, la deuxième est `1`, et ainsi de suite. Utilisez la dimension pour comparer l’engagement et l’achèvement par position au sein d’une coupure publicitaire.

## Mode de remplissage de cette dimension

La position de l’annonce publicitaire dans la capsule est définie par le lecteur à chaque événement `media.adStart`.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.ad.podPosition` de données contextuelles lorsque [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.podPosition`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Flux de données | `videoadinpod, post_videoadinpod` |

## Éléments de dimension

Chaque élément est la valeur de position entière (`0`, `1`, `2`, etc.) signalé le `media.adStart`.
