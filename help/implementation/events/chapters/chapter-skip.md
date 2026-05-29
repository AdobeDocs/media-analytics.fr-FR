---
title: Saut de chapitre
description: Signale que la visionneuse a ignoré un chapitre.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 10%

---


# Saut de chapitre

L’événement d’omission de chapitre indique que la visionneuse a ignoré un chapitre avant de terminer. Envoyez-le lorsque la visionneuse navigue au-delà de la limite du chapitre sans l’observer jusqu’à la fin. Envoyez le [chapitre terminé](chapter-complete.md) si le chapitre est lu jusqu’à sa fin.

* **Conditions préalables** : [début de session](../session/session-start.md), [début de chapitre](chapter-start.md)
* **Mesure associée** : aucune

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

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

>[!TAB iOS]

Appelez `trackEvent` avec le type d’événement `ChapterSkip`.

```swift
tracker.trackEvent(event: MediaEvent.ChapterSkip, info: nil, metadata: nil)
```

>[!TAB Android]

Appelez `trackEvent` avec le type d’événement `ChapterSkip`.

```kotlin
tracker.trackEvent(Media.Event.ChapterSkip, null, null)
```

>[!TAB Roku]

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

>[!TAB  API Media Edge ]

Appelez le point d’entrée [&#x200B; chapterSkip &#x200B;](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterskip) :

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

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Appelez `trackEvent` avec le type d’événement `ChapterSkip` :

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterSkip, null, null);
```

>[!TAB  Chromecast ]

Appelez `trackEvent` avec le type d’événement `ChapterSkip` :

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterSkip);
```

>[!TAB  API Media Collection ]

Envoyez une `chapterSkip` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "chapterSkip"
}
```

>[!ENDTABS]
