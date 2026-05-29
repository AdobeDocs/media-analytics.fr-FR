---
title: ID d’élément créatif
description: Définissez l’identifiant de contenu créatif pour chaque publicité.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 11%

---


# ID d’élément créatif

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Creative ID**. Voir [Creative ID](/help/reporting/dimensions/creative-id.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable Creative ID identifie le contenu publicitaire spécifique. Toute valeur de chaîne (généralement un identifiant de contenu publicitaire de votre plateforme de serveur de publicités) est acceptable.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.ad.creative` |
| **champ de collection XDM** | [`xdm.mediaCollection.advertisingDetails.creativeID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.ad.creative` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de la publicité](/help/implementation/events/ads/ad-start.md), fin de la publicité |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`creativeID` à l’intérieur des `xdm.mediaCollection.advertisingDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        creativeID: "creative-987"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Transmettez l’ID de contenu créatif en tant que clé de métadonnées dans l’argument HashMap à `trackEvent(AdStart)`. Utilisez `MediaConstants.AdMetadataKeys.CREATIVE_ID`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CREATIVE_ID] = "creative-987"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

Transmettez l’ID de contenu créatif en tant que clé de métadonnées dans l’argument HashMap à `trackEvent(AdStart)`. Utilisez `MediaConstants.AdMetadataKeys.CREATIVE_ID`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CREATIVE_ID] = "creative-987"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku]

`creativeID` à l’intérieur des `xdm.mediaCollection.advertisingDetails` lors de l’appel de `sendMediaEvent` pour `media.adStart` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "creativeID": "creative-987"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) avec `creativeID` à l’intérieur du `xdm.mediaCollection.advertisingDetails` :

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
          "podPosition": 0,
          "creativeID": "creative-987"
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

Transmettez l’ID de contenu créatif dans l’objet `contextData` à l’aide de `ADB.Media.AdMetadataKeys.CreativeId` :

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CreativeId] = "creative-987";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB  Chromecast ]

Définissez l’ID de contenu créatif à l’aide de `ADBMobile.media.AdMetadataKeys.CREATIVE_ID` dans l’objet de métadonnées publicitaire standard :

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var standardAdMetadata = {};
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_ID] = "creative-987";
adInfo[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardAdMetadata;
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB  API Media Collection ]

Incluez `media.ad.creativeId` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.creativeId": "creative-987"
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
