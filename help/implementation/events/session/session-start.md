---
title: Début de la session
description: Signalez le début d’une session multimédia et obtenez l’identifiant de session requis pour tous les événements suivants.
feature: Streaming Media
role: Developer
source-git-commit: 6534e4c76dcb4113bbbb99aed2a0e350f9256b15
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 10%

---


# Début de la session

L’événement de début de session ouvre une session de suivi multimédia. Il doit s’agir du premier événement envoyé pour toute lecture. La réponse renvoie un ID de session que tous les événements suivants d’une même session doivent inclure.

Une session expire automatiquement si **aucun événement n’est reçu pendant 10 minutes** ou s’il n’y a **aucun mouvement du curseur de lecture pendant 30 minutes**. Si une session expire, vous devez appeler à nouveau le démarrage de la session pour obtenir un nouvel ID de session.

* **Conditions préalables** : aucun ; toujours le premier événement
* **Mesure associée** : [Le média commence](/help/reporting/metrics/media-starts.md)

## SDK web

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec les `eventType: "media.sessionStart"` et les `sessionDetails` requises. La réponse inclut l’ID de session dans `handle[].payload[].sessionId` (type `media-analytics:new-session`). Stockez cette valeur et transmettez-la comme `sessionID` dans tous les événements suivants.

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

## SDK mobile

Appelez `trackSessionStart` avec un objet média et des métadonnées facultatives.

**iOS (Swift)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                               id: "video-id-123",
                                           length: 128,
                                       streamType: MediaConstants.StreamType.VOD,
                                        mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val mediaObject = Media.createMediaObject("video-123",
                                          "video-id-123",
                                          128,
                                          MediaConstants.StreamType.VOD,
                                          Media.MediaType.Video)

tracker.trackSessionStart(mediaObject, null)
```

## Roku (BrightScript)

Appelez `createMediaSession` avec les détails de session requis :

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

## API Media Edge

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart). La réponse inclut l’ID de session dans `handle[].payload[].sessionId` (type `media-analytics:new-session`).

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "playerName": "HTML5 Player",
          "contentType": "VOD",
          "length": 128,
          "channel": "Sports"
        },
        "playhead": 0
      }
    }
  }]
}'
```

## SDK Media

Appelez `trackSessionStart` avec un objet média créé à l’aide de `ADB.Media.createMediaObject` :

```javascript
var mediaObject = ADB.Media.createMediaObject(
  "video-123",                  // name
  "video-id-123",               // media ID
  128,                          // length (seconds)
  ADB.Media.StreamType.VOD,     // stream type
  ADB.Media.MediaType.Video     // media type
);

tracker.trackSessionStart(mediaObject, null);
```

## API Media Collection

Envoyez une `sessionStart` POST au point d’entrée [sessions](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md). L’en-tête du `Location` de réponse contient l’ID de session à utiliser dans toutes les requêtes d’événement ultérieures.

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports",
    "media.playerName": "HTML5 Player",
    "media.contentType": "vod",
    "media.length": 128,
    "media.id": "video-123"
  }
}
```
