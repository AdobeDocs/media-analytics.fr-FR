---
title: Type de chargement des annonces
description: Définissez le type de chargement publicitaire pour la session de diffusion en continu.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 3%

---


# Type de chargement des annonces

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Type de chargement des annonces**. Voir [Chargements d’annonces](/help/reporting/dimensions/ad-load-type.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable type de chargement de l’annonce publicitaire identifie le type d’annonce publicitaire chargé au début de la session. Cette valeur est définie par le système de diffusion de publicités interne de votre organisation et n’est pas limitée à une énumération standard. Vous pouvez utiliser n’importe quelle chaîne significative pour votre implémentation, telle que `"linear"`, `"dynamic"` ou `"programmatic"`.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.adLoad` |
| **champ de collection XDM** | [`xdm.mediaCollection.sessionDetails.adLoad`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.adLoad` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`adLoad` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de [`createMediaSession`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/createmediasession) :

```javascript
alloy("createMediaSession", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "My Video",
        length: 300,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        adLoad: "linear"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Transmettez le type de chargement de l’annonce publicitaire en tant que clé de métadonnées dans l’argument de dictionnaire à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.AD_LOAD`.

```swift
var videoMetadata: [String: String] = [:]
videoMetadata[MediaConstants.VideoMetadataKeys.AD_LOAD] = "linear"

tracker.trackSessionStart(info: mediaObject, metadata: videoMetadata)
```

>[!TAB Android]

Transmettez le type de chargement de l’annonce publicitaire en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.AD_LOAD`.

```kotlin
val videoMetadata = HashMap<String, String>()
videoMetadata[MediaConstants.VideoMetadataKeys.AD_LOAD] = "linear"

tracker.trackSessionStart(mediaInfo, videoMetadata)
```

>[!TAB Roku]

Utilisez `createMediaSession` pour définir des `adLoad` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "adLoad": "linear"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `adLoad` à l’intérieur du `xdm.mediaCollection.sessionDetails` :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 300,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "adLoad": "linear"
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

Transmettez le type de chargement d’annonce dans l’objet `contextData` à l’aide de `ADB.Media.VideoMetadataKeys.AdLoad` :

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.AdLoad] = "linear";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB  Chromecast ]

Utilisez `ADBMobile.media.VideoMetadataKeys.AD_LOAD` pour définir le type de chargement de l’annonce publicitaire dans la propriété `StandardMediaMetadata` de l’objet média avant d’appeler `trackSessionStart` :

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 300,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.AD_LOAD] = "linear";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB  API Media Collection ]

Incluez `media.adLoad` dans l’objet `params` de votre `sessionStart` requête POST :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.adLoad": "linear"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
