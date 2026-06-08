---
title: Début de la coupure publicitaire
description: Signalez le début d’une coupure publicitaire (une séquence d’une ou de plusieurs publicités).
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 6%

---


# Début de la coupure publicitaire

L’événement de début de coupure publicitaire signale le début d’une coupure publicitaire. Une coupure publicitaire est une séquence d’une ou de plusieurs publicités. Chaque événement `adStart`, `adComplete` et `adSkip` doit se produire entre une paire `adBreakStart` et `adBreakComplete`, même lorsqu’une seule publicité est lue.

* **Conditions préalables** : [début de session](../session/session-start.md)
* **Mesure associée** : aucune

>[!IMPORTANT]
>
>Les événements d’annonce (`adStart`, `adComplete`, `adSkip`) sont ignorés sans `adBreakStart` et `adBreakComplete` les signets. Sans elles, la durée de l’annonce publicitaire est attribuée à la durée du contenu principal, ce qui affecte les données de rapports agrégées.

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

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

>[!TAB iOS]

Transmettez le nom, la position et l’heure de début de la coupure publicitaire à `createAdBreakObject`, puis appelez `trackEvent`.

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

>[!TAB Android]

Transmettez le nom, la position et l’heure de début de la coupure publicitaire à `createAdBreakObject`, puis appelez `trackEvent`.

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1,
                                              0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

>[!TAB Roku Edge]

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

>[!TAB  API Media Edge ]

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

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Transmettez le nom, la position et l’heure de début de la coupure publicitaire à `ADB.Media.createAdBreakObject` :

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",  // name
  1,           // position
  0            // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

>[!TAB  Chromecast ]

Transmettez le nom, la position et l’heure de début de la coupure publicitaire à `ADBMobile.media.createAdBreakObject` :

```javascript
var adBreakInfo = ADBMobile.media.createAdBreakObject(
  "pre-roll",  // name
  1,           // position
  0            // start time (seconds)
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, adBreakInfo);
```

>[!TAB Roku 2.x]

Créez un objet de coupure publicitaire avec `adb_media_init_adbreakinfo`, puis suivez l’événement. Notez l’ordre des paramètres Roku : `name, startTime, position`.

```brightscript
adb = ADBMobile()
adBreakInfo = adb_media_init_adbreakinfo("pre-roll", 0.0, 1)  ' name, startTime, position

adb.mediaTrackEvent(adb.MEDIA_AD_BREAK_START, adBreakInfo)
```

>[!TAB  API Media Collection ]

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

>[!ENDTABS]
