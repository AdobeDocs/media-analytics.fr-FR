---
title: Mise en oeuvre et Rapports
description: Cette rubrique décrit la mise en oeuvre de la fonction de suivi de l’état du lecteur, y compris .
translation-type: tm+mt
source-git-commit: b0bfe74d1f6083e700dbf98f504a17518bd19ecb
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Mise en oeuvre et rapports

Au cours d’une session de lecture, chaque occurrence d’état (début à bout) doit faire l’objet d’un suivi individuel. Le SDK Media et l’API Media Collection fournissent de nouvelles méthodes de suivi pour cette fonctionnalité.

Le SDK multimédia comprend deux nouvelles méthodes pour le suivi d’état personnalisé :

`trackStateStart("state_name")`

`trackStateClose("state_name")`


L’API Media Collection inclut deux nouveaux événements dont le paramètre requis est &quot;media.stateName&quot; :

`stateStart` et `stateEnd`

## Mise en oeuvre du SDK Media

Débuts d’état du lecteur

```
// StateStart (ex: Mute is switched on)
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);
```

Fin de l&#39;état du lecteur

```
// StateEnd (ex: Mute is switched off)
tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```


## Implémentation de l’API de collecte de médias

Débuts d’état du lecteur

```
// StateStart (ex: Mute is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "stateStart",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

Fin de l&#39;état du lecteur

```
// StateEnd (ex: Mute is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events

{
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 600,
    "ts": 1569999730638
  }
}
```

## Mesures d’état

Les mesures fournies pour chaque état individuel sont calculées et transmises à Adobe Analytics en tant que paramètres de données contextuelles et stockées à des fins de rapports. Trois mesures sont disponibles pour chaque état :

* `a.media.states.(media.state.name).set = true` — Définit sur true si l’état a été défini au moins une fois par lecture spécifique d’un flux.
* `a.media.states.(media.state.name).count = 4` — Identifie le nombre d’occurrences d’un état au cours de chaque lecture individuelle d’un flux.
* `a.media.states.(media.state.name).time = 240` — Identifie la durée totale de l’état en secondes par lecture individuelle d’un flux

## Création de rapports

Toutes les mesures d’état peuvent être utilisées pour n’importe quel composant ou visualisation de rapports (segment, mesures calculées).
A déterminer - source/wiki pour obtenir des informations à jour - pour une capture d&#39;écran de AW

## Importation des mesures indiquées du lecteur vers Adobe Experience Platform

Les données stockées dans Analytics peuvent être utilisées à n’importe quel usage et les mesures d’état du lecteur peuvent être importées dans la plate-forme Adobe Experience à l’aide de XDM et utilisées avec Customer Journey Analytics. Les propriétés d’état standard possèdent des propriétés spécifiques tandis que les états personnalisés sont des propriétés disponibles via les événements personnalisés. Pour plus d&#39;informations, consultez la liste de propriétés des identités XDM à l&#39;adresse ?LINK TO METRIC LISTE ?.
