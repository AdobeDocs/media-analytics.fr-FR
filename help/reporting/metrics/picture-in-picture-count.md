---
title: Image dans le nombre d’images
description: Indique le nombre de fois que la visionneuse a effectué une saisie d’image en image au cours d’une session.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 8%

---


# Image dans le nombre d’images

>[!BEGINSHADEBOX]

*Cette page couvre la mesure de reporting **Nombre d’images**Image dans . Voir [Image dans l’image](/help/implementation/variables/player-state/picture-in-picture.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La mesure **Nombre d’images dans l’image** indique le nombre de fois que la visionneuse a effectué une lecture d’image dans l’image au cours d’une session. Chaque événement de début d’état image dans image incrémente le nombre. Associez avec [Flux impactés par l’image dans l’image](picture-in-picture-streams-impacted.md) pour les cumuls booléens au niveau de la session et avec [Durée totale de l’image dans l’image](picture-in-picture-total-duration.md) pour la durée totale à l’état.

## Méthode de calcul de cette mesure

Le serveur principal du média incrémente le champ `count` dans l’entrée `pictureInPicture` de `mediaReporting.states[]` sur chaque événement de début d’état image dans image. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.states.pictureinpicture.count` de données contextuelles lorsque le [[!UICONTROL suivi de l’état du lecteur]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) l’entrée où `name = "pictureInPicture"`, champ `count` |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.count` |
