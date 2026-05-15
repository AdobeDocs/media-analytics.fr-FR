---
title: Play
description: Signalez que le lecteur multimédia est entré en état de lecture.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 17%

---


# Play

L’événement de lecture signale que le lecteur multimédia a changé d’état pour la lecture. Envoyez-le au début initial du contenu, lors de la lecture automatique et chaque fois que le lecteur reprend après une pause ou une mise en mémoire tampon. Il n’existe pas d’événement de reprise distinct ; un événement de lecture après [Début de pause](pause-start.md) ou [Début de la mémoire tampon](buffer-start.md) sert de reprise.

* **Conditions préalables** : [début de session](../session/session-start.md)
* **Mesure associée** : [Le contenu commence](/help/reporting/metrics/content-starts.md)

## SDK web

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec `eventType: "media.play"` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.play",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK mobile

Appelez `trackPlay` lorsque le lecteur multimédia commence ou reprend la lecture.

**iOS (Swift)**

```swift
tracker.trackPlay()
```

**Android (Kotlin)**

```kotlin
tracker.trackPlay()
```

## Roku (BrightScript)

Appelez `sendMediaEvent` avec `eventType: "media.play"` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [play](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/play/) :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/play?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.play",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK Media

Appelez `trackPlay` lorsque le lecteur multimédia commence ou reprend la lecture :

```javascript
tracker.trackPlay();
```

## API Media Collection

Envoyez une `play` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "play"
}
```
