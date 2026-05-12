---
title: Identifiant de référencement
description: Définissez l’identifiant d’emplacement pour chaque publicité afin d’activer les répartitions par emplacement publicitaire.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 17%

---


# Identifiant de référencement

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **ID d’emplacement**. Voir [ID d’emplacement](/help/reporting/dimensions/placement-id.md) pour la dimension de rapport correspondante.*

>[!ENDSHADEBOX]

La variable d’identifiant d’emplacement identifie l’emplacement publicitaire (généralement un emplacement ou une zone défini dans votre plateforme de serveur de publicités).

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.ad.placement` |
| **champ de collection XDM** | [`mediaCollection.advertisingDetails.placementID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Obligatoire** | Non |
| **Envoyé avec** | Démarrage et fermeture de la publicité |

## SDK web

`placementID` à l’intérieur des `mediaCollection.advertisingDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        placementID: "placement-12"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez l’identifiant d’emplacement en tant que clé de métadonnées dans l’argument HashMap à `trackEvent(AdStart)`. Utilisez `MediaConstants.AdMetadataKeys.PLACEMENT_ID`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.PLACEMENT_ID] = "placement-12"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.PLACEMENT_ID] = "placement-12"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

`placementID` à l’intérieur des `mediaCollection.advertisingDetails` lors de l’appel de `sendMediaEvent` pour `media.adStart` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "placementID": "placement-12"
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) avec `placementID` à l’intérieur du `mediaCollection.advertisingDetails` :

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
          "placementID": "placement-12"
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Transmettez l’identifiant d’emplacement dans l’objet `contextData` à l’aide de `ADB.Media.AdMetadataKeys.PlacementId` :

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.PlacementId] = "placement-12";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## API Media Collection

Incluez `media.ad.placementId` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.placementId": "placement-12"
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.
