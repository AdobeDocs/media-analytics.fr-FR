---
title: Type d’affichage
description: Indique le format du contenu (épisode complet, aperçu, clip ou autre).
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 10%

---


# Type d’affichage

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Afficher le type**. Voir [Type d’affichage](/help/implementation/variables/standard-metadata/show-type.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Type d’affichage** indique le format du contenu à l’aide d’un code entier de chaîne. Utilisez-le pour séparer l’affichage du programme complet du contenu court, tel que des bandes-annonces et des clips, lors de la mesure de l’engagement.

## Mode de remplissage de cette dimension

Le type d’affichage est défini par le lecteur au début de la session.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.type` de données contextuelles lorsque [[!UICONTROL &#x200B; Métadonnées vidéo &#x200B;]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.showType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videoshowtype`, `post_videoshowtype` |
| Audience Manager | `c_contextdata.a.media.type` |

## Éléments de dimension

| Valeur | Description |
| --- | --- |
| `0` | Épisode complet |
| `1` | Aperçu ou bande-annonce |
| `2` | Clip |
| `3` | Autre |

Les valeurs sont signalées sous forme de chaînes. Les valeurs personnalisées sont acceptées, mais ne sont pas cumulées dans les quatre compartiments intégrés.
