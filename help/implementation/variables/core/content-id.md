---
title: Identifiant de contenu
description: Identifiez de manière unique un élément de contenu multimédia.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 9%

---


# Identifiant de contenu

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Content ID**. Voir [Contenu](/help/reporting/dimensions/content.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable d’ID de contenu identifie de manière unique chaque élément de contenu multimédia. Elle est requise pour toutes les implémentations de médias en flux continu et est la clé principale de la dimension de reporting de contenu. Définissez-le au début de la session et maintenez-le stable sur toutes les sessions pour la même ressource.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.name` |
| **champ de collection XDM** | [`xdm.mediaCollection.sessionDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.name` |
| **Obligatoire** | Oui |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`name` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "My Video",
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

Transmettez l’ID de contenu comme argument de `mediaId` à `createMediaObject`.

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

Transmettez l’ID de contenu comme argument de `mediaId` à `createMediaObject`.

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku]

`name` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de `createMediaSession` :

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

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `name` (l’identifiant de contenu) à l’intérieur du `xdm.mediaCollection.sessionDetails` :

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

Transmettez l’ID de contenu comme deuxième argument à `ADB.Media.createMediaObject` :

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",               // name (friendly name)
  "video-123",              // media ID — Content ID
  128,                      // length (seconds)
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB  Chromecast ]

Transmettez l’ID de contenu comme deuxième argument à `ADBMobile.media.createMediaObject` :

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

>[!TAB  API Media Collection ]

Incluez `media.id` dans l’objet `params` de votre `sessionStart` requête POST :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.id": "video-123"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
