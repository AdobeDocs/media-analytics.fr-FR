---
title: Suivi des états du lecteur
description: Découvrez les événements d’état du lecteur et comment effectuer le suivi du plein écran, du mode silencieux, du sous-titrage, de l’image dans l’image et des états ciblés.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 12%

---


# Suivi des états du lecteur

Les événements d’état du lecteur suivent la façon dont les visionneuses interagissent avec les contrôles du lecteur tout au long d’une session. Ils sont facultatifs et non obligatoires pour les implémentations de suivi multimédia de base. Les cinq états traçables sont les suivants : `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture` et `inFocus`.

Les événements d’état du lecteur sont utiles pour comprendre l’utilisation des fonctionnalités d’accessibilité, par exemple la fréquence à laquelle les visionneuses activent le sous-titrage ou désactivent le son. Ils révèlent également des modèles de comportement de visualisation tels que l’affichage plein écran par rapport à l’affichage en ligne et le multitâche image dans image.

## Événements du lecteur

| Événement du lecteur | Action |
| --- | --- |
| Le lecteur passe à un état | Début de l’état de l’appel |
| Le lecteur quitte un état | Fin de l’état de l’appel |

## États standard et personnalisés

Cinq états de lecteur standards sont disponibles, et vous pouvez y ajouter vos propres états personnalisés.

| Nom d’état standard | Constante Media SDK | Nom de l’API Media Collection |
|----|----|----|
| Plein écran | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Sous-titrage | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Mode muet | `ADB.Media.PlayerState.Mute` | `mute` |
| Image dans l’image | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| Dans le focus | `ADB.Media.PlayerState.InFocus` | `inFocus` |

Voir [Variables d’état du lecteur](/help/implementation/variables/player-state/) pour consulter la référence complète des variables, y compris les chemins XDM et les définitions de mesures.

**États personnalisés :** vous pouvez créer des états personnalisés pour capturer d’autres comportements de lecteur spécifiques à votre application. Voir [Référence de l’API Media : `createStateObject`](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/) pour plus d’informations sur la création d’objets d’état personnalisés.

## Procédure de mise en œuvre

1. **Appel [Début de l’état](state-start.md)** lorsque le lecteur entre dans l’un des cinq états traçables. Plusieurs états peuvent être actifs en même temps et plusieurs états peuvent être démarrés dans le même appel d’événement.
1. **Appeler [Fin d’état](state-end.md)** lorsque le lecteur quitte un état. Il est possible de terminer plusieurs états dans le même appel d’événement, et de démarrer et de terminer plusieurs états ensemble dans un seul appel.

## Instructions

* Une session vidéo est limitée à 10 états du lecteur.
* Toutes les combinaisons d’états sont autorisées.
* Si plusieurs états du lecteur sont transmis, seuls les 10 premiers sont conservés et transférés en aval vers le serveur principal du média.
* Le nombre maximal de 10 états s’applique à tous les états, qu’ils soient ouverts ou fermés.
* Un état peut commencer et se terminer plusieurs fois et compte comme un seul état. Par exemple, `closedCaptioning` peut être démarré et arrêté cinq fois, mais compte comme un seul état.
* L’état du lecteur est calculé sur l’ensemble des états de lecture (sans fractionnement).
* Les états du lecteur sont capturés pour chaque session de lecture individuelle. L’état du lecteur n’est pas calculé sur l’ensemble des lectures.
* La connaissance de l’état de l’application n’est pas conservée après l’arrêt d’un état. Après la fin d’un état, celui-ci doit être redémarré pour continuer le suivi.

## Mise à jour simultanée de plusieurs états

Sur les plateformes XDM, plusieurs changements d’état peuvent être regroupés par lots en un seul appel `statesUpdate` à l’aide de tableaux dans `statesStart` et `statesEnd`. Sur les SDK mobiles, chaque changement d’état nécessite un appel distinct.

Les exemples suivants démarrent en mode silencieux et image dans image, puis passent en mode plein écran.

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

```javascript
// t0 — start mute and picture-in-picture together
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }, { name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});

// t1 — end mute and picture-in-picture; start full screen
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "mute" }, { name: "pictureInPicture" }],
      statesStart: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});

// t2 — end full screen
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Mobile SDK ne prend pas en charge le traitement par lots : envoyez un appel distinct pour chaque changement d’état.

```swift
// t0 — start mute and picture-in-picture
let muteState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.MUTE)
let pipState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.PICTURE_IN_PICTURE)
tracker.trackEvent(event: MediaEvent.StateStart, info: muteState, metadata: nil)
tracker.trackEvent(event: MediaEvent.StateStart, info: pipState, metadata: nil)

// t1 — end mute and picture-in-picture; start full screen
tracker.trackEvent(event: MediaEvent.StateEnd, info: muteState, metadata: nil)
tracker.trackEvent(event: MediaEvent.StateEnd, info: pipState, metadata: nil)
let fullscreenState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)
tracker.trackEvent(event: MediaEvent.StateStart, info: fullscreenState, metadata: nil)

