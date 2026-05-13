---
source-git-commit: c06ecd16f417c9584fb87181074d1c2bee487e0b
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 5%

---
﻿---
title: Mesures calculées
description: Mesures calculées personnalisées pour les rapports de médias en flux continu dans Adobe Analytics et Customer Journey Analytics.
feature: Metrics
role: User, Admin
---

# Mesures calculées

Les mesures calculées pour les services de médias en flux continu Adobe sont des mesures personnalisées créées à partir des mesures de médias en flux continu standard. Vous pouvez ainsi obtenir des ratios tels que le temps de publicité moyen ou le taux d’achèvement des médias sans modifier votre implémentation.

Pour créer ces mesures calculées dans Analysis Workspace, consultez la présentation des mesures calculées respectives dans [Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/components/calculated-metrics/cm-overview) ou [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview).

| Mesure calculée | Description | Formule |
| --- | --- | --- |
| Temps moyen publicités par flux de médias | Démarrages d’annonces publicitaires par démarrage de médias | [`Ad Starts`](/help/reporting/metrics/ad-starts.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Temps moyen chapitres par flux de médias | Démarrages de chapitre par démarrage de média | [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Temps moyen temps passé sur le média | Temps total passé par démarrages de média (`HH:MM:SS`) | [`Media Time Spent`](/help/reporting/metrics/media-time-spent.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Temps moyen durée de contenu | Temps passé sur le contenu par démarrage de contenu (`HH:MM:SS`) | [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) / [`Content Starts`](/help/reporting/metrics/content-starts.md) |
| Temps moyen temps passé sur la publicité | Temps passé sur la publicité par démarrage de publicité (`HH:MM:SS`) | [`Ad Time Spent`](/help/reporting/metrics/ad-time-spent.md) / [`Ad Starts`](/help/reporting/metrics/ad-starts.md) |
| Temps moyen temps de chapitre passé | Temps passé sur le chapitre par démarrage de chapitre (`HH:MM:SS`) | [`Chapter Time Spent`](/help/reporting/metrics/chapter-time-spent.md) / [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) |
| Taux d’achèvement du média | Taux de contenu terminé par rapport au contenu multimédia initié | [`Content Completes`](/help/reporting/metrics/content-completes.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Taux d’achèvement du contenu | Taux de contenu terminé par rapport aux démarrages de contenu | [`Content Completes`](/help/reporting/metrics/content-completes.md) / [`Content Starts`](/help/reporting/metrics/content-starts.md) |
| Taux d’achèvement des publicités | Taux de publicités terminées par rapport aux démarrages de publicités | [`Ad Completes`](/help/reporting/metrics/ad-completes.md) / [`Ad Starts`](/help/reporting/metrics/ad-starts.md) |
| Taux d’achèvement du chapitre | Taux de chapitres terminés par rapport aux démarrages de chapitre | [`Chapter Completes`](/help/reporting/metrics/chapter-completes.md) / [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) |
| Déposer avant le taux de départ | Taux de pertes avant le démarrage par rapport aux démarrages du média | [`Drops Before Start`](/help/reporting/metrics/drops-before-start.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Taux de durée de pause du contenu | Taux de la durée totale de pause par rapport au temps passé sur le contenu | [`Total Pause Duration`](/help/reporting/metrics/total-pause-duration.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| Taux de durée du tampon de contenu | Taux de la durée totale de la mémoire tampon par rapport au temps passé sur le contenu | [`Total Buffer Duration`](/help/reporting/metrics/total-buffer-duration.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| Taux de temps de démarrage du contenu | Taux du temps de démarrage par rapport au temps passé sur le contenu | [`Time to Start`](/help/reporting/metrics/time-to-start.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| Taux de temps passé sur la publicité | Taux du temps passé sur la publicité par rapport au temps passé sur le contenu | [`Ad Time Spent`](/help/reporting/metrics/ad-time-spent.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
