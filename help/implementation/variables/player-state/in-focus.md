---
title: Dans le focus
description: Effectuez le suivi lorsque le lecteur est ciblé sur l’écran de la visionneuse afin que le serveur principal puisse signaler l’engagement du focus.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 5%

---


# Dans le focus

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour l’état du lecteur **In focus**. Voir [Flux impactés par dans le focus](/help/reporting/metrics/in-focus-streams-impacted.md), [Nombre de focus](/help/reporting/metrics/in-focus-count.md) et [Durée totale du focus](/help/reporting/metrics/in-focus-total-duration.md) pour les mesures de rapports correspondantes.*

>[!ENDSHADEBOX]

L’état du lecteur ciblé indique à quel moment le lecteur retient l’attention de la visionneuse. Déclenchez un événement de début d’état lorsque le lecteur reçoit le focus (généralement lorsque l’onglet ou la fenêtre du lecteur devient actif) et un événement de fin d’état lorsque le lecteur perd le focus. Le serveur principal calcule trois mesures à partir de ces événements : les flux impactés, le nombre d’entrées d’état et la durée totale d’état.

| Propriété | Valeur |
| --- | --- |
| **Variables de données contextuelles** | `a.media.states.infocus.set`, `a.media.states.infocus.count`, `a.media.states.infocus.time` |
| **champ de collection XDM** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) et [`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) (entrées avec `name: "inFocus"`) |
| **caractéristiques** | `c_contextdata.a.media.states.infocus.set`, `c_contextdata.a.media.states.infocus.count`, `c_contextdata.a.media.states.infocus.time` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de l’état](/help/implementation/events/player-state/state-start.md), [fin de l’état](/help/implementation/events/player-state/state-end.md) |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

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

>[!TAB iOS]

Utilisez `tracker.trackPlayerStateStart()` et `tracker.trackPlayerStateEnd()` avec la constante `MediaConstants.PlayerState.IN_FOCUS` .

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.IN_FOCUS)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

Utilisez `tracker.trackPlayerStateStart()` et `tracker.trackPlayerStateEnd()` avec la constante `MediaConstants.PlayerState.IN_FOCUS` .

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.IN_FOCUS)

tracker.trackPlayerStateStart(stateObject)
tracker.trackPlayerStateEnd(stateObject)
```

>[!TAB Roku]

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

>[!TAB  API Media Edge ]

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

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Utilisez `ADB.Media.createStateObject` et la constante `ADB.Media.PlayerState.InFocus` :

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.InFocus);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB  Chromecast ]

Utilisez `ADBMobile.media.createStateObject` avec la chaîne `"inFocus"` directement, car Chromecast ne dispose pas de constantes `PlayerState` nommées :

```javascript
var stateObject = ADBMobile.media.createStateObject("inFocus");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the player loses focus:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB  API Media Collection ]

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

>[!ENDTABS]
