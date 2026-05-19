---
title: Changement de débit
description: Signale que le débit de lecture a changé.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 14%

---


# Changement de débit

L’événement de changement de débit indique que le lecteur a négocié un nouveau débit de lecture. Envoyez-le chaque fois que le débit change pendant la lecture. Incluez la nouvelle valeur de débit dans les données de la QoE afin que le serveur principal puisse calculer [débit moyen](/help/reporting/metrics/average-bitrate.md) et la dimension par débit-intervalle.

* **Conditions préalables** : [début de session](../session/session-start.md)
* **Mesure associée** : [modifications de débit](/help/reporting/metrics/bitrate-changes.md)

## SDK web

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec `eventType: "media.bitrateChange"` et le nouveau débit en `qoeDataDetails` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## SDK mobile

Créez un objet QoE avec le nouveau débit et mettez à jour le dispositif de suivi avant le déclenchement de l’événement de changement de débit.

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(3200, 0, 24, 0)

tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

## Roku (BrightScript)

Appelez `sendMediaEvent` avec `eventType: "media.bitrateChange"` et le nouveau débit en `qoeDataDetails` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 90
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/) avec le nouveau débit en `qoeDataDetails` :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/bitrateChange?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 3200
        },
        "sessionID": "{sid}",
        "playhead": 90
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK Media

Créez un objet QoE avec le nouveau débit et mettez à jour le dispositif de suivi :

```javascript
var qoeObject = ADB.Media.createQoEObject(
  3200,  // bitrate (kbps)
  0,     // startup time (ms)
  24,    // fps
  0      // dropped frames
);

tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

## API Media Collection

Envoyez une `bitrateChange` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) avec le nouveau débit en `qoeData` :

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "qoeData": {
    "media.qoe.bitrate": 3200
  }
}
```
