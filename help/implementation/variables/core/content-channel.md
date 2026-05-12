---
title: Canal de contenu
description: Définissez le canal pour identifier la station de distribution, le réseau ou la propriété où le contenu est lu.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 12%

---


# Canal de contenu

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Canal de contenu**. Voir [Canal de contenu](/help/reporting/dimensions/content-channel.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable de canal de contenu identifie la station de distribution, le réseau ou la propriété où le contenu est lu. Elle est requise pour toutes les implémentations de streaming multimédia. Toute chaîne est acceptée. Les valeurs standard incluent un nom de réseau, une partie d’un chemin d’accès au site ou un identifiant de propriété interne.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.channel` |
| **champ de collection XDM** | [`mediaCollection.sessionDetails.channel`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obligatoire** | Oui |
| **Envoyé avec** | Début et fin de la session |

## SDK web

`channel` à l’intérieur des `mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video"
      },
      playhead: 0
    }
  }
});
```

## SDK mobile

Définissez le canal via la configuration du dispositif de suivi lors de la création du dispositif de suivi, à l’aide de `MediaConstants.TrackerConfig.CHANNEL`. Le canal ne fait pas partie de l’objet média.

**iOS (Swift)**

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

**Android (Kotlin)**

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

val tracker = Media.createTracker(config)
```

## Roku (BrightScript)

`channel` à l’intérieur des `mediaCollection.sessionDetails` lors de l’appel de `createMediaSession` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `channel` à l’intérieur du `mediaCollection.sessionDetails` :

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
          "channel": "Sports"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Définissez le canal sur `ADB.MediaConfig` avant de créer le dispositif de suivi :

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";

var tracker = ADB.Media.getInstance(mediaConfig);
```

## API Media Collection

Incluez `media.channel` dans l’objet `params` de votre `sessionStart` requête POST :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.
