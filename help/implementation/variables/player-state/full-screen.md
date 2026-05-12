---
title: Plein écran
description: Effectuez le suivi lorsque la visionneuse entre et quitte la lecture plein écran afin que le serveur principal puisse signaler l’engagement en plein écran.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 10%

---


# Plein écran

>[!BEGINSHADEBOX]

*Cette page couvre la collecte de données pour l’état du lecteur **Plein écran**. Voir [Flux affectés par le plein écran](/help/reporting/metrics/full-screen-streams-impacted.md), [Nombre de plein écran](/help/reporting/metrics/full-screen-count.md) et [Durée totale du plein écran](/help/reporting/metrics/full-screen-total-duration.md) pour les mesures de rapports correspondantes.*

>[!ENDSHADEBOX]

L’état du lecteur plein écran effectue le suivi lorsque la visionneuse entre en lecture plein écran et la quitte. Déclenchez un événement de début d’état lorsque la visionneuse passe en mode plein écran et un événement de fin d’état lorsque la visionneuse se ferme. Le serveur principal calcule trois mesures à partir de ces événements : les flux impactés, le nombre d’entrées d’état et la durée totale d’état.

| Propriété | Valeur |
| --- | --- |
| **Variables de données contextuelles** | `a.media.states.fullscreen.set`, `a.media.states.fullscreen.count`, `a.media.states.fullscreen.time` |
| **champ de collection XDM** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) et [`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) (entrées avec `name: "fullscreen"`) |
| **Obligatoire** | Non |
| **Envoyé avec** | Début état, fin état |

## SDK web

Utilisez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) pour envoyer un événement `media.statesUpdate` avec l’état ajouté à `statesStart` :

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

Lorsque la visionneuse quitte le mode plein écran, envoyez un autre événement dont le statut est défini sur `statesEnd` :

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

## SDK mobile

Utilisez `tracker.trackPlayerStateStart()` et `tracker.trackPlayerStateEnd()` avec la constante `MediaConstants.PlayerState.FULLSCREEN` .

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackPlayerStateStart(info: stateObject)
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackPlayerStateStart(stateObject)
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(stateObject)
```

## Roku (BrightScript)

Utilisez `sendMediaEvent` pour envoyer un événement `media.statesUpdate` avec l’état ajouté à `statesStart` :

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

Lorsque la visionneuse quitte le mode plein écran, envoyez un autre événement dont le statut est défini sur `statesEnd` :

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

Appelez le point d’entrée [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) avec le `fullscreen` en `statesStart` (ou `statesEnd` lorsque la visionneuse se ferme) :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "fullscreen" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## SDK Media

Utilisez `ADB.Media.createStateObject` et la constante `ADB.Media.PlayerState.FullScreen` :

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.FullScreen);

tracker.trackPlayerStateStart(stateObject);
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(stateObject);
```

## API Media Collection

Envoyez une requête POST `stateStart` lorsque la visionneuse passe en mode plein écran et une requête POST `stateEnd` lorsqu’elle se ferme :

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523850000 },
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.
