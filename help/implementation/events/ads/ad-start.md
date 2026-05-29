---
title: Démarrage de la publicité
description: Indique qu’une publicité individuelle a commencé à être lue.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 8%

---


# Démarrage de la publicité

L’événement de début de la publicité indique qu’une publicité individuelle a commencé à être lue. Cela doit se produire dans une paire [Début de la coupure publicitaire](ad-break-start.md) / [Fin de la coupure publicitaire](ad-break-complete.md).

* **Conditions préalables** : [début de session](../session/session-start.md), [début de la coupure publicitaire](ad-break-start.md)
* **Mesure associée** : [[!UICONTROL La publicité commence]](/help/reporting/metrics/ad-starts.md)

>[!IMPORTANT]
>
>Cet événement doit être entouré de `adBreakStart` et de `adBreakComplete` bookends, même lorsqu’une seule publicité est lue. Sans ces signets, les événements publicitaires sont ignorés et la durée de l’annonce publicitaire est comptabilisée comme la durée du contenu principal.

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec les `eventType: "media.adStart"` et les `advertisingDetails` requises :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        friendlyName: "Ford F-150",
        length: 15,
        playerName: "Freewheel",
        podPosition: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Transmettez le nom, l’ID, la position du pod et la longueur de l’annonce à `createAdObject`, puis appelez `trackEvent`.

```swift
let adObject = Media.createAdObjectWith(name: "Ford F-150",
                                          id: "ad-2125",
                                    position: 0,
                                      length: 15)

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: nil)
```

>[!TAB Android]

Transmettez le nom, l’ID, la position du pod et la longueur de l’annonce à `createAdObject`, puis appelez `trackEvent`.

```kotlin
val adObject = Media.createAdObject("Ford F-150",
                                    "ad-2125",
                                    0,
                                    15)

tracker.trackEvent(Media.Event.AdStart, adObject, null)
```

>[!TAB Roku]

Appelez `sendMediaEvent` avec les `eventType: "media.adStart"` et les `advertisingDetails` requises :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "friendlyName": "Ford F-150",
                "length": 15,
                "playerName": "Roku Player",
                "podPosition": 0
            },
            "playhead": 0
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) avec les `advertisingDetails` requises :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0,
        "advertisingDetails": {
          "name": "ad-2125",
          "length": 15,
          "playerName": "Freewheel",
          "podPosition": 0
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

Transmettez le nom, l’ID, la position et la longueur de l’annonce publicitaire à `ADB.Media.createAdObject` :

```javascript
var adInfo = ADB.Media.createAdObject(
  "Ford F-150",  // name (friendly name)
  "ad-2125",     // ad ID
  0,             // position in pod
  15             // length (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, null);
```

>[!TAB  Chromecast ]

Transmettez le nom, l’ID, la position et la longueur de l’annonce publicitaire à `ADBMobile.media.createAdObject` :

```javascript
var adInfo = ADBMobile.media.createAdObject(
  "Ford F-150",  // name (friendly name)
  "ad-2125",     // ad ID
  0,             // position in pod
  15             // length (seconds)
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB  API Media Collection ]

Envoyez une `adStart` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.id": "ad-2125",
    "media.ad.name": "Ford F-150",
    "media.ad.length": 15,
    "media.ad.podPosition": 0
  }
}
```

>[!ENDTABS]