// t2 — end full screen
tracker.trackEvent(event: MediaEvent.StateEnd, info: fullscreenState, metadata: nil)
```

>[!TAB Android]

Mobile SDK ne prend pas en charge le traitement par lots : envoyez un appel distinct pour chaque changement d’état.

```kotlin
// t0 — start mute and picture-in-picture
val muteState = Media.createStateObject(MediaConstants.PlayerState.MUTE)
val pipState = Media.createStateObject(MediaConstants.PlayerState.PICTURE_IN_PICTURE)
tracker.trackEvent(Media.Event.StateStart, muteState, null)
tracker.trackEvent(Media.Event.StateStart, pipState, null)

// t1 — end mute and picture-in-picture; start full screen
tracker.trackEvent(Media.Event.StateEnd, muteState, null)
tracker.trackEvent(Media.Event.StateEnd, pipState, null)
val fullscreenState = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)
tracker.trackEvent(Media.Event.StateStart, fullscreenState, null)

// t2 — end full screen
tracker.trackEvent(Media.Event.StateEnd, fullscreenState, null)
```

>[!TAB Roku Edge]

```brightscript
' t0 — start mute and picture-in-picture together
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{"name": "mute"}, {"name": "pictureInPicture"}],
            "playhead": 0
        }
    }
})

' t1 — end mute and picture-in-picture; start full screen
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{"name": "mute"}, {"name": "pictureInPicture"}],
            "statesStart": [{"name": "fullscreen"}],
            "playhead": 0
        }
    }
})

' t2 — end full screen
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{"name": "fullscreen"}],
            "playhead": 0
        }
    }
})
```

>[!TAB  API Media Edge ]

```sh
# t0 — start mute and picture-in-picture together
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{"name": "mute"}, {"name": "pictureInPicture"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:00:00+00:00"
    }
  }]
}'

# t1 — end mute and picture-in-picture; start full screen
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesEnd": [{"name": "mute"}, {"name": "pictureInPicture"}],
        "statesStart": [{"name": "fullscreen"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:01:00+00:00"
    }
  }]
}'

# t2 — end full screen
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesEnd": [{"name": "fullscreen"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:02:00+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Les modifications d’état multiples nécessitent des appels distincts.

```javascript
// t0 — start mute and picture-in-picture
var muteState = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
var pipState = ADB.Media.createStateObject(ADB.Media.PlayerState.PictureInPicture);
tracker.trackPlayerStateStart(muteState);
tracker.trackPlayerStateStart(pipState);

// t1 — end mute and picture-in-picture; start full screen
tracker.trackPlayerStateEnd(muteState);
tracker.trackPlayerStateEnd(pipState);
var fullscreenState = ADB.Media.createStateObject(ADB.Media.PlayerState.FullScreen);
tracker.trackPlayerStateStart(fullscreenState);

// t2 — end full screen
tracker.trackPlayerStateEnd(fullscreenState);
```

>[!TAB  Chromecast ]

Les modifications d’état multiples nécessitent des appels distincts.

```javascript
// t0 — start mute and picture-in-picture
var muteState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.Mute);
var pipState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.PictureInPicture);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, muteState, null);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, pipState, null);

// t1 — end mute and picture-in-picture; start full screen
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, muteState, null);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, pipState, null);
var fullscreenState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, fullscreenState, null);

// t2 — end full screen
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, fullscreenState, null);
```

>[!TAB Roku 2.x]

Le suivi de l’état du lecteur n’est pas disponible dans le SDK Roku 2.x. Pour suivre les états du lecteur, utilisez le SDK Roku Edge](/help/implementation/edge/roku.md).[

>[!TAB  API Media Collection ]

```json
// t0 — start mute and picture-in-picture together
{
  "eventType": "statesUpdate",
  "params": {
    "statesStart": [
      { "media.state.name": "mute" },
      { "media.state.name": "pictureInPicture" }
    ]
  },
  "playerTime": { "playhead": 0, "ts": 1569999130627 }
}

// t1 — end mute and picture-in-picture; start full screen
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      { "media.state.name": "mute" },
      { "media.state.name": "pictureInPicture" }
    ],
    "statesStart": [
      { "media.state.name": "fullScreen" }
    ]
  },
  "playerTime": { "playhead": 0, "ts": 1569999230627 }
}

// t2 — end full screen
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [{ "media.state.name": "fullScreen" }]
  },
  "playerTime": { "playhead": 0, "ts": 1569999330627 }
}
```

>[!ENDTABS]

## Pause longue

Lorsqu’une session vidéo a une durée de pause supérieure à 30 minutes, l’API nécessite une nouvelle session. Générez un nouvel ID de session et conservez tous les états actifs afin qu’ils puissent être restaurés avec des événements `stateStart` juste après le nouvel appel `sessionStart`.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

Une fois l’`sessionEnd` envoyée, démarrez une nouvelle session et renvoyez immédiatement les états actifs :

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

## Mesures d’état

Trois mesures sont calculées pour chaque état suivi et envoyées à Adobe Analytics lors de l’appel de fermeture du média :

| Mesure | Clé de données contextuelles | Description |
| --- | --- | --- |
| État défini | `a.media.states.[state.name].set = true` | `true` si le statut a été défini au moins une fois pendant la lecture |
| Nombre d’états | `a.media.states.[state.name].count = 4` | Nombre de fois où le statut s’est produit pendant la lecture |
| Heure de l’état | `a.media.states.[state.name].time = 240` | Temps total (secondes) passé dans l’état pendant la lecture |
