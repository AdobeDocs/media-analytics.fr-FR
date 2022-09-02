---
title: Mise à jour simultanée de plusieurs états du lecteur
description: Cette rubrique décrit la fonction de suivi de l’état du lecteur multiple.
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 7a28674024739593431a942d5e0a498294bbe793
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 10%

---

# Suivi de plusieurs états du lecteur

Il existe des situations où deux états du lecteur démarrent et se terminent en même temps ou lorsque la fin d’un état correspond également au début d’un autre état. Examinez l’exemple suivant :

![Plusieurs états du lecteur](assets/multiple-player-states.svg)

L’implémentation actuelle permet les deux scénarios :
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

Cependant, le client doit émettre de nombreuses `stateStart` et `stateEnd` pour signaler plusieurs changements d’état simultanés. Pour optimiser ce comportement commun, une nouvelle `statesUpdate` le type d’événement a été implémenté, qui met fin à une liste d’états et lance une liste de nouveaux états.

Utiliser la nouvelle `statesUpdate` , la liste d’événements ci-dessus devient :
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

Le nombre d’appels de mises à jour d’état a été réduit de 6 à 3 uniquement pour le même comportement. Le dernier événement aurait également pu être simple : `stateEnd(fullScreen)`.

## Mise en œuvre de l’API Media Collection

Exemples :

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
