---
title: Heure de début de la coupure publicitaire
description: Définissez l’heure de début (décalage) de la coupure publicitaire à l’intérieur du contenu, en secondes.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 12%

---


# Heure de début de la coupure publicitaire

>[!BEGINSHADEBOX]

*Cette page couvre la collecte de données pour la variable **Heure de début de la coupure publicitaire**. Voir [Position de la capsule](/help/reporting/dimensions/pod-position.md) pour la dimension de rapport correspondante.*

>[!ENDSHADEBOX]

La variable de temps de début de coupure publicitaire correspond au décalage de la coupure publicitaire à l’intérieur du contenu, mesuré en secondes. Pour un pre-roll, la valeur est `0` ; pour un mid-roll, la valeur est la position de la tête de lecture à laquelle la coupure commence.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.ad.podSecond` |
| **champ de collection XDM** | [`mediaCollection.advertisingPodDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Obligatoire** | Oui |
| **Envoyé avec** | Démarrage et fermeture de la publicité |

## SDK web

`offset` à l’intérieur des `mediaCollection.advertisingPodDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "mid-roll-1",
        index: 2,
        offset: 90
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## SDK mobile

Transmettez l’heure de début en secondes comme troisième argument à `createAdBreakObject`.

**iOS (Swift)**

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "mid-roll-1",
                                              position: 2,
                                             startTime: 90)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val adBreakObject = Media.createAdBreakObject("mid-roll-1",
                                              2L,
                                              90.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

## Roku (BrightScript)

`offset` à l’intérieur des `mediaCollection.advertisingPodDetails` lors de l’appel de `sendMediaEvent` pour `media.adBreakStart` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "mid-roll-1",
                "index": 2,
                "offset": 90
            },
            "playhead": 90
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) avec `offset` à l’intérieur du `mediaCollection.advertisingPodDetails` :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "index": 2,
          "offset": 90
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## SDK Media

Transmettez l’heure de début comme troisième argument à `ADB.Media.createAdBreakObject` :

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "mid-roll-1",
  2,
  90
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

## API Media Collection

Incluez `media.ad.podSecond` dans l’objet `params` de votre `adBreakStart` requête POST :

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podSecond": 90
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.
