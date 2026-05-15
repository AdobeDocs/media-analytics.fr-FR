---
title: Session terminée
description: Signale que la visionneuse a atteint la fin du contenu principal.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 16%

---


# Session terminée

L’événement de fin de session indique que la visionneuse a atteint la fin du contenu principal. La session n’est pas fermée immédiatement ; elle reste ouverte jusqu’à ce qu’elle expire naturellement. Si vous souhaitez fermer la session immédiatement, appelez plutôt [Fin de session](session-end.md).

* **Conditions préalables** : [début de session](session-start.md)
* **Mesure associée** : [Contenu terminé](/help/reporting/metrics/content-completes.md)

## SDK web

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec `eventType: "media.sessionComplete"` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 128
    }
  }
});
```

## SDK mobile

Appelez `trackComplete` lorsque le lecteur multimédia atteint la fin du contenu.

**iOS (Swift)**

```swift
tracker.trackComplete()
```

**Android (Kotlin)**

```kotlin
tracker.trackComplete()
```

## Roku (BrightScript)

Appelez `sendMediaEvent` avec `eventType: "media.sessionComplete"` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
            "playhead": 128
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [sessionComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessioncomplete) :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 128
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK Media

Appelez `trackComplete` lorsque le lecteur multimédia atteint la fin du contenu :

```javascript
tracker.trackComplete();
```

## API Media Collection

Envoyez une `sessionComplete` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 128, "ts": 1699523820000 },
  "eventType": "sessionComplete"
}
```
