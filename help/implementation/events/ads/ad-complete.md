---
title: Publicité terminée
description: Signalez qu’une publicité individuelle a fini de fonctionner.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 15%

---


# Publicité terminée

L’événement de fin d’annonce publicitaire indique qu’une annonce publicitaire individuelle a terminé sa lecture. Envoyez-le une fois la lecture de l’annonce terminée. Si la visionneuse ignore l’annonce publicitaire, envoyez [Saut d’annonce publicitaire](ad-skip.md) à la place.

* **Conditions préalables** : [Début de session](../session/session-start.md), [Début de la coupure publicitaire](ad-break-start.md), [Début de la publicité](ad-start.md)
* **Mesure associée** : [publicités terminées](/help/reporting/metrics/ad-completes.md)

>[!IMPORTANT]
>
>Cet événement doit être entouré de `adBreakStart` et de `adBreakComplete` bookends, même lorsqu’une seule publicité est lue. Sans ces signets, les événements publicitaires sont ignorés et la durée de l’annonce publicitaire est comptabilisée comme la durée du contenu principal.

## SDK web

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec `eventType: "media.adComplete"` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 15
    }
  }
});
```

## SDK mobile

Appelez `trackEvent` avec le type d’événement `AdComplete`.

**iOS (Swift)**

```swift
tracker.trackEvent(event: MediaEvent.AdComplete, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.AdComplete, null, null)
```

## Roku (BrightScript)

Appelez `sendMediaEvent` avec `eventType: "media.adComplete"` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adComplete",
        "mediaCollection": {
            "playhead": 15
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [adComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adcomplete) :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 15
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK Media

Appelez `trackEvent` avec le type d’événement `AdComplete` :

```javascript
tracker.trackEvent(ADB.Media.Event.AdComplete, null, null);
```

## API Media Collection

Envoyez une `adComplete` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 15, "ts": 1699523820000 },
  "eventType": "adComplete"
}
```
