---
title: Durée totale du blocage
description: Indique le temps de blocage cumulé pour les sommes et les moyennes entre les sessions.
feature: Metrics
role: User, Admin
source-git-commit: 1278355e0bfc67c635250c426edaf865fb658c37
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 7%

---


# Durée totale du blocage

La mesure **Durée totale du blocage** indique le temps de blocage cumulé entre les sessions, approprié pour les sommes, les moyennes et les cumuls de centiles. Utilisez la mesure pour calculer le temps total passé par les visionneuses à attendre une lecture bloquée au cours d’une période de rapport.

Dans Customer Journey Analytics, `mediaReporting.qoeDataDetails.stallTime` peut être utilisé comme mesure ou comme dimension sans composant de dimension distinct.

## Méthode de calcul de cette mesure

Le serveur principal du média additionne la durée de chaque intervalle de blocage, détecté lorsqu’aucun mouvement de tête de lecture n’est enregistré sur le contenu principal pendant au moins trois événements consécutifs. La mesure est signalée lors de l’appel de fermeture. Analysis Workspace affiche la valeur en tant que `HH:MM:SS` ; les flux de données, Data Warehouse et les API de création de rapports affichent la valeur en secondes.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.qoe.stallTime` à un événement personnalisé. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.stallTime`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (événement personnalisé auquel votre règle de traitement `a.media.qoe.stallTime` mappe ; voir recherche [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.stallTime` |
