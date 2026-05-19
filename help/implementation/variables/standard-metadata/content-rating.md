---
title: Classement du contenu
description: Définissez l’évaluation du contenu telle que définie par les directives parentales TV ou votre système d’évaluation régional.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 14%

---


# Classement du contenu

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Évaluation du contenu**. Voir [Évaluation du contenu](/help/reporting/dimensions/content-rating.md) pour la dimension de compte rendu des performances correspondante.*

>[!ENDSHADEBOX]

La variable d’évaluation du contenu est l’évaluation de l’audience telle que définie par les directives parentales de TV (`"TVY"`, `"TVG"`, `"TVPG"`, `"TVMA"`) ou tout système d’évaluation régional que vous utilisez. Utilisez-le pour comparer l’engagement et la charge publicitaire entre les niveaux d’évaluation.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.rating` |
| **champ de collection XDM** | [`mediaCollection.sessionDetails.rating`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.rating` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## SDK web

`rating` à l’intérieur des `mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        rating: "TVPG"
      },
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez l’évaluation en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.RATING`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.RATING] = "TVPG"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.RATING] = "TVPG"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilisez `createMediaSession` pour définir des `rating` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "rating": "TVPG"
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `rating` à l’intérieur du `mediaCollection.sessionDetails` :

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
          "rating": "TVPG"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Transmettez l’évaluation dans l’objet `contextData` à l’aide de `ADB.Media.VideoMetadataKeys.Rating` :

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Rating] = "TVPG";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Incluez `media.rating` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.rating": "TVPG"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.
