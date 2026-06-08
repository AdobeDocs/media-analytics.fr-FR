---
title: Heure de début de la coupure publicitaire
description: Définissez l’heure de début (décalage) de la coupure publicitaire à l’intérieur du contenu, en secondes.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 6%

---


# Heure de début de la coupure publicitaire

>[!BEGINSHADEBOX]

*Cette page couvre la collecte de données pour la variable **Heure de début de la coupure publicitaire**. Voir [Position de la capsule](/help/reporting/dimensions/pod-position.md) pour la dimension de rapport correspondante.*

>[!ENDSHADEBOX]

La variable de temps de début de coupure publicitaire correspond au décalage de la coupure publicitaire à l’intérieur du contenu, mesuré en secondes. Pour un pre-roll, la valeur est `0` ; pour un mid-roll, la valeur est la position de la tête de lecture à laquelle la coupure commence.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.ad.podSecond` |
| **champ de collection XDM** | [`xdm.mediaCollection.advertisingPodDetails.offset`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.ad.podSecond` |
| **Obligatoire** | Oui |
| **Envoyé avec** | [Début de la coupure publicitaire](/help/implementation/events/ads/ad-break-start.md), fin de la publicité |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`offset` à l’intérieur des `xdm.mediaCollection.advertisingPodDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

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

>[!TAB iOS]

Transmettez l’heure de début en secondes comme troisième argument à `createAdBreakObject`.

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "mid-roll-1",
                                              position: 2,
                                             startTime: 90)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

>[!TAB Android]

Transmettez l’heure de début en secondes comme troisième argument à `createAdBreakObject`.

```kotlin
val adBreakObject = Media.createAdBreakObject("mid-roll-1",
                                              2L,
                                              90.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

>[!TAB Roku Edge]

`offset` à l’intérieur des `xdm.mediaCollection.advertisingPodDetails` lors de l’appel de `sendMediaEvent` pour `media.adBreakStart` :

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

>[!TAB  API Media Edge ]

Appelez le point d’entrée [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) avec `offset` à l’intérieur du `xdm.mediaCollection.advertisingPodDetails` :

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

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Transmettez l’heure de début comme troisième argument à `ADB.Media.createAdBreakObject` :

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "mid-roll-1",
  2,
  90
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

>[!TAB  Chromecast ]

Transmettez l’heure de début en secondes comme troisième argument à `ADBMobile.media.createAdBreakObject` :

```javascript
var adBreakInfo = ADBMobile.media.createAdBreakObject(
  "mid-roll-1",
  2,
  90
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, adBreakInfo);
```

>[!TAB Roku 2.x]

Transmettez l’heure de début en secondes comme deuxième argument à `adb_media_init_adbreakinfo`. Notez l’ordre des paramètres Roku : `name, startTime, position`.

```brightscript
adb = ADBMobile()
adBreakInfo = adb_media_init_adbreakinfo("mid-roll-1", 90.0, 2)  ' name, startTime, position

adb.mediaTrackEvent(adb.MEDIA_AD_BREAK_START, adBreakInfo)
```

>[!TAB  API Media Collection ]

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

>[!ENDTABS]
