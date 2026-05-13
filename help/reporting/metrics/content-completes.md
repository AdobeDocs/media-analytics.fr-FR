---
title: Content completes
description: Comptabilise les sessions dont le curseur de lecture a atteint la fin du contenu.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 9%

---


# Content completes

La mesure **Contenu terminé** comptabilise les sessions dont le curseur de lecture a atteint la fin du contenu. Associez-le à [démarrages du contenu](content-starts.md) pour calculer le taux d’achèvement ; associez-le à [démarrages du média](media-starts.md) pour calculer le taux d’affichage de bout en bout.

## Méthode de calcul de cette mesure

Le serveur principal du média se `mediaReporting.sessionDetails.isCompleted = true` lorsqu’un événement de `media.sessionComplete` est reçu. La mesure est signalée lors de l’appel de fermeture. Une session qui expire sans `sessionComplete` explicite n’est pas comptabilisée comme une fin de session.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.complete` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isCompleted`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
