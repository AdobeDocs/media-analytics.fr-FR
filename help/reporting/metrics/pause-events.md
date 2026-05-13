---
title: Événements Pause
description: Compte chaque pause distincte qui s’est produite au cours d’une session.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 10%

---


# Événements Pause

La mesure **Événements de pause** comptabilise chaque événement de `media.pauseStart` distinct reçu au cours d’une session, y compris plusieurs pauses au cours de la même session. Associez-la à [ Durée totale de pause ](total-pause-duration.md) pour obtenir la durée moyenne de pause, ainsi qu’à [ Flux impactés par la pause ](paused-impacted-streams.md) pour compter les sessions qui se sont interrompues au moins une fois.

## Méthode de calcul de cette mesure

Le serveur principal du média est incrémenté `mediaReporting.sessionDetails.pauseCount` chaque événement `media.pauseStart`. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.pauseCount` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.pauseCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
