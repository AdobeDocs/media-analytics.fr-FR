---
title: Mise en oeuvre et Rapports
description: Cette rubrique décrit la mise en oeuvre de la fonction de suivi de l’état du lecteur, y compris .
translation-type: tm+mt
source-git-commit: 614780a121eac6d5f822d439365fa59f85959ce2
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Mise en oeuvre et rapports

Au cours d’une session de lecture, chaque occurrence d’état (début à bout) doit faire l’objet d’un suivi individuel. Le SDK Media et l’API Media Collection fournissent de nouvelles méthodes de suivi pour cette fonctionnalité.

Le SDK multimédia comprend deux nouvelles méthodes pour le suivi d’état personnalisé :

`trackStateStart("state_name")`

`trackStateClose("state_name")`


L’API de collecte de médias comprend deux nouveaux événements qui comportent `media.stateName` le paramètre requis :

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

* `a.media.states.[state.name].set = true` — Définit sur true si l’état a été défini au moins une fois par lecture spécifique d’un flux.
* `a.media.states.[state.name].count = 4` — Identifie le nombre d’occurrences d’un état au cours de chaque lecture individuelle d’un flux.
* `a.media.states.[state.name].time = 240` — Identifie la durée totale de l’état en secondes par lecture individuelle d’un flux

## Création de rapports

Toutes les mesures d’état du lecteur peuvent être utilisées pour toute visualisation de rapports disponible dans Analyse Workspace ou un composant (segment, mesures calculées) une fois qu’une suite de rapports est activée pour le suivi de l’état du lecteur. Les nouvelles mesures peuvent être activées à partir de la Console d’administration pour chaque rapport individuel à l’aide de la configuration du Rapports multimédia (Modifier les paramètres > Gestion des médias > Rapports multimédia).

![](assets/report-setup.png)

Dans Analytics Workspace, toutes les nouvelles propriétés se trouvent dans le panneau des mesures. Par exemple, vous pouvez effectuer des recherches en fonction `full screen` de la vue des données en plein écran dans le panneau des mesures.

![](assets/full-screen-report.png)

## Importation de mesures avec mention du lecteur vers la plateforme d’expérience Adobe

Les données stockées dans Analytics peuvent être utilisées à n’importe quel usage et les mesures d’état du lecteur peuvent être importées dans la plateforme Adobe Experience à l’aide de XDM et utilisées avec Customer Journey Analytics. Les propriétés d’état standard possèdent des propriétés spécifiques tandis que les états personnalisés sont des propriétés disponibles via les événements personnalisés. Pour plus d&#39;informations, consultez la liste de propriétés des identités XDM à l&#39;adresse ?LINK TO METRIC LISTE ?.
