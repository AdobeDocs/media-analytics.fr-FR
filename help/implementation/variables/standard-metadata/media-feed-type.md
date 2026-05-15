---
title: Type de flux multimédia
description: Identifiez le type de flux de diffusion (par exemple, East-HD ou West-SD) pour le contenu qui varie selon la région ou la qualité.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 13%

---


# Type de flux multimédia

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Type de flux multimédia**. Voir [Type de flux multimédia](/help/reporting/dimensions/media-feed-type.md) pour la dimension de rapport correspondante.*

>[!ENDSHADEBOX]

La variable de type de flux multimédia identifie le flux de diffusion (par exemple, `"East-HD"`, `"West-SD"` ou `"4K"`). Utilisez-le lorsque le même contenu est diffusé par le biais de plusieurs flux régionaux ou de qualité et que l’engagement doit être divisé par flux.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.feed` |
| **champ de collection XDM** | [`mediaCollection.sessionDetails.feed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.feed` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## SDK web

`feed` à l’intérieur des `mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        feed: "East-HD"
      },
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez le type de flux en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.MEDIA_FEED`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.MEDIA_FEED] = "East-HD"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.MEDIA_FEED] = "East-HD"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilisez `createMediaSession` pour définir des `feed` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "feed": "East-HD"
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `feed` à l’intérieur du `mediaCollection.sessionDetails` :

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
          "feed": "East-HD"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Transmettez le flux dans l’objet `contextData` à l’aide de `ADB.Media.VideoMetadataKeys.Feed` :

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Feed] = "East-HD";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Incluez `media.feed` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.feed": "East-HD"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.
