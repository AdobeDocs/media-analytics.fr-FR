---
title: Image dans l’image
description: Effectuez le suivi lorsque la visionneuse entre et quitte la lecture image par image afin que le serveur principal puisse signaler l’engagement PiP.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 8%

---


# Image dans l’image

>[!BEGINSHADEBOX]

*Cette page couvre la collecte de données pour l’état du lecteur **Image en image**. Voir [Flux affectés par image dans l’image](/help/reporting/metrics/picture-in-picture-streams-impacted.md), [Image dans le nombre d’images](/help/reporting/metrics/picture-in-picture-count.md) et [Durée totale de l’image dans l’image](/help/reporting/metrics/picture-in-picture-total-duration.md) pour les mesures de rapports correspondantes.*

>[!ENDSHADEBOX]

L’image dans le lecteur d’images suit le moment où la visionneuse entre et sort de la lecture d’image dans l’image. Déclenchez un événement de début d’état lorsque l’image dans l’image commence et un événement de fin d’état lorsqu’il se termine. Le serveur principal calcule trois mesures à partir de ces événements : les flux impactés, le nombre d’entrées d’état et la durée totale d’état.

| Propriété | Valeur |
| --- | --- |
| **Variables de données contextuelles** | `a.media.states.pictureinpicture.set`, `a.media.states.pictureinpicture.count`, `a.media.states.pictureinpicture.time` |
| **champ de collection XDM** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/media-collection-details) et [`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/media-collection-details) (entrées avec `name: "pictureInPicture"`) |
| **caractéristiques** | `c_contextdata.a.media.states.pictureinpicture.set`, `c_contextdata.a.media.states.pictureinpicture.count`, `c_contextdata.a.media.states.pictureinpicture.time` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de l’état](/help/implementation/events/player-state/state-start.md), [fin de l’état](/help/implementation/events/player-state/state-end.md) |

## SDK web

Utilisez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) pour envoyer un événement `media.statesUpdate` avec l’état ajouté à `statesStart` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Lorsque la visionneuse quitte la fonctionnalité image dans image, envoyez un autre événement dont le statut est en `statesEnd` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## SDK mobile

Utilisez `tracker.trackPlayerStateStart()` et `tracker.trackPlayerStateEnd()` avec la constante `MediaConstants.PlayerState.PICTURE_IN_PICTURE` .

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.PICTURE_IN_PICTURE)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.PICTURE_IN_PICTURE)

tracker.trackPlayerStateStart(stateObject)
tracker.trackPlayerStateEnd(stateObject)
```

## Roku (BrightScript)

Utilisez `sendMediaEvent` pour envoyer un événement `media.statesUpdate` avec l’état ajouté à `statesStart` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "pictureInPicture" }],
            "playhead": 60
        }
    }
})
```

Lorsque la visionneuse quitte la fonctionnalité image dans image, envoyez un autre événement dont le statut est en `statesEnd` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "pictureInPicture" }],
            "playhead": 90
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) avec le `pictureInPicture` en `statesStart` (ou `statesEnd` lorsque la visionneuse quitte PiP) :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "pictureInPicture" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## SDK Media

Utilisez `ADB.Media.createStateObject` et la constante `ADB.Media.PlayerState.PictureInPicture` :

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.PictureInPicture);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## API Media Collection

Envoyez une requête POST `stateStart` lorsque la saisie d’image commence et une requête POST `stateEnd` lorsqu’elle se termine :

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "pictureInPicture"
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.
