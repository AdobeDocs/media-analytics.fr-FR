---
title: Bloquer les flux impactés
description: Comptabilise les sessions au cours desquelles au moins un blocage s’est produit lors de la lecture.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 8%

---


# Bloquer les flux impactés

La mesure **Blocage des flux impactés** comptabilise les sessions dans lesquelles au moins un blocage s’est produit pendant la lecture. La mesure est un booléen au niveau de la session : plusieurs blocages au sein du même nombre de sessions sont comptabilisés comme un flux impacté. Pour le volume total de décrochage, utilisez [Événements de décrochage](stall-events.md).

## Méthode de calcul de cette mesure

Le serveur principal du média définit cet indicateur lorsqu’aucun mouvement de tête de lecture n’est enregistré sur le contenu principal pendant au moins trois événements consécutifs au cours de la session. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Créez une [règle de traitement](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.qoe.stall` à un événement personnalisé. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasStallImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (événement personnalisé auquel votre règle de traitement `a.media.qoe.stall` mappe ; voir recherche [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.stall` |
