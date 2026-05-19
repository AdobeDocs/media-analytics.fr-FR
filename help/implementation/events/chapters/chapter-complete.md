---
title: Chapitre terminé
description: Signalez qu’un segment de chapitre a terminé sa lecture.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 20%

---


# Chapitre terminé

L’événement de fin de chapitre indique qu’un chapitre a terminé sa lecture. Envoyez-le lorsque la visionneuse atteint la fin d’un chapitre. Si la visionneuse ignore le chapitre, envoyez plutôt [Ignorer le chapitre](chapter-skip.md).

* **Conditions préalables** : [début de session](../session/session-start.md), [début de chapitre](chapter-start.md)
* **Mesure associée** : [le chapitre est terminé](/help/reporting/metrics/chapter-completes.md)

## SDK web

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec `eventType: "media.chapterComplete"` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 240
    }
  }
});
```

## SDK mobile

Appelez `trackEvent` avec le type d’événement `ChapterComplete`.

**iOS (Swift)**

```swift
tracker.trackEvent(event: MediaEvent.ChapterComplete, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.ChapterComplete, null, null)
```

## Roku (BrightScript)

Appelez `sendMediaEvent` avec `eventType: "media.chapterComplete"` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterComplete",
        "mediaCollection": {
            "playhead": 240
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [chapterComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chaptercomplete) :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 240
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK Media

Appelez `trackEvent` avec le type d’événement `ChapterComplete` :

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterComplete, null, null);
```

## API Media Collection

Envoyez une `chapterComplete` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterComplete"
}
```
