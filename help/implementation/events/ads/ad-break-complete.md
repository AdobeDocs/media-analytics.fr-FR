---
title: Coupure publicitaire terminée
description: Signalez que toutes les publicités d’une coupure publicitaire sont terminées.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 16%

---


# Coupure publicitaire terminée

L’événement de fin de la coupure publicitaire indique que toutes les publicités d’une coupure publicitaire sont terminées (terminées ou ignorées). Il ferme la coupure publicitaire ouverte par [début de la coupure publicitaire](ad-break-start.md).

* **Conditions préalables** : [début de session](../session/session-start.md), [début de la coupure publicitaire](ad-break-start.md)
* **Mesure associée** : aucune

>[!IMPORTANT]
>
>Chaque `adBreakStart` doit avoir un `adBreakComplete` correspondant. Sans le signet de fermeture, les événements publicitaires sont ignorés et la durée de la publicité est attribuée au contenu principal.

## SDK web

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec `eventType: "media.adBreakComplete"` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK mobile

Appelez `trackEvent` avec le type d’événement `AdBreakComplete`.

**iOS (Swift)**

```swift
tracker.trackEvent(event: MediaEvent.AdBreakComplete, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.AdBreakComplete, null, null)
```

## Roku (BrightScript)

Appelez `sendMediaEvent` avec `eventType: "media.adBreakComplete"` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakComplete",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [adBreakComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakcomplete) :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adBreakComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK Media

Appelez `trackEvent` avec le type d’événement `AdBreakComplete` :

```javascript
tracker.trackEvent(ADB.Media.Event.AdBreakComplete, null, null);
```

## API Media Collection

Envoyez une `adBreakComplete` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakComplete"
}
```
