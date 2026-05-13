---
title: Débit moyen (mesure)
description: Indique le débit moyen pondéré brut de chaque session, en kbit/s.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 7%

---


# Débit moyen (mesure)

>[!BEGINSHADEBOX]

*Cette page couvre la mesure d’événement **Débit binaire moyen**, qui indique le débit binaire moyen pondéré brut par session. Voir [Débit moyen (dimension)](/help/reporting/dimensions/average-bitrate.md) pour la dimension regroupée. Voir [Débit binaire](/help/implementation/variables/quality/bitrate.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La mesure **Débit moyen** indique le débit de lecture moyen pondéré brut, en kbit/s, pour chaque session. Contrairement à la [dimension regroupée](/help/reporting/dimensions/average-bitrate.md), la mesure est une valeur numérique continue appropriée pour les sommes, les moyennes et les cumuls de centiles entre les sessions.

## Méthode de calcul de cette mesure

Le serveur principal du média calcule une moyenne pondérée de toutes les valeurs de débit signalées au cours de la session, pondérée par la durée d’activité de chaque débit. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.bitrateAverage` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateAverage`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
