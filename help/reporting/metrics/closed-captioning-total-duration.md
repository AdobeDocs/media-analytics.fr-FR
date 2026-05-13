---
title: Durée totale du sous-titrage
description: Indique que les légendes de secondes cumulées ont été activées au cours d’une session.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 7%

---


# Durée totale du sous-titrage

>[!BEGINSHADEBOX]

*Cette page couvre la mesure de création de rapports **Durée totale du sous-titrage**. Voir [Sous-titrage](/help/implementation/variables/player-state/closed-captioning.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La mesure **Durée totale du sous-titrage codé** indique la durée cumulée, en secondes, pendant laquelle les sous-titres ont été activés au cours d’une session. Le serveur principal additionne chaque intervalle entre un événement de début d’état activé pour les légendes et l’événement de fin d’état correspondant.

## Méthode de calcul de cette mesure

Le serveur principal du média additionne le temps écoulé sur tous les intervalles activés pour les sous-titres pendant la session. La mesure est signalée lors de l’appel de fermeture. Analysis Workspace affiche la valeur en tant que `HH:MM:SS` ; les flux de données, Data Warehouse et les API de création de rapports affichent la valeur en secondes.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.states.closedcaptioning.time` de données contextuelles lorsque le [[!UICONTROL suivi de l’état du lecteur]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/media-reporting-details) l’entrée où `name = "closedCaptioning"`, champ `time` |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
