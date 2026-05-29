---
title: Genre
description: Genre du contenu des rapports. Le contenu multigenre est fractionné sur plusieurs éléments de ligne, chacun recevant un poids de mesure égal.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

---


# Genre

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **genre**. Voir [Genre](/help/implementation/variables/standard-metadata/genre.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Genre** indique le genre du contenu. Le genre est collecté sous la forme d’une chaîne délimitée par des virgules et stocké sous la forme d’une dimension de liste. Le contenu multigenre est fractionné sur des éléments de ligne distincts, chacun recevant un poids de mesure égal. Utilisez-le pour comparer l’engagement entre les genres sans double-compter le temps passé sur une seule ressource multi-genre.

## Mode de remplissage de cette dimension

Le genre est défini par le lecteur au début de la session.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.genre` de données contextuelles (stockées sous forme de variable de liste) lorsque [[!UICONTROL Métadonnées vidéo]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.genreList`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) ou [`xdm.mediaReporting.sessionDetails.genre`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) (hérité) |
| Flux de données | `videogenre`, `post_videogenre` |
| Audience Manager | `c_contextdata.a.media.genre` |

## Éléments de dimension

Chaque élément est une valeur de genre. Les sessions multi-genres (par exemple, `"Drama,Action"`) apparaissent sous la forme de deux éléments de ligne distincts (`Drama` et `Action`), chaque élément recevant un crédit complet pour la session.
