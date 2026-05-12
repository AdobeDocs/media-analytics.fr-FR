---
title: Type de contenu
description: Définissez le type de contenu pour identifier le format du flux (VOD, Live, Linéaire, podcast, chanson, etc.).
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 10%

---


# Type de contenu

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Type de contenu**. Voir [Type de contenu](/help/reporting/dimensions/content-type.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable de type de contenu identifie le format du flux (par exemple, VOD, Live ou Linéaire pour la vidéo, ou podcast ou livre audio pour l’audio). Elle est requise pour toutes les implémentations de streaming multimédia et doit être définie au début de la session. Les valeurs définies par Adobe renseignent les segments et les rapports de type de contenu intégrés. Les chaînes personnalisées sont également acceptées, mais ne correspondent pas aux segments intégrés. Si elle n’est pas définie, la valeur par défaut est `missing_content_type`.

Valeurs recommandées :

* **Vidéo :** `vod`, `live`, `linear`, `ugc`, `dvod`
* **Audio :** `song`, `podcast`, `audiobook`, `radio`

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.contentType` |
| **champ de collection XDM** | [`mediaCollection.sessionDetails.contentType`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obligatoire** | Oui |
| **Envoyé avec** | Début et fin de la session |

## SDK web

`contentType` à l’intérieur des `mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video"
      },
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez la constante de type de contenu comme argument de `streamType` à `createMediaObject`. Utilisez des valeurs `MediaConstants.StreamType.*` telles que `VOD`, `LIVE`, `LINEAR`, `AOD`, `PODCAST`. Remarque : dans Mobile SDK, l’argument `streamType` contrôle le type de contenu. La variable Type de flux (audio ou vidéo) est l’argument `mediaType` distinct.

**iOS (Swift)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

## Roku (BrightScript)

`contentType` à l’intérieur des `mediaCollection.sessionDetails` lors de l’appel de `createMediaSession` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `contentType` à l’intérieur du `mediaCollection.sessionDetails` :

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
          "channel": "Sports"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Transmettez une constante `ADB.Media.StreamType.*` comme quatrième argument à `ADB.Media.createMediaObject` :

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADB.Media.StreamType.VOD, // Content type — VOD, LIVE, LINEAR, etc.
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Incluez `media.contentType` dans l’objet `params` de votre `sessionStart` requête POST :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.contentType": "vod"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.
