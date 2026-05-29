---
title: Début de l’état
description: Indique que le lecteur multimédia est entré en état de lecteur suivi.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 7%

---


# Début de l’état

L’événement de début d’état indique que le lecteur multimédia est entré dans un état suivi, tel que plein écran, muet ou sous-titrage. Un lecteur peut se trouver dans plusieurs états simultanément, et les états peuvent être démarrés et terminés dans le même appel d’événement. Fermez chaque état avec un événement [State end](state-end.md).

Noms d’état valides : `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture`, `inFocus`

* **Conditions préalables** : [début de session](../session/session-start.md)
* **Mesure associée** : varie selon l’état. Consultez [Suivi des états du lecteur](/help/implementation/events/player-state/overview.md).

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

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

>[!TAB iOS]

Utilisez `trackPlayerStateStart` avec un objet d’état créé à partir de la constante de `MediaConstants.PlayerState` appropriée.

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateStart, info: stateObject, metadata: nil)
```

>[!TAB Android]

Utilisez `trackPlayerStateStart` avec un objet d’état créé à partir de la constante de `MediaConstants.PlayerState` appropriée.

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateStart, stateObject, null)
```

>[!TAB Roku]

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

>[!TAB  API Media Edge ]

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

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Utilisez `ADB.Media.createStateObject` avec la constante de `ADB.Media.PlayerState` appropriée :

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Fullscreen);

tracker.trackPlayerStateStart(stateObject);
```

>[!TAB  Chromecast ]

Utilisez `ADBMobile.media.createStateObject` avec la constante de `ADBMobile.media.PlayerState` appropriée :

```javascript
var stateObject = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);

ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
```

>[!TAB  API Media Collection ]

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

>[!ENDTABS]
