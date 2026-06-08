---
title: Début de la mémoire tampon
description: Indique que le lecteur multimédia est entré en état de mise en mémoire tampon.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 7%

---


# Début de la mémoire tampon

L’événement de début de mémoire tampon signale que le lecteur multimédia est entré en état de mise en mémoire tampon.

* **Conditions préalables** : [début de session](../session/session-start.md)
* **Mesure associée** : [[!UICONTROL Événements de mise en mémoire tampon]](/help/reporting/metrics/buffer-events.md)

>[!NOTE]
>
>**API basées sur XDM (Web SDK, Roku, API Media Edge, API Media Collection) :** il n’existe aucun type d’événement de reprise de mémoire tampon ; l’extrémité de la mémoire tampon est déduite lorsque vous envoyez un événement [`play`](play.md) après `bufferStart`.
>
>**Mobile SDK :** appelez `trackEvent(BufferComplete)` lorsque le lecteur quitte la mise en mémoire tampon, puis appelez `trackPlay()` pour reprendre la lecture.

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec `eventType: "media.bufferStart"` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bufferStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

>[!TAB iOS]

Appelez `trackEvent` avec `BufferStart` lorsque le lecteur passe en état de mise en mémoire tampon et `BufferComplete` lorsqu’il se ferme.

```swift
// Buffer starts
tracker.trackEvent(event: MediaEvent.BufferStart, info: nil, metadata: nil)

// Buffer ends
tracker.trackEvent(event: MediaEvent.BufferComplete, info: nil, metadata: nil)
```

>[!TAB Android]

Appelez `trackEvent` avec `BufferStart` lorsque le lecteur passe en état de mise en mémoire tampon et `BufferComplete` lorsqu’il se ferme.

```kotlin
// Buffer starts
tracker.trackEvent(Media.Event.BufferStart, null, null)

// Buffer ends
tracker.trackEvent(Media.Event.BufferComplete, null, null)
```

>[!TAB Roku Edge]

Appelez `sendMediaEvent` avec `eventType: "media.bufferStart"` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bufferStart",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [bufferStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bufferstart/) :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/bufferStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.bufferStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45
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

Appelez `trackEvent` avec le type d’événement `BufferStart` :

```javascript
tracker.trackEvent(ADB.Media.Event.BufferStart, null, null);
```

>[!TAB  Chromecast ]

Appelez `trackEvent` avec `BufferStart` lorsque le lecteur passe en état de mise en mémoire tampon et `BufferComplete` lorsqu’il quitte :

```javascript
// Buffer starts
ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);

// Buffer ends
ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
```

>[!TAB Roku 2.x]

Appelez `mediaTrackEvent` avec `MEDIA_BUFFER_START` lorsque le lecteur passe en état de mise en mémoire tampon et `MEDIA_BUFFER_COMPLETE` lorsqu’il quitte :

```brightscript
adb = ADBMobile()

' Buffer starts
adb.mediaTrackEvent(adb.MEDIA_BUFFER_START)

' Buffer ends
adb.mediaTrackEvent(adb.MEDIA_BUFFER_COMPLETE)
```

>[!TAB  API Media Collection ]

Envoyez une `bufferStart` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "bufferStart"
}
```

>[!ENDTABS]
