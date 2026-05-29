---
title: Autorisé
description: Marquez une session comme authentifiée via Adobe Pass afin qu’elle soit comptabilisée dans l’événement Autorisé.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 9%

---


# Autorisé

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Autorisée**. Voir [Autorisé](/help/reporting/metrics/authorized.md) pour la mesure de reporting correspondante.*

>[!ENDSHADEBOX]

La variable autorisée marque une session dont l’utilisateur a été autorisé via Adobe Pass/TV-Everywhere. Définissez-la sur `"TRUE"` lorsqu’une autorisation est confirmée, sans quoi elle sera désactivée. Associez à [&#128279;](/help/implementation/variables/standard-metadata/mvpd.md) pour ventiler l&#39;authentification par fournisseur.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.pass.auth` |
| **champ de collection XDM** | [`xdm.mediaCollection.sessionDetails.authorized`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.pass.auth` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`authorized` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        authorized: "TRUE"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Transmettez l’indicateur autorisé en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.AUTHORIZED`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.AUTHORIZED] = "TRUE"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Transmettez l’indicateur autorisé en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.AUTHORIZED`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.AUTHORIZED] = "TRUE"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

Utilisez `createMediaSession` pour définir des `authorized` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "authorized": "TRUE"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `authorized` à l’intérieur du `xdm.mediaCollection.sessionDetails` :

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
          "authorized": "TRUE"
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

Transmettez l’indicateur autorisé dans l’objet `contextData` à l’aide de `ADB.Media.VideoMetadataKeys.Authorized` :

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Authorized] = "TRUE";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB  Chromecast ]

Utilisez `ADBMobile.media.VideoMetadataKeys.AUTHORIZED` pour définir l’indicateur autorisé dans la propriété `StandardMediaMetadata` de l’objet média avant d’appeler `trackSessionStart` :

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.AUTHORIZED] = "TRUE";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB  API Media Collection ]

Incluez `media.pass.auth` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.pass.auth": "TRUE"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
