---
title: Fin de l’état
description: Signalez que le lecteur multimédia a quitté un état de lecteur suivi.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 13%

---


# Fin de l’état

L’événement de fin d’état indique que le lecteur multimédia a quitté un état suivi, tel que le plein écran, le silence ou le sous-titrage. Envoyez-le pour fermer un état ouvert par [State start](state-start.md). Les états peuvent être démarrés et terminés dans le même appel d’événement. Un lecteur peut quitter plusieurs états simultanément.

Noms d’état valides : `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture`, `inFocus`

* **Conditions préalables** : [début de session](../session/session-start.md), [début d’état](state-start.md)
* **Mesure associée** : varie en fonction de l’état. Voir [Suivi de l’état du lecteur](/help/use-cases/player-state-tracking/implementation-and-reporting.md)

## SDK web

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec `eventType: "media.statesUpdate"` et le nom de l’état en `statesEnd` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

Les états peuvent être démarrés et terminés dans le même appel :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }],
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## SDK mobile

Utilisez `trackPlayerStateEnd` avec un objet d’état créé à partir de la constante de `MediaConstants.PlayerState` appropriée.

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateEnd, info: stateObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateEnd, stateObject, null)
```

## Roku (BrightScript)

Appelez `sendMediaEvent` avec `eventType: "media.statesUpdate"` et le nom de l’état en `statesEnd` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "fullscreen" }],
            "playhead": 90
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) avec le nom d’état en `statesEnd` :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 90,
        "statesEnd": [{ "name": "fullscreen" }]
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK Media

Utilisez `ADB.Media.createStateObject` avec la constante de `ADB.Media.PlayerState` appropriée :

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Fullscreen);

tracker.trackPlayerStateEnd(stateObject);
```

## API Media Collection

Envoyez une `stateEnd` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```
