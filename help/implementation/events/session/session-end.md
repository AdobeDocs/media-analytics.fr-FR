---
title: Fin de la session
description: Fermez immédiatement une session multimédia lorsque la personne qui la visionne abandonne le contenu.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 14%

---


# Fin de la session

L’événement de fin de session ferme immédiatement une session de suivi multimédia. Utilisez-le lorsque la visionneuse abandonne le contenu avant d’atteindre la fin et que vous ne souhaitez pas que les événements suivants soient suivis au cours de la même session. Si la visionneuse termine le contenu, appelez plutôt [Fin de la session](session-complete.md).

Sans fin de session explicite, une session se ferme automatiquement après 10 minutes d’absence d’événement ou 30 minutes d’absence de mouvement du curseur de lecture.

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
