---
title: Sous-titrage
description: Suivez quand la visionneuse active et désactive le sous-titrage pour que le serveur principal puisse signaler l’engagement du sous-titrage.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 9%

---


# Sous-titrage

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour l’état du lecteur **Sous-titrage**. Consultez [Flux affectés par le sous-titrage](/help/reporting/metrics/closed-captioning-streams-impacted.md), [Nombre de sous-titrages](/help/reporting/metrics/closed-captioning-count.md) et [Durée totale du sous-titrage](/help/reporting/metrics/closed-captioning-total-duration.md) pour les mesures de rapports correspondantes.*

>[!ENDSHADEBOX]

L’état du lecteur de sous-titrage est suivi lorsque la visionneuse active ou désactive les sous-titres. Déclenchez un événement de début d’état lorsque les sous-titres sont activés et un événement de fin d’état lorsque les sous-titres sont désactivés. Le serveur principal calcule trois mesures à partir de ces événements : les flux impactés, le nombre d’entrées d’état et la durée totale d’état.

| Propriété | Valeur |
| --- | --- |
| **Variables de données contextuelles** | `a.media.states.closedcaptioning.set`, `a.media.states.closedcaptioning.count`, `a.media.states.closedcaptioning.time` |
| **champ de collection XDM** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/media-collection-details) et [`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/media-collection-details) (entrées avec `name: "closedCaptioning"`) |
| **caractéristiques** | `c_contextdata.a.media.states.closedcaptioning.set`, `c_contextdata.a.media.states.closedcaptioning.count`, `c_contextdata.a.media.states.closedcaptioning.time` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de l’état](/help/implementation/events/player-state/state-start.md), [fin de l’état](/help/implementation/events/player-state/state-end.md) |

## SDK web

Utilisez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) pour envoyer un événement `media.statesUpdate` avec l’état ajouté à `statesStart` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "closedCaptioning" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Lorsque la visionneuse désactive les sous-titres, envoyez un autre événement dont le statut est en `statesEnd` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "closedCaptioning" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## SDK mobile

Utilisez `tracker.trackPlayerStateStart()` et `tracker.trackPlayerStateEnd()` avec la constante `MediaConstants.PlayerState.CLOSED_CAPTION` .

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.CLOSED_CAPTION)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.CLOSED_CAPTION)

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
            "statesStart": [{ "name": "closedCaptioning" }],
            "playhead": 60
        }
    }
})
```

Lorsque la visionneuse désactive les sous-titres, envoyez un autre événement dont le statut est en `statesEnd` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "closedCaptioning" }],
            "playhead": 90
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) avec des `closedCaptioning` en `statesStart` (ou `statesEnd` lorsque la visionneuse désactive les sous-titres) :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "closedCaptioning" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## SDK Media

Utilisez `ADB.Media.createStateObject` et la constante `ADB.Media.PlayerState.ClosedCaptioning` :

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.ClosedCaptioning);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## API Media Collection

Envoyez une requête POST `stateStart` lorsque les légendes sont activées et une requête POST `stateEnd` lorsqu’elles sont désactivées :

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "closedCaptioning"
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.
