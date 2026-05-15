---
title: Durée totale de la mémoire tampon (mesure)
description: Indique le temps de tampon cumulé pour les sommes et les moyennes entre les sessions.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 7%

---


# Durée totale de la mémoire tampon (mesure)

>[!BEGINSHADEBOX]

*Cette page couvre la mesure **Durée totale de la mémoire tampon**. Adobe Analytics renseigne automatiquement une paire [Durée totale de la mémoire tampon (dimension)](/help/reporting/dimensions/total-buffer-duration.md) à partir de la même variable de données contextuelles `a.media.qoe.bufferTime`. Customer Journey Analytics expose un seul champ de `mediaReporting.qoeDataDetails.bufferTime` que vous pouvez utiliser comme dimension ou mesure.*

>[!ENDSHADEBOX]

La mesure **Durée totale de la mémoire tampon** indique le temps de mémoire tampon cumulé entre les sessions, qui convient aux sommes, moyennes et cumuls de centiles. Utilisez la mesure pour calculer le temps total passé par les clients à attendre sur des tampons au cours d’une période de rapport.

## Méthode de calcul de cette mesure

Le serveur principal du média additionne la durée de chaque intervalle de mémoire tampon (du [&#x200B; début de la mémoire tampon &#x200B;](/help/implementation/events/playback/buffer-start.md) au changement d&#39;état suivant). La mesure est signalée lors de l’appel de fermeture. Analysis Workspace affiche la valeur en tant que `HH:MM:SS` ; les flux de données, Data Warehouse et les API de création de rapports affichent la valeur en secondes.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.bufferTime` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.bufferTime` |
