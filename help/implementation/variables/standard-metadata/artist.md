---
title: Artiste
description: Définissez le nom de l’artiste pour le contenu audio.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 16%

---


# Artiste

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Artist**. Voir [Artiste](/help/reporting/dimensions/artist.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable artist est le nom de l’artiste interprète pour le contenu audio (par exemple, `"Crested Larks"`). Utilisez-le sur des sessions de musique ou de podcast pour rompre l&#39;engagement de l&#39;interprète.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.artist` |
| **champ de collection XDM** | [`mediaCollection.sessionDetails.artist`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.artist` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## SDK web

`artist` à l’intérieur des `mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        artist: "Crested Larks"
      },
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez le nom de l’artiste en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.AudioMetadataKeys.ARTIST`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.ARTIST] = "Crested Larks"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.ARTIST] = "Crested Larks"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilisez `createMediaSession` pour définir des `artist` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "artist": "Crested Larks"
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `artist` à l’intérieur du `mediaCollection.sessionDetails` :

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
          "artist": "Crested Larks"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Transmettez l’artiste dans l’objet `contextData` à l’aide de `ADB.Media.AudioMetadataKeys.Artist` :

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Artist] = "Crested Larks";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Incluez `media.artist` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.artist": "Crested Larks"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.
