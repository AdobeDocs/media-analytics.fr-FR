---
title: Genre
description: Définissez le genre du contenu sous la forme d’une chaîne délimitée par des virgules. Le contenu multigenre est fractionné sur plusieurs éléments de ligne dans les rapports.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 12%

---


# Genre

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Genre**. Voir [Genre](/help/reporting/dimensions/genre.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable genre correspond au genre de contenu tel que défini par le producteur (par exemple, `"Drama"`, `"Comedy"` ou `"Drama,Action"`). Délimitez plusieurs valeurs par des virgules lorsque le contenu correspond à plusieurs genres. Dans les rapports, la variable de liste divise chaque valeur en un élément de ligne distinct, chaque élément de ligne recevant un poids métrique égal.

>[!NOTE]
>
>Dans le pipeline de création de rapports, la valeur de genre est exposée sous la forme `mediaReporting.sessionDetails.genreList` (un champ de liste). L’ancien chemin de `mediaReporting.sessionDetails.genre` reste fonctionnel, mais `genreList` est recommandé.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.genre` |
| **champ de collection XDM** | [`mediaCollection.sessionDetails.genre`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.genre` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## SDK web

`genre` à l’intérieur des `mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        genre: "Drama,Action"
      },
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez la chaîne de genre en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.GENRE`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilisez `createMediaSession` pour définir des `genre` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "genre": "Drama,Action"
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `genre` à l’intérieur du `mediaCollection.sessionDetails` :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 128,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "genre": "Drama,Action"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Transmettez le genre dans l’objet `contextData` à l’aide de `ADB.Media.VideoMetadataKeys.Genre` :

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Genre] = "Drama,Action";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Incluez `media.genre` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.genre": "Drama,Action"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.
