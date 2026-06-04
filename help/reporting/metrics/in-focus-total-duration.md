---
title: Durée totale du focus
description: Indique le nombre de secondes cumulées pendant lesquelles le lecteur a reçu le focus au cours d’une session.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 8%

---


# Durée totale du focus

>[!BEGINSHADEBOX]

*Cette page couvre la mesure de reporting **Durée totale du focus**. Voir [En bref](/help/implementation/variables/player-state/in-focus.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La mesure **Durée totale du focus** indique le temps cumulé, en secondes, pendant lequel le lecteur a été ciblé au cours d’une session. Le serveur principal additionne chaque intervalle entre un événement de début d’état de focus et l’événement de fin d’état correspondant.

## Méthode de calcul de cette mesure

Le serveur principal du média additionne le temps écoulé sur tous les intervalles ciblés pendant la session. La mesure est signalée lors de l’appel de fermeture. Analysis Workspace affiche la valeur en tant que `HH:MM:SS` ; les flux de données, Data Warehouse et les API de création de rapports affichent la valeur en secondes.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.states.infocus.time` de données contextuelles lorsque le [[!UICONTROL suivi de l’état du lecteur]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/media-reporting-details) l’entrée où `name = "inFocus"`, champ `time` |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.infocus.time` |
