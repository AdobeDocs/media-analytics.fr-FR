---
title: Coupure publicitaire terminée
description: Signalez que toutes les publicités d’une coupure publicitaire sont terminées.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 9%

---


# Coupure publicitaire terminée

L’événement de fin de la coupure publicitaire indique que toutes les publicités d’une coupure publicitaire sont terminées (terminées ou ignorées). Il ferme la coupure publicitaire ouverte par [début de la coupure publicitaire](ad-break-start.md).

* **Conditions préalables** : [début de session](../session/session-start.md), [début de la coupure publicitaire](ad-break-start.md)
* **Mesure associée** : aucune

>[!IMPORTANT]
>
>Chaque `adBreakStart` doit avoir un `adBreakComplete` correspondant. Sans le signet de fermeture, les événements publicitaires sont ignorés et la durée de la publicité est attribuée au contenu principal.

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec `eventType: "media.adBreakComplete"` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Appelez `trackEvent` avec le type d’événement `AdBreakComplete`.

```swift
tracker.trackEvent(event: MediaEvent.AdBreakComplete, info: nil, metadata: nil)
```

>[!TAB Android]

Appelez `trackEvent` avec le type d’événement `AdBreakComplete`.

```kotlin
tracker.trackEvent(Media.Event.AdBreakComplete, null, null)
```

>[!TAB Roku Edge]

Appelez `sendMediaEvent` avec `eventType: "media.adBreakComplete"` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakComplete",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [adBreakComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakcomplete) :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adBreakComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0
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

Appelez `trackEvent` avec le type d’événement `AdBreakComplete` :

```javascript
tracker.trackEvent(ADB.Media.Event.AdBreakComplete, null, null);
```

>[!TAB  Chromecast ]

Appelez `trackEvent` avec le type d’événement `AdBreakComplete` :

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete);
```

>[!TAB Roku 2.x]

Appelez `mediaTrackEvent` avec le type d’événement `MEDIA_AD_BREAK_COMPLETE` :

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_AD_BREAK_COMPLETE)
```

>[!TAB  API Media Collection ]

Envoyez une `adBreakComplete` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakComplete"
}
```

>[!ENDTABS]
