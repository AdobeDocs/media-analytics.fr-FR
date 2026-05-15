---
title: Réseau
description: Définissez le nom du réseau de diffusion ou du canal.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 16%

---


# Réseau

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Network**. Voir [Réseau](/help/reporting/dimensions/network.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable réseau est le nom du réseau ou du canal de diffusion (par exemple, `"Fox"`, `"ESPN"` ou `"HBO"`). Utilisez-la pour comparer l’engagement sur plusieurs réseaux au sein de la même propriété de diffusion en continu.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.network` |
| **champ de collection XDM** | [`mediaCollection.sessionDetails.network`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.network` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## SDK web

`network` à l’intérieur des `mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        network: "ESPN"
      },
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez le nom du réseau en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.NETWORK`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.NETWORK] = "ESPN"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.NETWORK] = "ESPN"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilisez `createMediaSession` pour définir des `network` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "network": "ESPN"
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `network` à l’intérieur du `mediaCollection.sessionDetails` :

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
          "network": "ESPN"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Transmettez le réseau dans l’objet `contextData` à l’aide de `ADB.Media.VideoMetadataKeys.Network` :

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Network] = "ESPN";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Incluez `media.network` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.network": "ESPN"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.
