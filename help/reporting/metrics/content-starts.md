---
title: Le contenu démarre
description: Comptabilise les sessions au cours desquelles le contenu principal a réellement commencé à être lu.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 10%

---


# Le contenu démarre

La mesure **Content starts** comptabilise les sessions au cours desquelles le contenu principal a réellement commencé à être lu. Contrairement aux [démarrages de médias](media-starts.md), il exclut les sessions qui se sont terminées pendant les publicités preroll, la mise en mémoire tampon ou les blocages. Cela en fait le bon dénominateur pour les taux d’achèvement et d’engagement.

## Méthode de calcul de cette mesure

Le serveur principal du média définit cet indicateur la première fois qu’un événement [play](/help/implementation/events/playback/play.md) pour le contenu principal est reçu. La mesure est déclenchée sur cet événement de lecture, mais signalée sur l’appel de fermeture. Pour calculer le taux de dépôt pré-roll, utilisez `(Media starts − Content starts) / Media starts`.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.play` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isPlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.play` |
