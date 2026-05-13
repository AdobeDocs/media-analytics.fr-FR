---
title: ID de campagne
description: Indique la campagne à laquelle appartient chaque annonce publicitaire.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 12%

---


# ID de campagne

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Identifiant de campagne**. Voir [Identifiant de campagne](/help/implementation/variables/ads/campaign-id.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Identifiant de campagne** indique la campagne publicitaire à laquelle chaque contenu publicitaire appartient. Utilisez la dimension pour cumuler l’engagement de plusieurs créatifs qui partagent une campagne.

## Mode de remplissage de cette dimension

L’identifiant de campagne est défini par le lecteur à chaque événement `media.adStart`.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.ad.campaign` de données contextuelles lorsque [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.campaignID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Flux de données | `videocampaign, post_videocampaign` |

## Éléments de dimension

Chaque élément correspond à la valeur de campagne littérale signalée sur `media.adStart`.
