---
title: Auteur
description: Définissez l’auteur du contenu. Principalement utilisé pour les livres audio.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 9%

---


# Auteur

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Auteur**. Voir [Auteur](/help/reporting/dimensions/author.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable auteur est l’auteur du contenu (par exemple, `"Eleanor Clementine"`). Principalement utilisé pour les livres audio, mais également acceptable pour les podcasts dont l’hôte ou le producteur est l’attribution pertinente.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.author` |
| **champ de collection XDM** | [`xdm.mediaCollection.sessionDetails.author`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.author` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`author` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        author: "Eleanor Clementine"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Transmettez l’auteur en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.AudioMetadataKeys.AUTHOR`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.AUTHOR] = "Eleanor Clementine"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Transmettez l’auteur en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.AudioMetadataKeys.AUTHOR`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.AUTHOR] = "Eleanor Clementine"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

Utilisez `createMediaSession` pour définir des `author` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "author": "Eleanor Clementine"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `author` à l’intérieur du `xdm.mediaCollection.sessionDetails` :

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
          "author": "Eleanor Clementine"
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

Transmettez l’auteur dans l’objet `contextData` à l’aide de `ADB.Media.AudioMetadataKeys.Author` :

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Author] = "Eleanor Clementine";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB  Chromecast ]

Utilisez `ADBMobile.media.AudioMetadataKeys.AUTHOR` pour définir l’auteur dans la propriété `StandardMediaMetadata` de l’objet média avant d’appeler `trackSessionStart` :

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Track", "audio-123", 240,
  ADBMobile.media.StreamType.AOD, ADBMobile.media.MediaType.Audio);
var standardMetadata = {};
standardMetadata[ADBMobile.media.AudioMetadataKeys.AUTHOR] = "Eleanor Clementine";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Utilisez `MEDIA_AudioMetadataKeyAUTHOR` pour définir l’auteur dans les métadonnées standard de l’objet média avant d’appeler `mediaTrackSessionStart` :

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Track", "audio-123", 240.0, adb.MEDIA_STREAM_TYPE_AOD, adb.MEDIA_TYPE_AUDIO)

standardMetadata = {}
standardMetadata[adb.MEDIA_AudioMetadataKeyAUTHOR] = "Eleanor Clementine"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB  API Media Collection ]

Incluez `media.author` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.author": "Eleanor Clementine"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
