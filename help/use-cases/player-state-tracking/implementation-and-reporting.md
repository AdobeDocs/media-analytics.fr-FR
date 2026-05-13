---
title: Mise en œuvre et création de rapports
description: Découvrez comment mettre en œuvre la fonction de suivi de lʼétat du lecteur, y compris.
exl-id: 19a97c9b-14d1-4f11-bb0a-3a1ad6f949da
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/NzekVHZYctiEjAWDpRhIdiw74amAX3wTX-z2nZDgvIw
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: f1f1a2d4-0976-4881-b091-c2bb8de7ffacid: f836f655-eebe-4b76-82bc-697955ec1ce3
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 308
ht-degree: 76%

---

# Mise en œuvre et création de rapports

Au cours d’une session de lecture, chaque occurrence d’état (du début à la fin de la lecture) doit faire l’objet d’un suivi individuel. Media SDK et l’API Media Collection fournissent des méthodes de suivi pour cette fonctionnalité.

Media SDK comprend deux méthodes de suivi d’état personnalisé :

`trackStateStart("state_name")`

`trackStateClose("state_name")`


L’API Media Collection comprend deux événements qui ont `media.stateName` comme paramètre obligatoire :

`stateStart` et `stateEnd`

## Mise en œuvre du SDK Media

Début de l’état du lecteur

```
// StateStart (ex: Mute is switched on)
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);
```

Fin de l’état du lecteur

```
// StateEnd (ex: Mute is switched off)
tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```


## Mise en œuvre de l’API Media Collection

Début de l’état du lecteur

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

Fin de l’état du lecteur

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

Les mesures fournies pour chaque état individuel sont calculées et transmises à Adobe Analytics en tant que paramètres de données contextuelles et sont stockées à des fins de création de rapports. Trois mesures sont disponibles pour chaque état :

* `a.media.states.[state.name].set = true` — Défini sur « true » si l’état a été défini au moins une fois au cours de chaque lecture spécifique d’un flux.
* `a.media.states.[state.name].count = 4` — Identifie le nombre d’occurrences d’un état au cours de chaque lecture individuelle d’un flux.
* `a.media.states.[state.name].time = 240` — Identifie la durée totale de l’état en secondes au cours de chaque lecture individuelle d’un flux.

## Création de rapports

Toutes les mesures d’état du lecteur peuvent être utilisées pour toutes les visualisations de rapports disponibles dans Analysis Workspace ou un composant (segment, mesures calculées) une fois qu’une suite de rapports est activée pour le suivi de l’état du lecteur. Ces mesures peuvent être activées à partir d’Admin Console pour chaque rapport individuel à l’aide de la Configuration du reporting multimédia (Modifier les paramètres > Gestion des médias > Reporting multimédia).

![](assets/report-setup.png)

Dans Analysis Workspace, toutes les nouvelles propriétés se trouvent dans le panneau des mesures. Par exemple, vous pouvez rechercher par `full screen` pour consulter les données portant sur le passage en plein écran dans le panneau des mesures.

![](assets/full-screen-report.png)

## Importation des mesures d’état du lecteur vers Adobe Experience Platform

Les données stockées dans Analytics peuvent être utilisées à n’importe quelle fin, et les mesures d’état du lecteur peuvent être importées dans Adobe Experience Platform à l’aide de XDM et utilisées avec Customer Journey Analytics. Les propriétés d’état standards possèdent des propriétés spécifiques, tandis que les états personnalisés sont des propriétés disponibles en utilisant des événements personnalisés.
