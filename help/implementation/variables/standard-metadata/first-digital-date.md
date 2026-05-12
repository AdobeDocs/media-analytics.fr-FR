---
title: Première date numérique
description: Définissez la date à laquelle le contenu sera diffusé pour la première fois sur une plateforme numérique. Adobe recommande le format AAAA-MM-JJ.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 13%

---


# Première date numérique

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Première date numérique**. Voir [Première date numérique](/help/reporting/dimensions/first-digital-date.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La première variable de date numérique correspond à la date à laquelle le contenu a été diffusé pour la première fois sur une plateforme numérique. Tout format de date est accepté, mais Adobe recommande de `YYYY-MM-DD` par souci de cohérence. Utilisez parallèlement à [Date de première diffusion](/help/implementation/variables/standard-metadata/first-air-date.md) pour comparer la date de publication numérique à celle de la diffusion originale.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.digitalDate` |
| **champ de collection XDM** | [`mediaCollection.sessionDetails.firstDigitalDate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obligatoire** | Non |
| **Envoyé avec** | Début et fin de la session |

## SDK web

`firstDigitalDate` à l’intérieur des `mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        firstDigitalDate: "2016-01-25"
      },
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez la première date numérique en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "2016-01-25"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "2016-01-25"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilisez `createMediaSession` pour définir des `firstDigitalDate` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "firstDigitalDate": "2016-01-25"
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `firstDigitalDate` à l’intérieur du `mediaCollection.sessionDetails` :

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
          "firstDigitalDate": "2016-01-25"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Transmettez la première date numérique dans l’objet `contextData` à l’aide de `ADB.Media.VideoMetadataKeys.FirstDigitalDate` :

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.FirstDigitalDate] = "2016-01-25";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Incluez `media.firstDigitalDate` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.firstDigitalDate": "2016-01-25"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.
