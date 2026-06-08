---
title: Nom du lecteur publicitaire
description: Définissez le nom du lecteur qui effectue le rendu des publicités. Le lecteur d’annonces publicitaires peut différer du lecteur de contenu principal.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 6%

---


# Nom du lecteur publicitaire

>[!BEGINSHADEBOX]

*Cette page couvre la collecte de données pour la variable **Nom du lecteur d’annonces**. Voir [Nom du lecteur d’annonces](/help/reporting/dimensions/ad-player-name.md) pour la dimension de compte rendu des performances correspondante.*

>[!ENDSHADEBOX]

La variable de nom du lecteur d’annonces identifie le lecteur qui a rendu chaque annonce publicitaire (par exemple, `"Freewheel"`, `"Google IMA"`). Le lecteur d’annonces publicitaires peut différer du lecteur de contenu principal lorsque des annonces sont regroupées par un service d’insertion d’annonces côté serveur. Utilisez cette variable pour comparer la qualité et l’achèvement des piles de diffusion d’annonces.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.ad.playerName` |
| **champ de collection XDM** | [`xdm.mediaCollection.advertisingDetails.playerName`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.ad.playerName` |
| **Obligatoire** | Oui |
| **Envoyé avec** | [Début de la publicité](/help/implementation/events/ads/ad-start.md), fin de la publicité |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`playerName` à l’intérieur des `xdm.mediaCollection.advertisingDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        playerName: "Freewheel"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Transmettez le nom du lecteur d’annonces comme clé `MediaConstants.AdMetadataKeys.AD_PLAYER` dans l’argument HashMap des métadonnées à `trackEvent(AdStart)`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

Transmettez le nom du lecteur d’annonces comme clé `MediaConstants.AdMetadataKeys.AD_PLAYER` dans l’argument HashMap des métadonnées à `trackEvent(AdStart)`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku Edge]

`playerName` à l’intérieur des `xdm.mediaCollection.advertisingDetails` lors de l’appel de `sendMediaEvent` pour `media.adStart` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "playerName": "Freewheel",
                "length": 15,
                "podPosition": 0
            },
            "playhead": 0
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) avec `playerName` à l’intérieur du `xdm.mediaCollection.advertisingDetails` :

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

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Transmettez le nom du lecteur d’annonces publicitaires dans l’objet `contextData` à l’aide de `ADB.Media.AdMetadataKeys.AdPlayer` :

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.AdPlayer] = "Freewheel";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB  Chromecast ]

Transmettez le nom du lecteur de publicités dans l’objet de métadonnées contextuelles lors du suivi de l’événement de début de la publicité :

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var metadata = { "a.media.ad.playerName": "Chromecast Player" };
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, metadata);
```

>[!TAB Roku 2.x]

Transmettez le nom du lecteur de publicités dans l’objet de données contextuelles lors du suivi de l’événement de début de la publicité :

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)

contextData = { "a.media.ad.playerName": "Roku Player" }
adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo, contextData)
```

>[!TAB  API Media Collection ]

Incluez `media.ad.playerName` dans l’objet `params` de votre `adStart` requête POST :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.playerName": "Freewheel"
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
