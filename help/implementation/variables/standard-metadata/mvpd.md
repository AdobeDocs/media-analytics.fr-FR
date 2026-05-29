---
title: MVPD
description: Définissez le distributeur de programmation vidéo multicanal lorsque l’utilisateur s’authentifie via Adobe Pass.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 9%

---


# MVPD

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **MVPD**. Voir [&#128279;](/help/reporting/dimensions/mvpd.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable MVPD (Multichannel Video Programming Distributor) est le fournisseur de services par câble, satellite ou MVPD virtuel par lequel l’utilisateur s’est authentifié (par exemple, `"Comcast"`, `"DirecTV"` ou `"YouTubeTV"`). Définissez-le lorsque le contenu est bloqué derrière l’authentification Adobe Pass ou TV-Everywhere. Associez à [Autorisé](/help/implementation/variables/standard-metadata/authorized.md) pour suivre les sessions qui ont terminé l’authentification.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.pass.mvpd` |
| **champ de collection XDM** | [`xdm.mediaCollection.sessionDetails.mvpd`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.pass.mvpd` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`mvpd` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        mvpd: "Comcast"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Transmettez le MVPD en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.MVPD`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.MVPD] = "Comcast"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Transmettez le MVPD en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.MVPD`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.MVPD] = "Comcast"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

Utilisez `createMediaSession` pour définir des `mvpd` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "mvpd": "Comcast"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `mvpd` à l’intérieur du `xdm.mediaCollection.sessionDetails` :

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
          "mvpd": "Comcast"
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

Transmettez le MVPD dans l’objet `contextData` à l’aide de `ADB.Media.VideoMetadataKeys.MVPD` :

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.MVPD] = "Comcast";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB  Chromecast ]

Utilisez `ADBMobile.media.VideoMetadataKeys.MVPD` pour définir le MVPD dans la propriété `StandardMediaMetadata` de l’objet média avant d’appeler `trackSessionStart` :

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.MVPD] = "Comcast";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB  API Media Collection ]

Incluez `media.pass.mvpd` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.pass.mvpd": "Comcast"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
