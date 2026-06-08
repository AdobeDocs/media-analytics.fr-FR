---
title: Durée du contenu
description: Définissez la longueur du contenu en secondes au début de la session. Il génère des marqueurs de progression et une audience moyenne par minute.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 7%

---


# Durée du contenu

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Longueur du contenu**. Voir [Longueur du contenu](/help/reporting/dimensions/content-length.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable de longueur du contenu correspond à la durée totale du contenu, en secondes. Elle est requise pour toutes les implémentations de streaming multimédia et doit être définie au début de la session. La longueur du contenu génère plusieurs mesures calculées en arrière-plan, y compris les marqueurs de progression (10/25/50/75/95 %) et l’audience moyenne par minute. Si la longueur du contenu n’est pas définie ou est inférieure à zéro, ces mesures ne sont pas générées. Pour les flux en direct d’une durée inconnue, utilisez `86400` (24 heures).

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.length` |
| **champ de collection XDM** | [`xdm.mediaCollection.sessionDetails.length`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.length` |
| **Obligatoire** | Oui |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`length` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

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

Transmettez la longueur du contenu en secondes comme argument de `length` à `createMediaObject`.

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

Transmettez la longueur du contenu en secondes comme argument de `length` à `createMediaObject`.

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku Edge]

`length` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de `createMediaSession` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "friendlyName": "My Video",
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

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `length` à l’intérieur du `xdm.mediaCollection.sessionDetails` :

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

Transmettez la longueur du contenu en secondes comme troisième argument à `ADB.Media.createMediaObject` :

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,                      // length in seconds
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB  Chromecast ]

Transmettez la longueur du contenu en secondes comme troisième argument à `ADBMobile.media.createMediaObject` :

```javascript
var mediaInfo = ADBMobile.media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADBMobile.media.StreamType.VOD,
  ADBMobile.media.MediaType.Video
);
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Transmettez la longueur du contenu en secondes comme troisième argument à `adb_media_init_mediainfo` :

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB  API Media Collection ]

Incluez `media.length` dans l’objet `params` de votre `sessionStart` requête POST :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.length": 128
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
