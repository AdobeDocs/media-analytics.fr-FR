---
title: Mode muet
description: Suivez le moment où la visionneuse désactive le son et le réactive pour que le serveur principal puisse signaler l’engagement du mode silencieux.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 6%

---


# Mode muet

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour l’état du lecteur **Muet**. Voir [Flux impactés par le mode muet](/help/reporting/metrics/mute-streams-impacted.md), [Nombre de messages muets](/help/reporting/metrics/mute-count.md) et [Durée totale du mode muet](/help/reporting/metrics/mute-total-duration.md) pour les mesures de rapports correspondantes.*

>[!ENDSHADEBOX]

Le statut Silence du lecteur indique quand la visionneuse désactive le son. Déclenchez un événement de début d’état lorsque la visionneuse désactive le son et un événement de fin d’état lorsque la visionneuse le réactive. Le serveur principal calcule trois mesures à partir de ces événements : les flux impactés, le nombre d’entrées d’état et la durée totale d’état.

| Propriété | Valeur |
| --- | --- |
| **Variables de données contextuelles** | `a.media.states.mute.set`, `a.media.states.mute.count`, `a.media.states.mute.time` |
| **champ de collection XDM** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) et [`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) (entrées avec `name: "mute"`) |
| **caractéristiques** | `c_contextdata.a.media.states.mute.set`, `c_contextdata.a.media.states.mute.count`, `c_contextdata.a.media.states.mute.time` |
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

>[!TAB iOS]

Utilisez `tracker.trackPlayerStateStart()` et `tracker.trackPlayerStateEnd()` avec la constante `MediaConstants.PlayerState.MUTE` .

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.MUTE)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

Utilisez `tracker.trackPlayerStateStart()` et `tracker.trackPlayerStateEnd()` avec la constante `MediaConstants.PlayerState.MUTE` .

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.MUTE)

tracker.trackPlayerStateStart(stateObject)
tracker.trackPlayerStateEnd(stateObject)
```

>[!TAB Roku Edge]

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

>[!TAB  API Media Edge ]

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

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Utilisez `ADB.Media.createStateObject` et la constante `ADB.Media.PlayerState.Mute` :

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB  Chromecast ]

Utilisez `ADBMobile.media.createStateObject` avec la chaîne `"mute"` directement, car Chromecast ne dispose pas de constantes `PlayerState` nommées :

```javascript
var stateObject = ADBMobile.media.createStateObject("mute");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the viewer unmutes:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB Roku 2.x]

Le suivi de l’état du lecteur n’est pas disponible dans le SDK Roku 2.x. Pour suivre les états du lecteur, utilisez le SDK Roku Edge](/help/implementation/edge/roku.md).[

>[!TAB  API Media Collection ]

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

>[!ENDTABS]
