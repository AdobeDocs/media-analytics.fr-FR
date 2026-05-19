---
title: Annonce publicitaire ignorée
description: Indique que la visionneuse a ignoré une publicité.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 15%

---


# Annonce publicitaire ignorée

L’événement d’omission de publicité indique que la visionneuse a ignoré une publicité avant sa fin. L’envoyer lorsque la visionneuse sélectionne le bouton Ignorer . Envoyez [publicité terminée](ad-complete.md) au lieu de lire la publicité jusqu’à la fin.

* **Conditions préalables** : [Début de session](../session/session-start.md), [Début de la coupure publicitaire](ad-break-start.md), [Début de la publicité](ad-start.md)
* **Mesure associée** : aucune

>[!IMPORTANT]
>
>Cet événement doit être entouré de `adBreakStart` et de `adBreakComplete` bookends, même lorsqu’une seule publicité est lue. Sans ces signets, les événements publicitaires sont ignorés et la durée de l’annonce publicitaire est comptabilisée comme la durée du contenu principal.

## SDK web

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec `eventType: "media.adSkip"` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adSkip",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 5
    }
  }
});
```

## SDK mobile

Appelez `trackEvent` avec le type d’événement `AdSkip`.

**iOS (Swift)**

```swift
tracker.trackEvent(event: MediaEvent.AdSkip, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.AdSkip, null, null)
```

## Roku (BrightScript)

Appelez `sendMediaEvent` avec `eventType: "media.adSkip"` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adSkip",
        "mediaCollection": {
            "playhead": 5
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [adSkip](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adskip) :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adSkip?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adSkip",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 5
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK Media

Appelez `trackEvent` avec le type d’événement `AdSkip` :

```javascript
tracker.trackEvent(ADB.Media.Event.AdSkip, null, null);
```

## API Media Collection

Envoyez une `adSkip` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 5, "ts": 1699523820000 },
  "eventType": "adSkip"
}
```
