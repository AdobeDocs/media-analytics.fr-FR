---
title: Canal de contenu
description: Définissez le canal pour identifier la station de distribution, le réseau ou la propriété où le contenu est lu.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 6%

---


# Canal de contenu

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Canal de contenu**. Voir [Canal de contenu](/help/reporting/dimensions/content-channel.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable de canal de contenu identifie la station de distribution, le réseau ou la propriété où le contenu est lu. Elle est requise pour toutes les implémentations de streaming multimédia. Toute chaîne est acceptée. Les valeurs standard incluent un nom de réseau, une partie d’un chemin d’accès au site ou un identifiant de propriété interne.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.channel` |
| **champ de collection XDM** | [`xdm.mediaCollection.sessionDetails.channel`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.channel` |
| **Obligatoire** | Oui |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`channel` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

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

>[!TAB iOS]

Définissez le canal via la configuration du dispositif de suivi lors de la création du dispositif de suivi, à l’aide de `MediaConstants.TrackerConfig.CHANNEL`. Le canal ne fait pas partie de l’objet média.

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

>[!TAB Android]

Définissez le canal via la configuration du dispositif de suivi lors de la création du dispositif de suivi, à l’aide de `MediaConstants.TrackerConfig.CHANNEL`. Le canal ne fait pas partie de l’objet média.

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

val tracker = Media.createTracker(config)
```

>[!TAB Roku Edge]

`channel` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de `createMediaSession` :

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

>[!TAB  API Media Edge ]

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `channel` à l’intérieur du `xdm.mediaCollection.sessionDetails` :

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

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Définissez le canal sur `ADB.MediaConfig` avant de créer le dispositif de suivi :

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";

var tracker = ADB.Media.getInstance(mediaConfig);
```

>[!TAB  Chromecast ]

Transmettez `channel` comme clé de métadonnées standard lors de l’appel de `trackSessionStart` :

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var metadata = { "a.media.channel": "Sports" };
ADBMobile.media.trackSessionStart(mediaInfo, metadata);
```

>[!TAB Roku 2.x]

Définissez `channel` dans la section `mediaHeartbeat` du `ADBMobileConfig.json`. Le canal est une valeur de configuration et non une valeur par session :

```json
"mediaHeartbeat": {
  "channel": "Sports"
}
```

>[!TAB  API Media Collection ]

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

>[!ENDTABS]
