---
title: Annonces démarrées
description: Comptabilise chaque publicité ayant commencé à être lue au cours d’une session.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 10%

---


# Annonces démarrées

La mesure **Publicités démarrées** comptabilise chaque publicité qui a commencé à être lue au cours d’une session. Associez-la à [Fin de la publicité](ad-completes.md) pour calculer le taux de fin de la publicité, ainsi qu’à [Nombre de publicités](/help/reporting/metrics/ad-count.md) pour le cumul au niveau de la session équivalent.

## Méthode de calcul de cette mesure

Le serveur principal du média se `mediaReporting.advertisingDetails.isStarted = true` lorsqu’un événement de `media.adStart` est reçu. La mesure est signalée lors de l’appel de démarrage de la publicité.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.ad.view` de données contextuelles lorsque [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.isStarted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
