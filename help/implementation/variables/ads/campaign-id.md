---
title: ID de campagne
description: Définissez l’identifiant de campagne pour chaque publicité afin que l’engagement puisse être agrégé par campagne.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 15%

---


# ID de campagne

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Identifiant de campagne**. Voir [Identifiant de campagne](/help/reporting/dimensions/campaign-id.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable d’identifiant de campagne identifie la campagne publicitaire à laquelle le contenu publicitaire appartient. Toute valeur de chaîne (généralement un identifiant de campagne de votre plateforme de serveur de publicités) est acceptable. Utilisez la variable pour cumuler l’engagement de plusieurs créatifs qui partagent une campagne.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.ad.campaign` |
| **champ de collection XDM** | [`mediaCollection.advertisingDetails.campaignID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.ad.campaign` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de la publicité](/help/implementation/events/ads/ad-start.md), fin de la publicité |

## SDK web

`campaignID` à l’intérieur des `mediaCollection.advertisingDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        campaignID: "fall-2024"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez l’identifiant de campagne en tant que clé de métadonnées dans l’argument HashMap à `trackEvent(AdStart)`. Utilisez `MediaConstants.AdMetadataKeys.CAMPAIGN_ID`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

`campaignID` à l’intérieur des `mediaCollection.advertisingDetails` lors de l’appel de `sendMediaEvent` pour `media.adStart` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "campaignID": "fall-2024"
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) avec `campaignID` à l’intérieur du `mediaCollection.advertisingDetails` :

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
          "campaignID": "fall-2024"
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Transmettez l’identifiant de campagne dans l’objet `contextData` à l’aide de `ADB.Media.AdMetadataKeys.CampaignId` :

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CampaignId] = "fall-2024";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## API Media Collection

Incluez `media.ad.campaignId` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.campaignId": "fall-2024"
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.
