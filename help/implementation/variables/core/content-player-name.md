---
title: Nom du lecteur de contenu
description: Définissez le nom du lecteur pour identifier le lecteur qui a rendu le contenu.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 6%

---


# Nom du lecteur de contenu

>[!BEGINSHADEBOX]

*Cette page couvre la collecte de données pour la variable **Content Player name**. Voir [Nom du lecteur de contenu](/help/reporting/dimensions/content-player-name.md) pour la dimension de compte rendu des performances correspondante.*

>[!ENDSHADEBOX]

La variable de nom du lecteur de contenu identifie le lecteur qui a rendu le contenu (par exemple, `HTML5 Player`, `Brightcove` ou `Roku Player`). Elle est requise pour toutes les implémentations de streaming multimédia et doit être définie au début de la session. La valeur est utilisée dans la dimension Nom du lecteur de contenu pour comparer l’engagement et la qualité entre les lecteurs dans la même propriété.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.playerName` |
| **champ de collection XDM** | [`xdm.mediaCollection.sessionDetails.playerName`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.playerName` |
| **Obligatoire** | Oui |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`playerName` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

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

Définissez le nom du lecteur via la configuration du dispositif de suivi lors de la création du dispositif de suivi, à l’aide de `MediaConstants.TrackerConfig.PLAYER_NAME`. Le nom du lecteur ne fait pas partie de l’objet média.

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

>[!TAB Android]

Définissez le nom du lecteur via la configuration du dispositif de suivi lors de la création du dispositif de suivi, à l’aide de `MediaConstants.TrackerConfig.PLAYER_NAME`. Le nom du lecteur ne fait pas partie de l’objet média.

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

val tracker = Media.createTracker(config)
```

>[!TAB Roku Edge]

`playerName` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de `createMediaSession` :

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

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `playerName` à l’intérieur du `xdm.mediaCollection.sessionDetails` :

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

Définissez le nom du lecteur sur `ADB.MediaConfig` avant de créer le dispositif de suivi :

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";

var tracker = ADB.Media.getInstance(mediaConfig);
```

>[!TAB  Chromecast ]

Transmettez le nom du lecteur en tant que clé de métadonnées standard lors de l’appel de `trackSessionStart` :

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var metadata = { "a.media.playerName": "Chromecast Player" };
ADBMobile.media.trackSessionStart(mediaInfo, metadata);
```

>[!TAB Roku 2.x]

Définissez `playerName` dans la section `mediaHeartbeat` du `ADBMobileConfig.json`. Le nom du lecteur est une valeur de configuration et non une valeur par session :

```json
"mediaHeartbeat": {
  "playerName": "Roku Player"
}
```

>[!TAB  API Media Collection ]

Incluez `media.playerName` dans l’objet `params` de votre `sessionStart` requête POST :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.playerName": "HTML5 Player"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
