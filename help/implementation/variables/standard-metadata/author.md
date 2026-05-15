---
title: Auteur
description: Définissez l’auteur du contenu. Principalement utilisé pour les livres audio.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 16%

---


# Auteur

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Auteur**. Voir [Auteur](/help/reporting/dimensions/author.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable auteur est l’auteur du contenu (par exemple, `"Eleanor Clementine"`). Principalement utilisé pour les livres audio, mais également acceptable pour les podcasts dont l’hôte ou le producteur est l’attribution pertinente.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.author` |
| **champ de collection XDM** | [`mediaCollection.sessionDetails.author`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.author` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## SDK web

`author` à l’intérieur des `mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        author: "Eleanor Clementine"
      },
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez l’auteur en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.AudioMetadataKeys.AUTHOR`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.AUTHOR] = "Eleanor Clementine"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.AUTHOR] = "Eleanor Clementine"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilisez `createMediaSession` pour définir des `author` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "author": "Eleanor Clementine"
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `author` à l’intérieur du `mediaCollection.sessionDetails` :

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
          "author": "Eleanor Clementine"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Transmettez l’auteur dans l’objet `contextData` à l’aide de `ADB.Media.AudioMetadataKeys.Author` :

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Author] = "Eleanor Clementine";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Incluez `media.author` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.author": "Eleanor Clementine"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.
