---
title: Nom de la publicité
description: Définissez le nom convivial de la publicité.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 8%

---


# Nom de la publicité

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Nom de l’annonce**. Voir [Nom de l’annonce](/help/reporting/dimensions/ad-name.md) pour la dimension de compte rendu des performances correspondante.*

>[!ENDSHADEBOX]

La variable de nom de l’annonce est le titre lisible par l’utilisateur de l’annonce (par exemple, `"Ford F-150"`). Définissez-le sur chaque événement `media.adStart`.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.ad.friendlyName` |
| **champ de collection XDM** | [`xdm.mediaCollection.advertisingDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.ad.friendlyName` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de la publicité](/help/implementation/events/ads/ad-start.md), fin de la publicité |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`friendlyName` à l’intérieur des `xdm.mediaCollection.advertisingDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        friendlyName: "Ford F-150"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Transmettez le nom de l’annonce publicitaire comme premier argument (`name`) à `createAdObject`. Le deuxième argument est l’ID de publicité.

```swift
let adObject = Media.createAdObjectWith(name: "Ford F-150",
                                          id: "ad-2125",
                                    position: 0,
                                      length: 15)

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: nil)
```

>[!TAB Android]

Transmettez le nom de l’annonce publicitaire comme premier argument (`name`) à `createAdObject`. Le deuxième argument est l’ID de publicité.

```kotlin
val adObject = Media.createAdObject("Ford F-150",
                                    "ad-2125",
                                    0L,
                                    15.0)

tracker.trackEvent(Media.Event.AdStart, adObject, null)
```

>[!TAB Roku]

`friendlyName` à l’intérieur des `xdm.mediaCollection.advertisingDetails` lors de l’appel de `sendMediaEvent` pour `media.adStart` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "friendlyName": "Ford F-150",
                "length": 15,
                "podPosition": 0,
                "playerName": "Roku Player"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) avec `friendlyName` à l’intérieur du `xdm.mediaCollection.advertisingDetails` :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "advertisingDetails": {
          "name": "ad-2125",
          "friendlyName": "Ford F-150",
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

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Transmettez le nom de l’annonce publicitaire comme premier argument à `ADB.Media.createAdObject` :

```javascript
var adInfo = ADB.Media.createAdObject(
  "Ford F-150",
  "ad-2125",
  0,
  15
);

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB  Chromecast ]

Transmettez le nom de l’annonce publicitaire comme premier argument à `ADBMobile.media.createAdObject` :

```javascript
var adInfo = ADBMobile.media.createAdObject(
  "Ford F-150",
  "ad-2125",
  1,
  30
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB  API Media Collection ]

Incluez `media.ad.name` dans l’objet `params` de votre `adStart` requête POST :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.name": "Ford F-150"
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
