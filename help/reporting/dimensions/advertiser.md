---
title: Annonceur
description: Indique la société ou la marque apparaissant dans chaque publicité.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 11%

---


# Annonceur

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Annonceur**. Voir [Advertiser](/help/implementation/variables/ads/advertiser.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Annonceur** indique la société ou la marque présentée dans chaque publicité (par exemple, `"Ford"` ou `"Coca-Cola"`). Utilisez la dimension pour ventiler l’engagement et l’achèvement par l’annonceur.

## Mode de remplissage de cette dimension

L’annonceur est défini par le lecteur à chaque événement `media.adStart`.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.ad.advertiser` de données contextuelles lorsque [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.advertiser`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Flux de données | `videoadvertiser, post_videoadvertiser` |

## Éléments de dimension

Chaque élément correspond au nom littéral de l’annonceur signalé sur `media.adStart`.
