---
title: Nombre d’annonces
description: Indique le nombre de publicités lancées au cours d’une session.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 9%

---


# Nombre d’annonces

La mesure **Nombre d’annonces** indique le nombre d’annonces publicitaires lancées au cours d’une session. Utilisez-le pour comprendre et charger par contenu, canal ou type de flux. Pour les nombres de démarrages d’annonce publicitaire pivotés par dimensions d’annonce (annonceur, campagne, contenu créatif), utilisez la mesure Démarrages d’annonce publicitaire disponible lorsque la catégorie Variable d’annonce publicitaire est activée.

## Méthode de calcul de cette mesure

Le serveur principal du média est incrémenté `mediaReporting.sessionDetails.adCount` chaque événement [début de publicité](/help/implementation/events/ads/ad-start.md) reçu au cours de la session. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.adCount` à un événement personnalisé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.adCount`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (événement personnalisé auquel votre règle de traitement `a.media.adCount` mappe ; voir recherche [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | S.O. |
