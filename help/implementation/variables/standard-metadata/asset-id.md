---
title: ID de ressource
description: Définissez l’ID de ressource, un identifiant de secteur stable pour la ressource multimédia, tel qu’un EIDR ou un ID TMS/Gracenote.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 13%

---


# ID de ressource

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **ID de ressource**. Voir [ID de ressource](/help/reporting/dimensions/asset-id.md) pour la dimension de rapport correspondante.*

>[!ENDSHADEBOX]

La variable d’ID de ressource est l’identifiant unique de la ressource de média sous-jacente (par exemple, un ID d’épisode, un ID d’animation ou un ID d’événement en direct). Généralement fourni par des autorités de métadonnées telles que EIDR, TMS/Gracenote ou Rovi, mais les identifiants propriétaires ou internes sont également acceptés. Utilisez-le lorsque vous devez comparer l’engagement sur les plateformes de distribution qui peuvent attribuer différents ID de contenu à la même ressource sous-jacente.

>[!NOTE]
>
>Le champ de collection XDM utilise des `ID` majuscules : `assetID`.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.asset` |
| **champ de collection XDM** | [`mediaCollection.sessionDetails.assetID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obligatoire** | Non |
| **Envoyé avec** | Début et fin de la session |

## SDK web

`assetID` à l’intérieur des `mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        assetID: "89745363"
      },
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez l’ID de ressource en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.ASSET_ID`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilisez `createMediaSession` pour définir des `assetID` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "assetID": "89745363"
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `assetID` à l’intérieur du `mediaCollection.sessionDetails` :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 128,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "assetID": "89745363"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Transmettez l’ID de ressource dans l’objet `contextData` à l’aide de `ADB.Media.VideoMetadataKeys.AssetId` :

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.AssetId] = "89745363";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Incluez `media.assetId` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.assetId": "89745363"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.
