---
title: Mise à jour simultanée de plusieurs états du lecteur
description: Cette rubrique décrit la fonctionnalité de tracking de plusieurs états du lecteur.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 7a512a81-a6d1-4d0c-a4fe-91e9b11419db
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 100%

---

# Suivi de plusieurs états du lecteur

Parfois, deux états du lecteur démarrent et se terminent au même moment, ou la fin d’un état est également le début d’un autre, comme illustré dans l’image suivante :

![Plusieurs états du lecteur](assets/multiple-player-states.png)

L’implémentation actuelle permet les deux scénarios :
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

Toutefois, cette implémentation nécessite que vous émettiez plusieurs événements `stateStart` et `stateEnd` pour signaler plusieurs changements d’état simultanés. Afin
d’optimiser ce comportement commun, un nouveau type d’événement `statesUpdate` a été implémenté. Celui-ci met fin à une liste d’états
tout en démarrant une liste de nouveaux états.

Grâce au nouvel événement `statesUpdate`, la liste ci-dessus devient :
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

Le nombre d’appels de mises à jour d’état a été réduit de six à trois pour le même comportement. Le dernier événement
aurait également pu être un simple `stateEnd(fullScreen)`.

## Implémentation de l’API Media Collection {#mpst-api}

Vous pouvez utiliser l’API Media Collection pour implémenter le tracking de plusieurs états du lecteur.

### Exemple

Vous trouverez ci-dessous un exemple d’implémentation de l’API Media Collection pour le tracking de plusieurs états du lecteur.

```
// statesUpdate (ex: mute and pictureInPicture are switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesStart": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: mute and pictureInPicture are switched off, fullScreen is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ],
    "statesStart": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: fullScreen is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

## Implémentation du SDK Media

Il n’existe aucune implémentation du SDK Media.
