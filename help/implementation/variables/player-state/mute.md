---
title: Mode muet
description: Suivez le moment où la visionneuse désactive le son et le réactive pour que le serveur principal puisse signaler l’engagement du mode silencieux.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 10%

---


# Mode muet

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour l’état du lecteur **Muet**. Voir [Flux impactés par le mode muet](/help/reporting/metrics/mute-streams-impacted.md), [Nombre de messages muets](/help/reporting/metrics/mute-count.md) et [Durée totale du mode muet](/help/reporting/metrics/mute-total-duration.md) pour les mesures de rapports correspondantes.*

>[!ENDSHADEBOX]

Le statut Silence du lecteur indique quand la visionneuse désactive le son. Déclenchez un événement de début d’état lorsque la visionneuse désactive le son et un événement de fin d’état lorsque la visionneuse le réactive. Le serveur principal calcule trois mesures à partir de ces événements : les flux impactés, le nombre d’entrées d’état et la durée totale d’état.

| Propriété | Valeur |
| --- | --- |
| **Variables de données contextuelles** | `a.media.states.mute.set`, `a.media.states.mute.count`, `a.media.states.mute.time` |
| **champ de collection XDM** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/media-collection-details) et [`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/media-collection-details) (entrées avec `name: "mute"`) |
| **Obligatoire** | Non |
| **Envoyé avec** | Début état, fin état |

## SDK web

Utilisez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) pour envoyer un événement `media.statesUpdate` avec l’état ajouté à `statesStart` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Lorsque la visionneuse réactive le son, envoyez un autre événement dont le statut est défini sur `statesEnd` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "mute" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## SDK mobile

Utilisez `tracker.trackPlayerStateStart()` et `tracker.trackPlayerStateEnd()` avec la constante `MediaConstants.PlayerState.MUTE` .

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.MUTE)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.MUTE)

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
            "statesStart": [{ "name": "mute" }],
            "playhead": 60
        }
    }
})
```

Lorsque la visionneuse réactive le son, envoyez un autre événement dont le statut est défini sur `statesEnd` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "mute" }],
            "playhead": 90
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) avec le `mute` en `statesStart` (ou `statesEnd` lorsque la visionneuse active le son) :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "mute" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## SDK Media

Utilisez `ADB.Media.createStateObject` et la constante `ADB.Media.PlayerState.Mute` :

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## API Media Collection

Envoyez une requête POST `stateStart` lorsque la visionneuse désactive le son, et une requête POST `stateEnd` lorsqu’elle le fait :

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "mute"
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.
