---
title: Dans le focus
description: Effectuez le suivi lorsque le lecteur est ciblé sur l’écran de la visionneuse afin que le serveur principal puisse signaler l’engagement du focus.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 9%

---


# Dans le focus

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour l’état du lecteur **In focus**. Voir [Flux impactés par dans le focus](/help/reporting/metrics/in-focus-streams-impacted.md), [Nombre de focus](/help/reporting/metrics/in-focus-count.md) et [Durée totale du focus](/help/reporting/metrics/in-focus-total-duration.md) pour les mesures de rapports correspondantes.*

>[!ENDSHADEBOX]

L’état du lecteur ciblé indique à quel moment le lecteur retient l’attention de la visionneuse. Déclenchez un événement de début d’état lorsque le lecteur reçoit le focus (généralement lorsque l’onglet ou la fenêtre du lecteur devient actif) et un événement de fin d’état lorsque le lecteur perd le focus. Le serveur principal calcule trois mesures à partir de ces événements : les flux impactés, le nombre d’entrées d’état et la durée totale d’état.

| Propriété | Valeur |
| --- | --- |
| **Variables de données contextuelles** | `a.media.states.infocus.set`, `a.media.states.infocus.count`, `a.media.states.infocus.time` |
| **champ de collection XDM** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) et [`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) (entrées avec `name: "inFocus"`) |
| **Obligatoire** | Non |
| **Envoyé avec** | Début état, fin état |

## SDK web

Utilisez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) pour envoyer un événement `media.statesUpdate` avec l’état ajouté à `statesStart` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "inFocus" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Lorsque le lecteur perd le focus, envoyez un autre événement dont le statut est défini sur `statesEnd` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "inFocus" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## SDK mobile

Utilisez `tracker.trackPlayerStateStart()` et `tracker.trackPlayerStateEnd()` avec la constante `MediaConstants.PlayerState.IN_FOCUS` .

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.IN_FOCUS)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.IN_FOCUS)

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
            "statesStart": [{ "name": "inFocus" }],
            "playhead": 60
        }
    }
})
```

Lorsque le lecteur perd le focus, envoyez un autre événement dont le statut est défini sur `statesEnd` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "inFocus" }],
            "playhead": 90
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) avec des `inFocus` en `statesStart` (ou `statesEnd` lorsque le lecteur perd le focus) :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "inFocus" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## SDK Media

Utilisez `ADB.Media.createStateObject` et la constante `ADB.Media.PlayerState.InFocus` :

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.InFocus);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## API Media Collection

Envoyez une requête POST `stateStart` lorsque le lecteur reçoit le focus, et une requête POST `stateEnd` lorsqu’il le perd :

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "inFocus"
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.
