---
title: Saut de chapitre
description: Signale que la visionneuse a ignoré un chapitre.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 18%

---


# Saut de chapitre

L’événement d’omission de chapitre indique que la visionneuse a ignoré un chapitre avant de terminer. Envoyez-le lorsque la visionneuse navigue au-delà de la limite du chapitre sans l’observer jusqu’à la fin. Envoyez le [chapitre terminé](chapter-complete.md) si le chapitre est lu jusqu’à sa fin.

* **Conditions préalables** : [début de session](../session/session-start.md), [début de chapitre](chapter-start.md)
* **Mesure associée** : aucune

## SDK web

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec `eventType: "media.chapterSkip"` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterSkip",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

## SDK mobile

Appelez `trackEvent` avec le type d’événement `ChapterSkip`.

**iOS (Swift)**

```swift
tracker.trackEvent(event: MediaEvent.ChapterSkip, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.ChapterSkip, null, null)
```

## Roku (BrightScript)

Appelez `sendMediaEvent` avec `eventType: "media.chapterSkip"` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterSkip",
        "mediaCollection": {
            "playhead": 60
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [ chapterSkip ](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterskip) :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterSkip?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterSkip",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 60
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK Media

Appelez `trackEvent` avec le type d’événement `ChapterSkip` :

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterSkip, null, null);
```

## API Media Collection

Envoyez une `chapterSkip` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "chapterSkip"
}
```
