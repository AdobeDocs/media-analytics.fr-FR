---
title: MVPD
description: Définissez le distributeur de programmation vidéo multicanal lorsque l’utilisateur s’authentifie via Adobe Pass.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 15%

---


# MVPD

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **MVPD**. Voir [](/help/reporting/dimensions/mvpd.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable MVPD (Multichannel Video Programming Distributor) est le fournisseur de services par câble, satellite ou MVPD virtuel par lequel l’utilisateur s’est authentifié (par exemple, `"Comcast"`, `"DirecTV"` ou `"YouTubeTV"`). Définissez-le lorsque le contenu est bloqué derrière l’authentification Adobe Pass ou TV-Everywhere. Associez à [Autorisé](/help/implementation/variables/standard-metadata/authorized.md) pour suivre les sessions qui ont terminé l’authentification.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.pass.mvpd` |
| **champ de collection XDM** | [`mediaCollection.sessionDetails.mvpd`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obligatoire** | Non |
| **Envoyé avec** | Début et fin de la session |

## SDK web

`mvpd` à l’intérieur des `mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

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

## SDK mobile

Transmettez le MVPD en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.MVPD`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.MVPD] = "Comcast"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.MVPD] = "Comcast"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

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

## API Media Edge

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `mvpd` à l’intérieur du `mediaCollection.sessionDetails` :

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

## SDK Media

Transmettez le MVPD dans l’objet `contextData` à l’aide de `ADB.Media.VideoMetadataKeys.MVPD` :

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.MVPD] = "Comcast";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

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
