---
title: Date de première diffusion
description: Réglez la date à laquelle le contenu a été diffusé pour la première fois à la télévision. Adobe recommande le format AAAA-MM-JJ.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 8%

---


# Date de première diffusion

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **First Air date**. Voir [Date de première diffusion](/help/reporting/dimensions/first-air-date.md) pour la dimension de création de rapports correspondante.*

>[!ENDSHADEBOX]

La première variable de date de diffusion correspond à la date de première diffusion du contenu à la télévision. Tout format de date est accepté, mais Adobe recommande de `YYYY-MM-DD` par souci de cohérence. Utilisez-le pour comparer l’engagement sur les nouvelles versions au contenu du catalogue.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.airDate` |
| **champ de collection XDM** | [`xdm.mediaCollection.sessionDetails.firstAirDate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.airDate` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`firstAirDate` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        firstAirDate: "2016-01-25"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Transmettez la première date de publication en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE] = "2016-01-25"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Transmettez la première date de publication en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE] = "2016-01-25"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

Utilisez `createMediaSession` pour définir des `firstAirDate` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "firstAirDate": "2016-01-25"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `firstAirDate` à l’intérieur du `xdm.mediaCollection.sessionDetails` :

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
          "firstAirDate": "2016-01-25"
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

Transmettez la première date de publication dans l’objet `contextData` à l’aide de `ADB.Media.VideoMetadataKeys.FirstAirDate` :

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.FirstAirDate] = "2016-01-25";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB  Chromecast ]

Utilisez `ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE` pour définir la première date de diffusion dans la propriété `StandardMediaMetadata` de l’objet média avant d’appeler `trackSessionStart` :

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE] = "2016-01-25";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB  API Media Collection ]

Incluez `media.firstAirDate` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.firstAirDate": "2016-01-25"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
