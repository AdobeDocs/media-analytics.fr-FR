---
title: Durée totale de l'image dans l'image
description: Indique le nombre de secondes cumulées passées par la visionneuse dans la capture d’images au cours d’une session.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 6%

---


# Durée totale de l&#39;image dans l&#39;image

>[!BEGINSHADEBOX]

*Cette page couvre la mesure de reporting **Durée totale de l’image dans l’image**. Voir [Image dans l’image](/help/implementation/variables/player-state/picture-in-picture.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La mesure **Durée totale de l’image dans l’image** indique le temps cumulé, en secondes, que le lecteur a passé en mode image dans l’image au cours d’une session. Le serveur principal additionne chaque intervalle entre un événement de début d’état image dans image et l’événement de fin d’état correspondant.

## Méthode de calcul de cette mesure

Le serveur principal du média additionne le temps écoulé sur tous les intervalles image par image au cours de la session. La mesure est signalée lors de l’appel de fermeture. Analysis Workspace affiche la valeur en tant que `HH:MM:SS` ; les flux de données, Data Warehouse et les API de création de rapports affichent la valeur en secondes.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.states.pictureinpicture.time` de données contextuelles lorsque le [[!UICONTROL suivi de l’état du lecteur]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) l’entrée où `name = "pictureInPicture"`, champ `time` |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
