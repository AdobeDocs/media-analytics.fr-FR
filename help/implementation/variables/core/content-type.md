---
title: Type de contenu
description: Définissez le type de contenu pour identifier le format du flux (VOD, Live, Linéaire, podcast, chanson, etc.).
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 5%

---


# Type de contenu

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Type de contenu**. Voir [Type de contenu](/help/reporting/dimensions/content-type.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable de type de contenu identifie le format du flux (par exemple, VOD, Live ou Linéaire pour la vidéo, ou podcast ou livre audio pour l’audio). Elle est requise pour toutes les implémentations de streaming multimédia et doit être définie au début de la session. Les valeurs définies par Adobe renseignent les segments et les rapports de type de contenu intégrés. Les chaînes personnalisées sont également acceptées, mais ne correspondent pas aux segments intégrés. Si elle n’est pas définie, la valeur par défaut est `missing_content_type`.

Valeurs recommandées :

* **Vidéo :** `vod`, `live`, `linear`, `ugc`, `dvod`
* **Audio :** `song`, `podcast`, `audiobook`, `radio`

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.contentType` |
| **champ de collection XDM** | [`xdm.mediaCollection.sessionDetails.contentType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.contentType` |
| **Obligatoire** | Oui |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`contentType` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

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

Transmettez la constante de type de contenu comme argument de `streamType` à `createMediaObject`. Utilisez des valeurs `MediaConstants.StreamType.*` telles que `VOD`, `LIVE`, `LINEAR`, `AOD`, `PODCAST`. Remarque : dans Mobile SDK, l’argument `streamType` contrôle le type de contenu. La variable Type de flux (audio ou vidéo) est l’argument `mediaType` distinct.

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

Transmettez la constante de type de contenu comme argument de `streamType` à `createMediaObject`. Utilisez des valeurs `MediaConstants.StreamType.*` telles que `VOD`, `LIVE`, `LINEAR`, `AOD`, `PODCAST`. Remarque : dans Mobile SDK, l’argument `streamType` contrôle le type de contenu. La variable Type de flux (audio ou vidéo) est l’argument `mediaType` distinct.

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku Edge]

`contentType` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de `createMediaSession` :

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

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `contentType` à l’intérieur du `xdm.mediaCollection.sessionDetails` :

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

Transmettez une constante `ADB.Media.StreamType.*` comme quatrième argument à `ADB.Media.createMediaObject` :

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADB.Media.StreamType.VOD, // Content type — VOD, LIVE, LINEAR, etc.
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB  Chromecast ]

Transmettez une constante `ADBMobile.media.StreamType.*` comme quatrième argument à `ADBMobile.media.createMediaObject` :

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

Transmettez une constante `MEDIA_STREAM_TYPE_*` comme quatrième argument (`streamType`) à `adb_media_init_mediainfo`. Dans le SDK Roku 2.x, cet argument porte le type de contenu (`vod`, `live`, `linear`) :

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB  API Media Collection ]

Incluez `media.contentType` dans l’objet `params` de votre `sessionStart` requête POST :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.contentType": "vod"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
