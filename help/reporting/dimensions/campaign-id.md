---
title: ID de campagne
description: Indique la campagne à laquelle appartient chaque annonce publicitaire.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 13%

---


# ID de campagne

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Identifiant de campagne**. Voir [Identifiant de campagne](/help/implementation/variables/ads/campaign-id.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Identifiant de campagne** indique la campagne publicitaire à laquelle chaque contenu publicitaire appartient. Utilisez la dimension pour cumuler l’engagement de plusieurs créatifs qui partagent une campagne.

## Mode de remplissage de cette dimension

L’identifiant de campagne est défini par le lecteur à chaque événement [début de la publicité](/help/implementation/events/ads/ad-start.md).

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.ad.campaign` de données contextuelles lorsque [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.campaignID`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Flux de données | `videocampaign`, `post_videocampaign` |
| Audience Manager | `c_contextdata.a.media.ad.campaign` |

## Éléments de dimension

Chaque élément correspond à la valeur de campagne littérale signalée au [début de la publicité](/help/implementation/events/ads/ad-start.md).
