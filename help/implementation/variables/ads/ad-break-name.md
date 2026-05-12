---
title: Nom de la coupure publicitaire
description: Définissez le nom convivial de la coupure publicitaire parent.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 12%

---


# Nom de la coupure publicitaire

>[!BEGINSHADEBOX]

*Cette page couvre la collecte de données pour la variable **Nom de la coupure publicitaire**. Voir [Nom de la capsule](/help/reporting/dimensions/pod-name.md) pour la dimension de rapport correspondante.*

>[!ENDSHADEBOX]

La variable de nom de coupure publicitaire est le nom convivial de la coupure publicitaire (par exemple, `"pre-roll"`, `"mid-roll-1"`, `"post-roll"`). La valeur est définie sur l’objet de coupure publicitaire et non sur des publicités individuelles.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.ad.podFriendlyName` |
| **champ de collection XDM** | [`mediaCollection.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Obligatoire** | Oui (Mobile SDK) ; Non (Edge, API Media Collection) |
| **Envoyé avec** | Démarrage et fermeture de la publicité |

## SDK web

`friendlyName` à l’intérieur des `mediaCollection.advertisingPodDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) pour `media.adBreakStart` :

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

Transmettez le nom de la coupure publicitaire comme premier argument (`name`) à `createAdBreakObject`, puis suivez l’événement de démarrage de la coupure publicitaire avant l’événement de démarrage de la publicité.

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
                                              1L,
                                              0.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

## Roku (BrightScript)

`friendlyName` à l’intérieur des `mediaCollection.advertisingPodDetails` lors de l’appel de `sendMediaEvent` pour `media.adBreakStart` :

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

Appelez le point d’entrée [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) avec `friendlyName` à l’intérieur du `mediaCollection.advertisingPodDetails` :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "friendlyName": "pre-roll",
          "index": 1,
          "offset": 0
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Transmettez le nom de la coupure publicitaire comme premier argument à `ADB.Media.createAdBreakObject` :

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",
  1,
  0
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

## API Media Collection

Incluez `media.ad.podFriendlyName` dans l’objet `params` de votre `adBreakStart` requête POST :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podFriendlyName": "pre-roll"
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.
