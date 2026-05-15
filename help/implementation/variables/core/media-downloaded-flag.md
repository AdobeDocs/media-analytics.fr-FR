---
title: Indicateur de média téléchargé
description: Marquer une session comme étant une lecture hors ligne téléchargée afin qu’elle soit signalée séparément des sessions en flux continu.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 10%

---


# Indicateur de média téléchargé

>[!BEGINSHADEBOX]

*Cette page couvre la collecte de données pour la variable **indicateur téléchargé par Media**. Voir [Média téléchargé](/help/reporting/dimensions/media-downloaded-flag.md) pour la dimension de rapport correspondante.*

>[!ENDSHADEBOX]

L’indicateur média téléchargé indique qu’une session est une lecture de contenu hors ligne précédemment téléchargé plutôt qu’un flux en direct depuis Internet. Définissez-le lors de l’initialisation du dispositif de suivi (Mobile SDK) ou incluez-le dans la payload `sessionStart` (API Edge / Media Collection). Utilisez cet indicateur pour séparer la lecture hors ligne des sessions en flux continu dans les rapports.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.downloaded` |
| **champ de collection XDM** | [`mediaCollection.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.downloaded` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## SDK web

Définissez `isDownloaded` à `true` dans `mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

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
        streamType: "video",
        isDownloaded: true
      },
      playhead: 0
    }
  }
});
```

## SDK mobile

Définissez l’indicateur de contenu téléchargé sur la configuration du dispositif de suivi lors de la création du dispositif de suivi, à l’aide de `MediaConstants.TrackerConfig.DOWNLOADED_CONTENT`.

**iOS (Swift)**

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"
config[MediaConstants.TrackerConfig.DOWNLOADED_CONTENT] = true

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

**Android (Kotlin)**

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"
config[MediaConstants.TrackerConfig.DOWNLOADED_CONTENT] = true

val tracker = Media.createTracker(config)
```

## Roku (BrightScript)

Définissez `isDownloaded` à `true` dans `mediaCollection.sessionDetails` lors de l’appel de `createMediaSession` :

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
                "streamType": "video",
                "isDownloaded": true
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [téléchargé](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/downloaded/#downloaded) après le retour en ligne de l’appareil, ce qui met en lot la session hors ligne complète dans `mediaDownloadedEvents`. Adobe définit automatiquement le `isDownloaded` sur `true` et attribue un ID de session ; n’incluez aucun des deux dans la payload.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.downloaded",
      "mediaDownloadedEvents": [
        {
          "mediaEventTimestamp": "YYYY-09-26T15:52:24+00:00",
          "mediaEventType": "media.sessionStart",
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
        },
        {
          "mediaEventTimestamp": "YYYY-09-26T15:54:32+00:00",
          "mediaEventType": "media.sessionComplete",
          "mediaCollection": {
            "playhead": 128
          }
        }
      ]
    }
  }]
}
```

## SDK Media

Définissez `downloadedContent` sur `ADB.MediaConfig` avant de créer le dispositif de suivi :

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";
mediaConfig.downloadedContent = true;

var tracker = ADB.Media.getInstance(mediaConfig);
```

## API Media Collection

Incluez `media.downloaded` dans l’objet `params` de votre `sessionStart` requête POST :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.downloaded": true
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.
