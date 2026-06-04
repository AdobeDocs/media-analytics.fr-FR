---
title: Durée totale en plein écran
description: Indique le nombre de secondes cumulées passées par la visionneuse en plein écran au cours d’une session.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 8%

---


# Durée totale en plein écran

>[!BEGINSHADEBOX]

*Cette page couvre la mesure de reporting **Durée totale du plein écran**. Voir [Plein écran](/help/implementation/variables/player-state/full-screen.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La mesure **Durée totale du plein écran** indique le temps cumulé, en secondes, que la visionneuse a passé en plein écran au cours d’une session. Le serveur principal additionne chaque intervalle entre un événement de début d’état plein écran et l’événement de fin d’état correspondant.

## Méthode de calcul de cette mesure

Le serveur principal du média additionne le temps écoulé sur tous les intervalles en plein écran pendant la session. La mesure est signalée lors de l’appel de fermeture. Analysis Workspace affiche la valeur en tant que `HH:MM:SS` ; les flux de données, Data Warehouse et les API de création de rapports affichent la valeur en secondes.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.states.fullscreen.time` de données contextuelles lorsque le [[!UICONTROL suivi de l’état du lecteur]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) l’entrée où `name = "fullscreen"`, champ `time` |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.time` |
