---
title: Plein écran
description: Effectuez le suivi lorsque la visionneuse entre et quitte la lecture plein écran afin que le serveur principal puisse signaler l’engagement en plein écran.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 7%

---


# Plein écran

>[!BEGINSHADEBOX]

*Cette page couvre la collecte de données pour l’état du lecteur **Plein écran**. Voir [Flux affectés par le plein écran](/help/reporting/metrics/full-screen-streams-impacted.md), [Nombre de plein écran](/help/reporting/metrics/full-screen-count.md) et [Durée totale du plein écran](/help/reporting/metrics/full-screen-total-duration.md) pour les mesures de rapports correspondantes.*

>[!ENDSHADEBOX]

L’état du lecteur plein écran effectue le suivi lorsque la visionneuse entre en lecture plein écran et la quitte. Déclenchez un événement de début d’état lorsque la visionneuse passe en mode plein écran et un événement de fin d’état lorsque la visionneuse se ferme. Le serveur principal calcule trois mesures à partir de ces événements : les flux impactés, le nombre d’entrées d’état et la durée totale d’état.

| Propriété | Valeur |
| --- | --- |
| **Variables de données contextuelles** | `a.media.states.fullscreen.set`, `a.media.states.fullscreen.count`, `a.media.states.fullscreen.time` |
| **champ de collection XDM** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) et [`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) (entrées avec `name: "fullscreen"`) |
| **caractéristiques** | `c_contextdata.a.media.states.fullscreen.set`, `c_contextdata.a.media.states.fullscreen.count`, `c_contextdata.a.media.states.fullscreen.time` |
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

>[!TAB iOS]

Utilisez `tracker.trackPlayerStateStart()` et `tracker.trackPlayerStateEnd()` avec la constante `MediaConstants.PlayerState.FULLSCREEN` .

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackPlayerStateStart(info: stateObject)
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

Utilisez `tracker.trackPlayerStateStart()` et `tracker.trackPlayerStateEnd()` avec la constante `MediaConstants.PlayerState.FULLSCREEN` .

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackPlayerStateStart(stateObject)
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(stateObject)
```

>[!TAB Roku]

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

>[!TAB  API Media Edge ]

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

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Utilisez `ADB.Media.createStateObject` et la constante `ADB.Media.PlayerState.FullScreen` :

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.FullScreen);

tracker.trackPlayerStateStart(stateObject);
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB  Chromecast ]

Utilisez `ADBMobile.media.createStateObject` avec la chaîne `"fullscreen"` directement, car Chromecast ne dispose pas de constantes `PlayerState` nommées :

```javascript
var stateObject = ADBMobile.media.createStateObject("fullscreen");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the user exits full-screen:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB  API Media Collection ]

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

>[!ENDTABS]
