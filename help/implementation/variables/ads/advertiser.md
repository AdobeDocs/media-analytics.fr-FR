---
title: Annonceur
description: Définissez la société ou la marque présentée dans chaque publicité.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 16%

---


# Annonceur

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Advertiser**. Voir [Annonceur](/help/reporting/dimensions/advertiser.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable de l’annonceur correspond à la société ou à la marque présentée dans la publicité (par exemple, `"Ford"` ou `"Coca-Cola"`). Utilisez la variable pour ventiler l’engagement et l’achèvement par l’annonceur.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.ad.advertiser` |
| **champ de collection XDM** | [`mediaCollection.advertisingDetails.advertiser`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.ad.advertiser` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de la publicité](/help/implementation/events/ads/ad-start.md), fin de la publicité |

## SDK web

`advertiser` à l’intérieur des `mediaCollection.advertisingDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        advertiser: "Ford"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez l’annonceur en tant que clé de métadonnées dans l’argument HashMap à `trackEvent(AdStart)`. Utilisez `MediaConstants.AdMetadataKeys.ADVERTISER`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.ADVERTISER] = "Ford"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.ADVERTISER] = "Ford"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

`advertiser` à l’intérieur des `mediaCollection.advertisingDetails` lors de l’appel de `sendMediaEvent` pour `media.adStart` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "advertiser": "Ford"
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) avec `advertiser` à l’intérieur du `mediaCollection.advertisingDetails` :

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
          "advertiser": "Ford"
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Transmettez l’annonceur dans l’objet `contextData` à l’aide de `ADB.Media.AdMetadataKeys.Advertiser` :

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.Advertiser] = "Ford";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## API Media Collection

Incluez `media.ad.advertiser` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.advertiser": "Ford"
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.
