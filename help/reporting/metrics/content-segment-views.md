---
title: Vues de segment de contenu
description: Comptabilise les segments dans lesquels la lecture du contenu principal actif a eu lieu.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 9%

---


# Vues de segment de contenu

La mesure **Vues des segments de contenu** comptabilise les segments de contenu de cinq minutes dans lesquels la lecture du contenu principal actif a eu lieu. La mesure confirme que la visionneuse a lu du contenu dans ce segment au lieu de simplement le charger ou de le mettre en mémoire tampon. Associez-le à la dimension [Segment de contenu](/help/reporting/dimensions/content-segment.md) pour ventiler les parties réellement consommées par les visionneuses de contenu de forme longue.

## Méthode de calcul de cette mesure

Le serveur principal du média définit cet indicateur pour tout appel de fermeture qui couvre un segment dans lequel au moins un événement [play](/help/implementation/events/playback/play.md) pour le contenu principal a été reçu. La mesure est signalée lors de l’appel de fermeture. Sur le chemin d’accès de l’API Media Edge, les vues de segment se déclenchent dans la même condition que les démarrages de contenu. Les deux nécessitent un événement [play](/help/implementation/events/playback/play.md) sur le contenu principal.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.segmentView` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasSegmentView`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | S.O. |
