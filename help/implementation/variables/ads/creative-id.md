---
title: ID d’élément créatif
description: Définissez l’identifiant de contenu créatif pour chaque publicité.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 18%

---


# ID d’élément créatif

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Creative ID**. Voir [Creative ID](/help/reporting/dimensions/creative-id.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable Creative ID identifie le contenu publicitaire spécifique. Toute valeur de chaîne (généralement un identifiant de contenu publicitaire de votre plateforme de serveur de publicités) est acceptable.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.ad.creative` |
| **champ de collection XDM** | [`mediaCollection.advertisingDetails.creativeID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Obligatoire** | Non |
| **Envoyé avec** | Démarrage et fermeture de la publicité |

## SDK web

`creativeID` à l’intérieur des `mediaCollection.advertisingDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

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

## SDK mobile

Transmettez l’ID de contenu créatif en tant que clé de métadonnées dans l’argument HashMap à `trackEvent(AdStart)`. Utilisez `MediaConstants.AdMetadataKeys.CREATIVE_ID`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CREATIVE_ID] = "creative-987"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CREATIVE_ID] = "creative-987"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

`creativeID` à l’intérieur des `mediaCollection.advertisingDetails` lors de l’appel de `sendMediaEvent` pour `media.adStart` :

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

## API Media Edge

Appelez le point d’entrée [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) avec `creativeID` à l’intérieur du `mediaCollection.advertisingDetails` :

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

## SDK Media

Transmettez l’ID de contenu créatif dans l’objet `contextData` à l’aide de `ADB.Media.AdMetadataKeys.CreativeId` :

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CreativeId] = "creative-987";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## API Media Collection

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
