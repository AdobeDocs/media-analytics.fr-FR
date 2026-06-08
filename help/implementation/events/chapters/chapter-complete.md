---
title: Chapitre terminé
description: Signalez qu’un segment de chapitre a terminé sa lecture.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 10%

---


# Chapitre terminé

L’événement de fin de chapitre indique qu’un chapitre a terminé sa lecture. Envoyez-le lorsque la visionneuse atteint la fin d’un chapitre. Si la visionneuse ignore le chapitre, envoyez plutôt [Ignorer le chapitre](chapter-skip.md).

* **Conditions préalables** : [début de session](../session/session-start.md), [début de chapitre](chapter-start.md)
* **Mesure associée** : [[!UICONTROL le chapitre est terminé]](/help/reporting/metrics/chapter-completes.md)

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

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

>[!TAB iOS]

Appelez `trackEvent` avec le type d’événement `ChapterComplete`.

```swift
tracker.trackEvent(event: MediaEvent.ChapterComplete, info: nil, metadata: nil)
```

>[!TAB Android]

Appelez `trackEvent` avec le type d’événement `ChapterComplete`.

```kotlin
tracker.trackEvent(Media.Event.ChapterComplete, null, null)
```

>[!TAB Roku Edge]

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

>[!TAB  API Media Edge ]

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

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Appelez `trackEvent` avec le type d’événement `ChapterComplete` :

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterComplete, null, null);
```

>[!TAB  Chromecast ]

Appelez `trackEvent` avec le type d’événement `ChapterComplete` :

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterComplete);
```

>[!TAB Roku 2.x]

Appelez `mediaTrackEvent` avec le type d’événement `MEDIA_CHAPTER_COMPLETE` :

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_CHAPTER_COMPLETE)
```

>[!TAB  API Media Collection ]

Envoyez une `chapterComplete` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterComplete"
}
```

>[!ENDTABS]
