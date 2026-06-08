---
title: Annonce publicitaire ignorée
description: Indique que la visionneuse a ignoré une publicité.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 8%

---


# Annonce publicitaire ignorée

L’événement d’omission de publicité indique que la visionneuse a ignoré une publicité avant sa fin. L’envoyer lorsque la visionneuse sélectionne le bouton Ignorer . Envoyez [publicité terminée](ad-complete.md) au lieu de lire la publicité jusqu’à la fin.

* **Conditions préalables** : [Début de session](../session/session-start.md), [Début de la coupure publicitaire](ad-break-start.md), [Début de la publicité](ad-start.md)
* **Mesure associée** : aucune

>[!IMPORTANT]
>
>Cet événement doit être entouré de `adBreakStart` et de `adBreakComplete` bookends, même lorsqu’une seule publicité est lue. Sans ces signets, les événements publicitaires sont ignorés et la durée de l’annonce publicitaire est comptabilisée comme la durée du contenu principal.

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec `eventType: "media.adSkip"` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adSkip",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 5
    }
  }
});
```

>[!TAB iOS]

Appelez `trackEvent` avec le type d’événement `AdSkip`.

```swift
tracker.trackEvent(event: MediaEvent.AdSkip, info: nil, metadata: nil)
```

>[!TAB Android]

Appelez `trackEvent` avec le type d’événement `AdSkip`.

```kotlin
tracker.trackEvent(Media.Event.AdSkip, null, null)
```

>[!TAB Roku Edge]

Appelez `sendMediaEvent` avec `eventType: "media.adSkip"` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adSkip",
        "mediaCollection": {
            "playhead": 5
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [adSkip](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adskip) :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adSkip?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adSkip",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 5
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

Appelez `trackEvent` avec le type d’événement `AdSkip` :

```javascript
tracker.trackEvent(ADB.Media.Event.AdSkip, null, null);
```

>[!TAB  Chromecast ]

Appelez `trackEvent` avec le type d’événement `AdSkip` :

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdSkip);
```

>[!TAB Roku 2.x]

Appelez `mediaTrackEvent` avec le type d’événement `MEDIA_AD_SKIP` :

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_AD_SKIP)
```

>[!TAB  API Media Collection ]

Envoyez une `adSkip` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 5, "ts": 1699523820000 },
  "eventType": "adSkip"
}
```

>[!ENDTABS]
