---
title: Mesures calculées
description: Mesures calculées personnalisées pour les rapports de médias en flux continu dans Adobe Analytics et Customer Journey Analytics.
feature: Metrics
role: User, Admin
source-git-commit: cb3770abd06eb8debe4ff92641835f04f62471f7
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 4%

---

# Mesures calculées du streaming multimédia

Les mesures calculées pour les services de médias en flux continu Adobe sont des mesures personnalisées créées à partir des mesures de médias en flux continu standard. Vous pouvez ainsi obtenir des ratios tels que le temps de publicité moyen ou le taux d’achèvement des médias sans modifier votre implémentation.

Pour créer ces mesures calculées dans Analysis Workspace, consultez la présentation des mesures calculées respectives dans [Adobe Analytics](https://experienceleague.adobe.com/fr/docs/analytics/components/calculated-metrics/cm-overview) ou [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview).

| Mesure calculée | Description | Formule |
| --- | --- | --- |
| Temps moyen publicités par flux de médias | [[!UICONTROL Publicités démarrées]](/help/reporting/metrics/ad-starts.md) par [[!UICONTROL Médias démarrés]](/help/reporting/metrics/media-starts.md) | `[Ad starts] / [Media starts]` |
| Temps moyen chapitres par flux de médias | [[!UICONTROL Démarrages du chapitre]](/help/reporting/metrics/chapter-starts.md) par [[!UICONTROL démarrages des médias]](/help/reporting/metrics/media-starts.md) | `[Chapter starts] / [Media starts]` |
| Temps moyen temps passé sur le média | [[!UICONTROL Durée des médias]](/help/reporting/metrics/media-time-spent.md) par [[!UICONTROL démarrages des médias]](/help/reporting/metrics/media-starts.md) (`HH:MM:SS`) | `[Media time spent] / [Media starts]` |
| Temps moyen durée de contenu | [[!UICONTROL Temps passé sur le contenu]](/help/reporting/metrics/content-time-spent.md) par [[!UICONTROL Début du contenu]](/help/reporting/metrics/content-starts.md) (`HH:MM:SS`) | `[Content time spent] / [Content starts]` |
| Temps moyen temps passé sur la publicité | [[!UICONTROL Temps passé sur la publicité]](/help/reporting/metrics/ad-time-spent.md) par [[!UICONTROL démarrages de publicité]](/help/reporting/metrics/ad-starts.md) (`HH:MM:SS`) | `[Ad time spent] / [Ad starts]` |
| Temps moyen temps de chapitre passé | [[!UICONTROL Temps passé sur le chapitre]](/help/reporting/metrics/chapter-time-spent.md) par [[!UICONTROL début du chapitre]](/help/reporting/metrics/chapter-starts.md) (`HH:MM:SS`) | `[Chapter time spent] / [Chapter starts]` |
| Taux d’achèvement du média | Taux de [[!UICONTROL contenu terminé]](/help/reporting/metrics/content-completes.md) par rapport à [[!UICONTROL médias démarrés]](/help/reporting/metrics/media-starts.md) | `[Content completes] / [Media starts]` |
| Taux d’achèvement du contenu | Taux de [[!UICONTROL contenu terminé]](/help/reporting/metrics/content-completes.md) par rapport à [[!UICONTROL contenu démarré]](/help/reporting/metrics/content-starts.md) | `[Content completes] / [Content starts]` |
| Taux d’achèvement des publicités | Taux de [[!UICONTROL publicités terminées]](/help/reporting/metrics/ad-completes.md) par rapport à [[!UICONTROL publicités démarrées]](/help/reporting/metrics/ad-starts.md) | `[Ad completes] / [Ad starts]` |
| Taux d’achèvement du chapitre | Taux de [[!UICONTROL chapitres terminés]](/help/reporting/metrics/chapter-completes.md) par rapport à [[!UICONTROL chapitres démarrés]](/help/reporting/metrics/chapter-starts.md) | `[Chapter completes] / [Chapter starts]` |
| Déposer avant le taux de départ | Taux de [[!UICONTROL pertes avant le démarrage]](/help/reporting/metrics/drops-before-start.md) par rapport à [[!UICONTROL démarrages des médias]](/help/reporting/metrics/media-starts.md) | `[Drops before start] / [Media starts]` |
| Taux de durée de pause du contenu | Taux de [[!UICONTROL Durée totale de la pause]](/help/reporting/metrics/total-pause-duration.md) par rapport à [[!UICONTROL Temps passé sur le contenu]](/help/reporting/metrics/content-time-spent.md) | `[Total pause duration] / [Content time spent]` |
| Taux de durée du tampon de contenu | Taux de [[!UICONTROL Durée totale de la mémoire tampon]](/help/reporting/metrics/total-buffer-duration.md) par rapport à [[!UICONTROL Temps passé sur le contenu]](/help/reporting/metrics/content-time-spent.md) | `[Total buffer duration] / [Content time spent]` |
| Taux de temps de démarrage du contenu | Taux de [[!UICONTROL Temps de démarrage]](/help/reporting/metrics/time-to-start.md) par rapport à [[!UICONTROL Temps passé sur le contenu]](/help/reporting/metrics/content-time-spent.md) | `[Time to start] / [Content time spent]` |
| Taux de temps passé sur la publicité | Taux de [[!UICONTROL temps passé sur la publicité]](/help/reporting/metrics/ad-time-spent.md) par rapport à [[!UICONTROL temps passé sur le contenu]](/help/reporting/metrics/content-time-spent.md) | `[Ad time spent] / [Content time spent]` |

