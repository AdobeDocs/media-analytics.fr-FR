---
title: Position de l’annonce publicitaire dans la capsule
description: Définissez la position d’index de l’annonce publicitaire dans sa coupure publicitaire parente. La première publicité a un index de 0.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 12%

---


# Position de l’annonce publicitaire dans la capsule

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Position de l’annonce dans la capsule**. Voir [Annonce publicitaire dans la position de la capsule](/help/reporting/dimensions/ad-in-pod-position.md) pour la dimension de rapport correspondante.*

>[!ENDSHADEBOX]

La variable de position de l’annonce publicitaire dans la capsule correspond à la position indexée sur zéro de l’annonce publicitaire dans sa coupure publicitaire parente. La première publicité d&#39;une capsule a un index `0`, la seconde a un index `1`, etc. Utilisez la dimension pour comparer l’engagement et l’achèvement par position au sein d’une coupure publicitaire.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.ad.podPosition` |
| **champ de collection XDM** | [`mediaCollection.advertisingDetails.podPosition`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.ad.podPosition` |
| **Obligatoire** | Oui |
| **Envoyé avec** | [Début de la publicité](/help/implementation/events/ads/ad-start.md), fin de la publicité |

## SDK web

`podPosition` à l’intérieur des `mediaCollection.advertisingDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        podPosition: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez la position comme troisième argument à `createAdObject`.

**iOS (Swift)**

```swift
let adObject = Media.createAdObjectWith(name: "Ford F-150",
                                          id: "ad-2125",
                                    position: 0,
                                      length: 15)

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val adObject = Media.createAdObject("Ford F-150",
                                    "ad-2125",
                                    0L,
                                    15.0)

tracker.trackEvent(Media.Event.AdStart, adObject, null)
```

## Roku (BrightScript)

`podPosition` à l’intérieur des `mediaCollection.advertisingDetails` lors de l’appel de `sendMediaEvent` pour `media.adStart` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "podPosition": 0,
                "length": 15,
                "playerName": "Roku Player"
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) avec `podPosition` à l’intérieur du `mediaCollection.advertisingDetails` :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "advertisingDetails": {
          "name": "ad-2125",
          "length": 15,
          "playerName": "Freewheel",
          "podPosition": 0
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Transmettez la position comme troisième argument à `ADB.Media.createAdObject` :

```javascript
var adInfo = ADB.Media.createAdObject(
  "Ford F-150",
  "ad-2125",
  0,
  15
);

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## API Media Collection

Incluez `media.ad.podPosition` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.podPosition": 0
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.
