---
title: Ping
description: Envoyez une pulsation pour maintenir la session multimédia active et suivre la progression de la lecture à intervalles réguliers.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 1%

---


# Ping

L’événement ping est une pulsation qui maintient la session active et suit la progression de la lecture. Envoyez-le sur un minuteur pendant la lecture. Sur les SDK mobiles, les pings sont envoyés automatiquement. Sur toutes les autres plateformes, ils doivent être envoyés manuellement selon l’intervalle spécifié.

* **Contenu principal** : première commande ping 10 secondes après le début de la lecture, puis toutes les 10 secondes par la suite
* **Contenu publicitaire** : toutes les secondes pendant le suivi des publicités

N’incluez pas d’objet `params` dans le corps de la requête ping.

* **Conditions préalables** : [début de session](../session/session-start.md)
* **Mesure associée** : aucune

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

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

>[!TAB iOS]

Mobile SDK envoie automatiquement des événements ping. Aucun appel explicite n’est requis.

>[!TAB Android]

Mobile SDK envoie automatiquement des événements ping. Aucun appel explicite n’est requis.

>[!TAB Roku Edge]

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

>[!TAB  API Media Edge ]

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

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Media SDK envoie automatiquement des événements ping. Aucun appel explicite n’est requis.

>[!TAB  Chromecast ]

Le SDK Chromecast envoie automatiquement des événements ping. Aucun appel explicite n’est requis.

>[!TAB Roku 2.x]

Media SDK envoie automatiquement des événements ping tant que vous appelez `processMediaMessages` dans votre boucle d’événement. Mettez à jour le curseur de lecture pour que chaque ping indique la position actuelle :

```brightscript
ADBMobile().mediaUpdatePlayhead(10)
```

>[!TAB  API Media Collection ]

Envoyez une `ping` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) sur un minuteur. N’incluez pas d’objet `params` :

```json
{
  "playerTime": { "playhead": 10, "ts": 1699523820000 },
  "eventType": "ping"
}
```

>[!ENDTABS]
