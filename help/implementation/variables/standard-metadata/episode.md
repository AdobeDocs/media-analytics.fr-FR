---
title: Épisode
description: Définissez le numéro d’épisode pour le contenu épisodique afin que les épisodes individuels puissent être signalés séparément.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 10%

---


# Épisode

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Episode**. Voir [Épisode](/help/reporting/dimensions/episode.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable d’épisode correspond au nombre d’épisodes au cours de la saison (généralement un entier de chaîne comme `"13"`). Associez-la à [Spectacle](/help/implementation/variables/standard-metadata/show.md) et [Saison](/help/implementation/variables/standard-metadata/season.md) afin que l’engagement puisse être divisé par épisode individuel.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.episode` |
| **champ de collection XDM** | [`xdm.mediaCollection.sessionDetails.episode`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.episode` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`episode` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        episode: "13"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Transmettez le numéro d’épisode en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.EPISODE`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.EPISODE] = "13"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Transmettez le numéro d’épisode en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.EPISODE`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.EPISODE] = "13"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

Utilisez `createMediaSession` pour définir des `episode` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "episode": "13"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `episode` à l’intérieur du `xdm.mediaCollection.sessionDetails` :

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
          "episode": "13"
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

Transmettez l’épisode dans l’objet `contextData` à l’aide de `ADB.Media.VideoMetadataKeys.Episode` :

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Episode] = "13";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB  Chromecast ]

Utilisez `ADBMobile.media.VideoMetadataKeys.EPISODE` pour définir le numéro d’épisode dans la propriété `StandardMediaMetadata` de l’objet média avant d’appeler `trackSessionStart` :

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.EPISODE] = "13";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB  API Media Collection ]

Incluez `media.episode` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.episode": "13"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
