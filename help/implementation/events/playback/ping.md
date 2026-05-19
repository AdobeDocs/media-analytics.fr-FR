---
title: Ping
description: Envoyez une pulsation pour maintenir la session multimédia active et suivre la progression de la lecture à intervalles réguliers.
feature: Streaming Media
role: Developer
source-git-commit: 6534e4c76dcb4113bbbb99aed2a0e350f9256b15
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 5%

---


# Ping

L’événement ping est une pulsation qui maintient la session active et suit la progression de la lecture. Envoyez-le sur un minuteur pendant la lecture. Sur les SDK mobiles, les pings sont envoyés automatiquement. Sur toutes les autres plateformes, ils doivent être envoyés manuellement selon l’intervalle spécifié.

* **Contenu principal** : première commande ping 10 secondes après le début de la lecture, puis toutes les 10 secondes par la suite
* **Contenu publicitaire** : toutes les secondes pendant le suivi des publicités

N’incluez pas d’objet `params` dans le corps de la requête ping.

* **Conditions préalables** : [début de session](../session/session-start.md)
* **Mesure associée** : aucune

## SDK web

Planifiez un appel `sendEvent` récurrent avec `eventType: "media.ping"`. Mettez à jour la `playhead` vers la position de lecture actuelle à chaque appel :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.ping",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 10
    }
  }
});
```

## SDK mobile

Mobile SDK envoie automatiquement des événements ping. Aucun appel explicite n’est requis.

## Roku (BrightScript)

Planifiez un appel `sendMediaEvent` récurrent avec `eventType: "media.ping"`. Mettez à jour la `playhead` vers la position de lecture actuelle à chaque appel :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.ping",
        "mediaCollection": {
            "playhead": 10
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [ping](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ping/) sur un minuteur. Adobe recommande d’exécuter le premier ping 10 secondes après le début de la lecture principale, toutes les 10 secondes par la suite et toutes les secondes pendant le suivi publicitaire :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/ping?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.ping",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 10
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK Media

Media SDK envoie automatiquement des événements ping. Aucun appel explicite n’est requis.

## API Media Collection

Envoyez une `ping` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) sur un minuteur. N’incluez pas d’objet `params` :

```json
{
  "playerTime": { "playhead": 10, "ts": 1699523820000 },
  "eventType": "ping"
}
```
