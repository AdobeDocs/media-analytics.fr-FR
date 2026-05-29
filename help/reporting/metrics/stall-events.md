---
title: Événements de blocage
description: Comptabilise les événements de blocage pour les sommes et les moyennes entre les sessions.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 7%

---


# Événements de blocage

La mesure **Événements de blocage** comptabilise les événements de blocage entre les sessions, adaptés aux sommes, aux moyennes et aux cumuls de centiles. Utilisez cette mesure pour calculer le volume total de décrochage au cours d’une période de rapport et pour comparer la stabilité du décrochage sur l’ensemble du contenu, des réseaux ou des lecteurs.

Dans Customer Journey Analytics, `xdm.mediaReporting.qoeDataDetails.stallCount` peut être utilisé comme mesure ou comme dimension sans composant de dimension distinct.

## Méthode de calcul de cette mesure

Le serveur principal du média incrémente le nombre chaque fois qu’aucun mouvement de tête de lecture n’est enregistré sur le contenu principal pendant au moins trois événements consécutifs. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Créez une [règle de traitement](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.qoe.stallCount` à un événement personnalisé. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.stallCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (événement personnalisé auquel votre règle de traitement `a.media.qoe.stallCount` mappe ; voir recherche [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.stallCount` |

Pour les rapports booléens au niveau de la session (si un blocage s’est produit), utilisez [Bloquer les flux impactés](stall-impacted-streams.md).
