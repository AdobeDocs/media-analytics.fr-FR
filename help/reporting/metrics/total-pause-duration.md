---
title: Durée totale de la pause
description: Indique le nombre cumulé de secondes passées par la visionneuse en pause au cours d’une session.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 10%

---


# Durée totale de la pause

La mesure **Durée totale de pause** indique le nombre cumulé de secondes que la visionneuse a passées en pause au cours d’une session. La mesure correspond à la somme de tous les intervalles entre chaque événement [pause start](/help/implementation/events/playback/pause-start.md) et l’événement [play](/help/implementation/events/playback/play.md) suivant. Plusieurs pauses sont ajoutées ensemble. Associez à [Événements Pause](pause-events.md) pour obtenir la durée moyenne de la pause.

## Méthode de calcul de cette mesure

Le serveur principal du média additionne le temps écoulé entre chaque événement [pause start](/help/implementation/events/playback/pause-start.md) et l’événement [play](/help/implementation/events/playback/play.md) correspondant. La mesure est signalée lors de l’appel de fermeture. La valeur s’affiche sous la forme `HH:MM:SS` dans Analysis Workspace et en secondes dans les autres applications.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.pauseTime` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.pauseTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | S.O. |
