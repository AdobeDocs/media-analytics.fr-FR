---
title: Fin de la session
description: Fermez immédiatement une session multimédia lorsque la personne qui la visionne abandonne le contenu.
feature: Streaming Media
role: Developer
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 8%

---


# Fin de la session

L’événement de fin de session ferme immédiatement et de manière irréversible une session de suivi multimédia. La session se termine par une fermeture définitive : une fois envoyée, la session se termine et aucun autre événement ne peut être suivi en dessous. N’utilisez la fin de session que lorsque vous êtes certain qu’aucun événement supplémentaire ne se produira, par exemple lorsque le lecteur est détruit ou que la page est déchargée. Dans la plupart des cas, il est plus sûr de laisser la session expirer naturellement plutôt que de risquer d’interrompre les événements qui pourraient encore arriver. Si la visionneuse termine le contenu, appelez plutôt [Fin de la session](session-complete.md).

Sans fin de session explicite, une session se ferme automatiquement après 10 minutes d’absence d’événement ou 30 minutes d’absence de mouvement du curseur de lecture.

>[!NOTE]
>
>Vous pouvez appeler en toute sécurité la fin de session plusieurs fois pour la même session. Le serveur principal ferme la session sur le premier événement et supprime silencieusement tous les événements suivants pour cet ID de session, y compris une seconde fin de session. Vous n’avez pas besoin de vous prémunir contre les appels en double dans des conditions de concurrence, telles qu’un délai d’expiration de 30 minutes expirant au moment où la visionneuse ferme le lecteur.

* **Conditions préalables** : [début de session](session-start.md)
* **Mesure associée** : aucune

## SDK web

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec `eventType: "media.sessionEnd"` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionEnd",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## SDK mobile

Appelez `trackSessionEnd` lorsque la visionneuse ferme le lecteur ou quitte le lecteur.

**iOS (Swift)**

```swift
tracker.trackSessionEnd()
```

**Android (Kotlin)**

```kotlin
tracker.trackSessionEnd()
```

## Roku (BrightScript)

Appelez `sendMediaEvent` avec `eventType: "media.sessionEnd"` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionEnd",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [sessionEnd](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionend) :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionEnd?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionEnd",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK Media

Appelez `trackSessionEnd` lorsque la visionneuse ferme le lecteur ou quitte le lecteur :

```javascript
tracker.trackSessionEnd();
```

## API Media Collection

Envoyez une `sessionEnd` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "sessionEnd"
}
```
