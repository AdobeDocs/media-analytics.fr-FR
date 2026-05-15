---
title: Format du flux
description: Définissez le format du flux pour identifier le niveau de qualité (HD, SD ou autre libellé utilisé par votre pipeline de diffusion).
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---


# Format du flux

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Format de flux**. Voir [Format de flux](/help/reporting/dimensions/stream-format.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable de format du flux identifie le niveau de qualité du flux (généralement `"HD"` ou `"SD"`, mais toute chaîne est acceptée). Définissez-le lorsque vous souhaitez ventiler l’engagement, l’achèvement ou la qualité par niveau de qualité de diffusion.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.format` |
| **champ de collection XDM** | [`mediaCollection.sessionDetails.streamFormat`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.format` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## SDK Web

`streamFormat` à l’intérieur des `mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        streamFormat: "HD"
      },
      playhead: 0
    }
  }
});
```

## SDK Mobile

Transmettez le format de flux en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.STREAM_FORMAT`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.STREAM_FORMAT] = "HD"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.STREAM_FORMAT] = "HD"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilisez `createMediaSession` pour définir des `streamFormat` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "streamFormat": "HD"
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `streamFormat` à l’intérieur du `mediaCollection.sessionDetails` :

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
          "streamFormat": "HD"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Transmettez le format de flux dans l’objet `contextData` à l’aide de `ADB.Media.VideoMetadataKeys.StreamFormat` :

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.StreamFormat] = "HD";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Incluez `media.streamFormat` dans l’objet `params` de votre `sessionStart` requête POST :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.streamFormat": "HD"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.
