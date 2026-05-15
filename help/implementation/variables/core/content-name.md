---
title: Nom du contenu
description: Définissez le nom convivial du contenu (le titre lisible par l’utilisateur affiché dans les rapports).
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 15%

---


# Nom du contenu

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Content name**. Voir [Nom du contenu](/help/reporting/dimensions/content-name.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable de nom du contenu est le titre du contenu lisible par l’utilisateur (par exemple, `"Blinding Light"`). Elle est facultative, mais vivement recommandée. Dans le schéma XDM, il mappe sur `friendlyName` (non `name` ; `name` contient l’ID de contenu).

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.friendlyName` |
| **champ de collection XDM** | [`mediaCollection.sessionDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.friendlyName` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## SDK web

`friendlyName` à l’intérieur des `mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "Blinding Light",
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

## SDK mobile

Transmettez le nom lisible par l’utilisateur comme premier argument (`name`) à `createMediaObject`. Le deuxième argument est l’identifiant du contenu.

**iOS (Swift)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "Blinding Light",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
var mediaInfo = Media.createMediaObject("Blinding Light",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

## Roku (BrightScript)

`friendlyName` à l’intérieur des `mediaCollection.sessionDetails` lors de l’appel de `createMediaSession` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "friendlyName": "Blinding Light",
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

## API Media Edge

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `friendlyName` à l’intérieur du `mediaCollection.sessionDetails` :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "friendlyName": "Blinding Light",
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

## SDK Media

Transmettez le nom lisible par l’utilisateur comme premier argument à `ADB.Media.createMediaObject` :

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "Blinding Light",    // name (friendly name)
  "video-123",              // media ID
  128,
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Incluez `media.name` dans l’objet `params` de votre `sessionStart` requête POST :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.name": "Blinding Light"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.
