---
title: Début de l’état
description: Indique que le lecteur multimédia est entré en état de lecteur suivi.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 13%

---


# Début de l’état

L’événement de début d’état indique que le lecteur multimédia est entré dans un état suivi, tel que plein écran, muet ou sous-titrage. Un lecteur peut se trouver dans plusieurs états simultanément, et les états peuvent être démarrés et terminés dans le même appel d’événement. Fermez chaque état avec un événement [State end](state-end.md).

Noms d’état valides : `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture`, `inFocus`

* **Conditions préalables** : [début de session](../session/session-start.md)
* **Mesure associée** : varie en fonction de l’état. Voir [Suivi de l’état du lecteur](/help/use-cases/player-state-tracking/implementation-and-reporting.md)

## SDK web

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec `eventType: "media.statesUpdate"` et le nom de l’état en `statesStart` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Plusieurs états peuvent être démarrés dans le même appel :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [
        { name: "fullscreen" },
        { name: "mute" }
      ],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

## SDK mobile

Utilisez `trackPlayerStateStart` avec un objet d’état créé à partir de la constante de `MediaConstants.PlayerState` appropriée.

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateStart, info: stateObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateStart, stateObject, null)
```

## Roku (BrightScript)

Appelez `sendMediaEvent` avec `eventType: "media.statesUpdate"` et le nom de l’état en `statesStart` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "fullscreen" }],
            "playhead": 60
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) avec le nom d’état en `statesStart` :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 60,
        "statesStart": [{ "name": "fullscreen" }]
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

tracker.trackPlayerStateStart(stateObject);
```

## API Media Collection

Envoyez une `stateStart` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```
