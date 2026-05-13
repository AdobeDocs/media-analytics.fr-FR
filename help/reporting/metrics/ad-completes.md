---
title: Fin de la publicité
description: Comptabilise chaque publicité lue jusqu’à la fin.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 11%

---


# Fin de la publicité

La mesure **Publicité terminée** comptabilise chaque publicité lue jusqu’à la fin. Associez-le à [Lancements de l’annonce publicitaire](ad-starts.md) pour calculer le taux d’achèvement de l’annonce publicitaire.

## Méthode de calcul de cette mesure

Le serveur principal du média se `mediaReporting.advertisingDetails.isCompleted = true` lorsqu’un événement de `media.adComplete` est reçu. La mesure est signalée lors de l’appel de fermeture de la publicité. Les publicités ignorées ou abandonnées ne sont pas considérées comme terminées.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.ad.complete` de données contextuelles lorsque [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.isCompleted`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
