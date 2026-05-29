---
title: Saison
description: Indique le numéro de saison pour le contenu épisodique.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 10%

---


# Saison

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Saison**. Voir [Saison](/help/implementation/variables/standard-metadata/season.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Saison** indique le numéro de saison pour le contenu épisodique. Utilisez-le avec [Spectacle](show.md) et [Épisode](episode.md) pour des échappements épisodiques complets.

## Mode de remplissage de cette dimension

La saison est définie par le lecteur au début de la session lorsque le contenu fait partie d’une série.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.season` de données contextuelles lorsque [[!UICONTROL &#x200B; Métadonnées vidéo &#x200B;]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.season`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videoseason`, `post_videoseason` |
| Audience Manager | `c_contextdata.a.media.season` |

## Éléments de dimension

Chaque élément correspond à la valeur de saison littérale signalée au début de la session (généralement un entier de chaîne tel que `"1"`, `"2"`). Cohérence entre les épisodes d’une même émission ; la dimension ne normalise pas les `"1"` et les `"01"` au même élément de ligne.
