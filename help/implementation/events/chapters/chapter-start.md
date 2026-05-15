---
title: Début du chapitre
description: Signalez le début d’un segment de chapitre dans le contenu.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 17%

---


# Début du chapitre

L’événement de début de chapitre signale le début d’un chapitre dans le contenu. Le suivi des chapitres est facultatif et n’est pas obligatoire pour le suivi des médias principaux.

* **Conditions préalables** : [début de session](../session/session-start.md)
* **Mesure associée** : [Le chapitre commence](/help/reporting/metrics/chapter-starts.md)

## SDK web

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec les `eventType: "media.chapterStart"` et les `chapterDetails` requises :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterStart",
    mediaCollection: {
      chapterDetails: {
        friendlyName: "Pilot Episode - Opening",
        index: 1,
        offset: 0,
        length: 240
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez le nom, la position, la longueur et l’heure de début du chapitre à `createChapterObject`, puis appelez `trackEvent`.

**iOS (Swift)**

```swift
let chapterObject = Media.createChapterObjectWith(name: "Pilot Episode - Opening",
                                              position: 1,
                                                length: 240,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val chapterObject = Media.createChapterObject("Pilot Episode - Opening",
                                              1,
                                              240,
                                              0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

## Roku (BrightScript)

Appelez `sendMediaEvent` avec les `eventType: "media.chapterStart"` et les `chapterDetails` requises :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
            "chapterDetails": {
                "friendlyName": "Pilot Episode - Opening",
                "index": 1,
                "offset": 0,
                "length": 240
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) avec les `chapterDetails` requises :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0,
        "chapterDetails": {
          "index": 1,
          "length": 240,
          "offset": 0
        }
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK Media

Transmettez le nom, la position, la longueur et l’heure de début du chapitre à `ADB.Media.createChapterObject` :

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length (seconds)
  0                           // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, null);
```

## API Media Collection

Envoyez une `chapterStart` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Pilot Episode - Opening",
    "media.chapter.index": 1,
    "media.chapter.offset": 0,
    "media.chapter.length": 240
  }
}
```
