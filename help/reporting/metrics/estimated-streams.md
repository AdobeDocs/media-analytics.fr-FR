---
title: Flux estimés
description: Estime le nombre de flux audio ou vidéo par session.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 10%

---


# Flux estimés

La mesure **Flux estimés** se rapproche du nombre de flux audio ou vidéo par session, un flux étant comptabilisé toutes les 30 minutes de lecture totale. Il est destiné aux accords de syndication de contenu et aux approximations où chaque bloc de consommation de 30 minutes compte comme un « flux » distinct.

## Méthode de calcul de cette mesure

Le serveur principal des médias calcule `mediaReporting.sessionDetails.estimatedStreams = FLOOR(totalTimePlayed / 1800) + 1`, où `totalTimePlayed` correspond [Temps passé sur les médias](media-time-spent.md) en secondes. La mesure est signalée lors de l’appel de fermeture.

| Temps passé sur le média | Flux estimés |
| --- | --- |
| 0-29 min | 1 |
| 30-59 min | 2 |
| 60-89 min | 3 |
| 90+ min | 4+ |

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Créez une [règle de traitement](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.estimatedStreams` à un événement personnalisé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.estimatedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (événement personnalisé auquel votre règle de traitement `a.media.estimatedStreams` mappe ; voir recherche [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.estimatedStreams` |
