---
title: Station
description: Définissez le nom ou l’ID de la station radio pour le contenu de diffusion audio.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 10%

---


# Station

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Station**. Voir [Station](/help/reporting/dimensions/station.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable station est le nom ou l’identifiant de la station radio qui diffuse le contenu audio (par exemple, `"NPR"` ou `"WXYZ-FM"`). Utilisez-le pour comparer l&#39;engagement entre les stations d&#39;un réseau syndiqué.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.station` |
| **champ de collection XDM** | [`xdm.mediaCollection.sessionDetails.station`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.station` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`station` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        station: "NPR"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Transmettez la station en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.AudioMetadataKeys.STATION`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.STATION] = "NPR"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Transmettez la station en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.AudioMetadataKeys.STATION`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.STATION] = "NPR"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

Utilisez `createMediaSession` pour définir des `station` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "station": "NPR"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `station` à l’intérieur du `xdm.mediaCollection.sessionDetails` :

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
          "station": "NPR"
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

Transmettez la station dans l’objet `contextData` à l’aide de `ADB.Media.AudioMetadataKeys.Station` :

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Station] = "NPR";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB  Chromecast ]

Utilisez `ADBMobile.media.AudioMetadataKeys.STATION` pour définir le nom de la station dans la propriété `StandardMediaMetadata` de l’objet média avant d’appeler `trackSessionStart` :

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Track", "audio-123", 240,
  ADBMobile.media.StreamType.AOD, ADBMobile.media.MediaType.Audio);
var standardMetadata = {};
standardMetadata[ADBMobile.media.AudioMetadataKeys.STATION] = "NPR";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB  API Media Collection ]

Incluez `media.station` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.station": "NPR"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
