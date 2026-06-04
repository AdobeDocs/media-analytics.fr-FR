---
title: Fin de la publicité
description: Comptabilise chaque publicité lue jusqu’à la fin.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 12%

---


# Fin de la publicité

La mesure **Publicité terminée** comptabilise chaque publicité lue jusqu’à la fin. Associez-le à [Lancements de l’annonce publicitaire](ad-starts.md) pour calculer le taux d’achèvement de l’annonce publicitaire.

## Méthode de calcul de cette mesure

Le serveur principal du média définit cet indicateur lorsqu’un événement [fin de la publicité](/help/implementation/events/ads/ad-complete.md) est reçu. La mesure est signalée lors de l’appel de fermeture de la publicité. Les publicités ignorées ou abandonnées ne sont pas considérées comme terminées.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.ad.complete` de données contextuelles lorsque [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.isCompleted`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.ad.complete` |
