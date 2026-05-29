---
title: Publicité terminée
description: Signalez qu’une publicité individuelle a fini de fonctionner.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 9%

---


# Publicité terminée

L’événement de fin d’annonce publicitaire indique qu’une annonce publicitaire individuelle a terminé sa lecture. Envoyez-le une fois la lecture de l’annonce terminée. Si la visionneuse ignore l’annonce publicitaire, envoyez [Saut d’annonce publicitaire](ad-skip.md) à la place.

* **Conditions préalables** : [Début de session](../session/session-start.md), [Début de la coupure publicitaire](ad-break-start.md), [Début de la publicité](ad-start.md)
* **Mesure associée** : [[!UICONTROL publicités terminées]](/help/reporting/metrics/ad-completes.md)

>[!IMPORTANT]
>
>Cet événement doit être entouré de `adBreakStart` et de `adBreakComplete` bookends, même lorsqu’une seule publicité est lue. Sans ces signets, les événements publicitaires sont ignorés et la durée de l’annonce publicitaire est comptabilisée comme la durée du contenu principal.

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec `eventType: "media.adComplete"` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 15
    }
  }
});
```

>[!TAB iOS]

Appelez `trackEvent` avec le type d’événement `AdComplete`.

```swift
tracker.trackEvent(event: MediaEvent.AdComplete, info: nil, metadata: nil)
```

>[!TAB Android]

Appelez `trackEvent` avec le type d’événement `AdComplete`.

```kotlin
tracker.trackEvent(Media.Event.AdComplete, null, null)
```

>[!TAB Roku]

Appelez `sendMediaEvent` avec `eventType: "media.adComplete"` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adComplete",
        "mediaCollection": {
            "playhead": 15
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [adComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adcomplete) :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 15
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

Appelez `trackEvent` avec le type d’événement `AdComplete` :

```javascript
tracker.trackEvent(ADB.Media.Event.AdComplete, null, null);
```

>[!TAB  Chromecast ]

Appelez `trackEvent` avec le type d’événement `AdComplete` :

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete);
```

>[!TAB  API Media Collection ]

Envoyez une `adComplete` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 15, "ts": 1699523820000 },
  "eventType": "adComplete"
}
```

>[!ENDTABS]
