---
title: Annonces démarrées
description: Comptabilise chaque publicité ayant commencé à être lue au cours d’une session.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 11%

---


# Annonces démarrées

La mesure **Publicités démarrées** comptabilise chaque publicité qui a commencé à être lue au cours d’une session. Associez-la à [Fin de la publicité](ad-completes.md) pour calculer le taux de fin de la publicité, ainsi qu’à [Nombre de publicités](/help/reporting/metrics/ad-count.md) pour le cumul au niveau de la session équivalent.

## Méthode de calcul de cette mesure

Le serveur principal du média définit cet indicateur lorsqu’un événement [début de la publicité](/help/implementation/events/ads/ad-start.md) est reçu. La mesure est signalée lors de l’appel de démarrage de la publicité.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.ad.view` de données contextuelles lorsque [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.isStarted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.ad.view` |
