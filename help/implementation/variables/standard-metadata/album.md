---
title: Album
description: Définissez le nom de l’album pour le contenu audio.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 10%

---


# Album

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Album**. Voir [Album](/help/reporting/dimensions/album.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable album est le nom de l’album auquel appartient la piste audio (par exemple, `"Pinegrove"`). Utilisez-le pour remonter l&#39;engagement entre les pistes du même album.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.album` |
| **champ de collection XDM** | [`xdm.mediaCollection.sessionDetails.album`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.album` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`album` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        album: "Pinegrove"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Transmettez l’album en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.AudioMetadataKeys.ALBUM`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.ALBUM] = "Pinegrove"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Transmettez l’album en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.AudioMetadataKeys.ALBUM`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.ALBUM] = "Pinegrove"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

Utilisez `createMediaSession` pour définir des `album` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "album": "Pinegrove"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `album` à l’intérieur du `xdm.mediaCollection.sessionDetails` :

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
          "album": "Pinegrove"
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

Transmettez l’album dans l’objet `contextData` à l’aide de `ADB.Media.AudioMetadataKeys.Album` :

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Album] = "Pinegrove";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB  Chromecast ]

Utilisez `ADBMobile.media.AudioMetadataKeys.ALBUM` pour définir l’album dans la propriété `StandardMediaMetadata` de l’objet média avant d’appeler `trackSessionStart` :

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Track", "audio-123", 240,
  ADBMobile.media.StreamType.AOD, ADBMobile.media.MediaType.Audio);
var standardMetadata = {};
standardMetadata[ADBMobile.media.AudioMetadataKeys.ALBUM] = "Pinegrove";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB  API Media Collection ]

Incluez `media.album` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.album": "Pinegrove"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
