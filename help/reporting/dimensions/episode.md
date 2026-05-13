---
title: Épisode
description: Indique le numéro de l’épisode au cours d’une saison.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 9%

---


# Épisode

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Épisode**. Voir [Épisode](/help/implementation/variables/standard-metadata/episode.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Épisode** indique le numéro de l’épisode au cours d’une saison. Utilisez-le avec [Show](show.md) et [Season](season.md) pour ventiler l’engagement au niveau de chaque épisode.

## Mode de remplissage de cette dimension

L’épisode est défini par le lecteur au début de la session.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.episode` de données contextuelles lorsque [[!UICONTROL &#x200B; Métadonnées vidéo &#x200B;]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.episode`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videoepisode, post_videoepisode` |

## Éléments de dimension

Chaque élément correspond à la valeur d’épisode littérale signalée au début de la session (généralement un entier de chaîne tel que `"13"`). Les numéros d’épisodes ne sont pas uniques au fil des saisons ; couplés à la saison pour des échappées sans ambiguïté.
