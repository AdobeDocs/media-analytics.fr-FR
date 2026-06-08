---
title: Nom de la coupure publicitaire
description: Définissez le nom convivial de la coupure publicitaire parent.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 6%

---


# Nom de la coupure publicitaire

>[!BEGINSHADEBOX]

*Cette page couvre la collecte de données pour la variable **Nom de la coupure publicitaire**. Voir [Nom de la capsule](/help/reporting/dimensions/pod-name.md) pour la dimension de rapport correspondante.*

>[!ENDSHADEBOX]

La variable de nom de coupure publicitaire est le nom convivial de la coupure publicitaire (par exemple, `"pre-roll"`, `"mid-roll-1"`, `"post-roll"`). La valeur est définie sur l’objet de coupure publicitaire et non sur des publicités individuelles.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.ad.podFriendlyName` |
| **champ de collection XDM** | [`xdm.mediaCollection.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.ad.podFriendlyName` |
| **Obligatoire** | Oui (Mobile SDK) ; Non (Edge, API Media Collection) |
| **Envoyé avec** | [Début de la coupure publicitaire](/help/implementation/events/ads/ad-break-start.md), fin de la publicité |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`friendlyName` à l’intérieur des `xdm.mediaCollection.advertisingPodDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) pour `media.adBreakStart` :

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

Transmettez le nom de la coupure publicitaire comme premier argument (`name`) à `createAdBreakObject`, puis suivez l’événement de démarrage de la coupure publicitaire avant l’événement de démarrage de la publicité.

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

>[!TAB Android]

Transmettez le nom de la coupure publicitaire comme premier argument (`name`) à `createAdBreakObject`, puis suivez l’événement de démarrage de la coupure publicitaire avant l’événement de démarrage de la publicité.

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1L,
                                              0.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

>[!TAB Roku Edge]

`friendlyName` à l’intérieur des `xdm.mediaCollection.advertisingPodDetails` lors de l’appel de `sendMediaEvent` pour `media.adBreakStart` :

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

Appelez le point d’entrée [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) avec `friendlyName` à l’intérieur du `xdm.mediaCollection.advertisingPodDetails` :

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

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Transmettez le nom de la coupure publicitaire comme premier argument à `ADB.Media.createAdBreakObject` :

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",
  1,
  0
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

>[!TAB  Chromecast ]

Transmettez le nom de la coupure publicitaire comme premier argument à `ADBMobile.media.createAdBreakObject` :

```javascript
var adBreakInfo = ADBMobile.media.createAdBreakObject(
  "pre-roll",
  1,
  0
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, adBreakInfo);
```

>[!TAB Roku 2.x]

Transmettez le nom de la coupure publicitaire comme premier argument à `adb_media_init_adbreakinfo`. Notez l’ordre des paramètres Roku : `name, startTime, position`.

```brightscript
adb = ADBMobile()
adBreakInfo = adb_media_init_adbreakinfo("pre-roll", 0.0, 1)  ' name, startTime, position

adb.mediaTrackEvent(adb.MEDIA_AD_BREAK_START, adBreakInfo)
```

>[!TAB  API Media Collection ]

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

>[!ENDTABS]
