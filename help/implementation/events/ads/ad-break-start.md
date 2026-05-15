---
title: Début de la coupure publicitaire
description: Signalez le début d’une coupure publicitaire (une séquence d’une ou de plusieurs publicités).
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 13%

---


# Début de la coupure publicitaire

L’événement de début de coupure publicitaire signale le début d’une coupure publicitaire. Une coupure publicitaire est une séquence d’une ou de plusieurs publicités. Chaque événement `adStart`, `adComplete` et `adSkip` doit se produire entre une paire `adBreakStart` et `adBreakComplete`, même lorsqu’une seule publicité est lue.

* **Conditions préalables** : [début de session](../session/session-start.md)
* **Mesure associée** : aucune

>[!IMPORTANT]
>
>Les événements d’annonce (`adStart`, `adComplete`, `adSkip`) sont ignorés sans `adBreakStart` et `adBreakComplete` les signets. Sans elles, la durée de l’annonce publicitaire est attribuée à la durée du contenu principal, ce qui affecte les données de rapports agrégées.

## SDK web

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec les `eventType: "media.adBreakStart"` et les `advertisingPodDetails` requises :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "pre-roll",
        index: 1,
        offset: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez le nom, la position et l’heure de début de la coupure publicitaire à `createAdBreakObject`, puis appelez `trackEvent`.

**iOS (Swift)**

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1,
                                              0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

## Roku (BrightScript)

Appelez `sendMediaEvent` avec les `eventType: "media.adBreakStart"` et les `advertisingPodDetails` requises :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "pre-roll",
                "index": 1,
                "offset": 0
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) avec les `advertisingPodDetails` requises :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adBreakStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0,
        "advertisingPodDetails": {
          "index": 0,
          "offset": 0
        }
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK Media

Transmettez le nom, la position et l’heure de début de la coupure publicitaire à `ADB.Media.createAdBreakObject` :

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",  // name
  1,           // position
  0            // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

## API Media Collection

Envoyez une `adBreakStart` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podFriendlyName": "pre-roll",
    "media.ad.podIndex": 1,
    "media.ad.podSecond": 0
  }
}
```
