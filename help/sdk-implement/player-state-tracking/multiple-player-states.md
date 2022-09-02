---
title: Mise à jour simultanée de plusieurs états du lecteur
description: Cette rubrique décrit la fonction de suivi de l’état du lecteur multiple.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: fdbb777547181422b81ff6f7874bec3d317d02e9
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 9%

---

# Suivi de plusieurs états du lecteur

Parfois, deux états du lecteur démarrent et se terminent en même temps ou la fin d’un état correspond également au début d’un autre état, comme illustré dans l’image suivante :

![Plusieurs états du lecteur](assets/multiple-player-states.svg)

L’implémentation actuelle permet les deux scénarios :
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

Toutefois, cela nécessite que vous émettiez plusieurs `stateStart` et `stateEnd` pour signaler plusieurs changements d’état simultanés. Pour optimiser ce comportement commun, une nouvelle `statesUpdate` le type d’événement a été implémenté, qui met fin à une liste d’états et lance une liste de nouveaux états.

Utiliser la nouvelle `statesUpdate` , la liste d’événements ci-dessus devient :
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

Le nombre d’appels de mises à jour d’état a été réduit de six à trois pour le même comportement. Le dernier événement aurait également pu être simple : `stateEnd(fullScreen)`.

## Mise en œuvre de l’API Media Collection {#mpst-api}

Vous pouvez utiliser l’API Media Collection pour mettre en oeuvre le suivi de l’état de plusieurs lecteurs.

### Exemple

Vous trouverez ci-dessous un exemple de mise en oeuvre de l’API Media Collection pour le suivi de l’état de plusieurs lecteurs.

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

## Mise en œuvre du SDK Media

Il n’existe aucune mise en oeuvre du SDK Media.
