---
title: Reprises du contenu
description: Marquez une session qui reprend une lecture précédemment interrompue afin que le serveur principal comptabilise un événement de reprise du contenu.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 10%

---


# Reprises du contenu

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Content resumes**. Voir [Reprises du contenu](/help/reporting/metrics/content-resumes.md) pour la mesure de création de rapports correspondante.*

>[!ENDSHADEBOX]

La variable de reprise du contenu marque une session qui reprend une lecture précédemment interrompue. Définissez-le sur `media.sessionStart` afin que le serveur principal compte un événement de reprise du contenu pour la session et l’exclut des nouveaux comptes de flux. Pour les implémentations directes d’API et d’API Edge, le client est chargé de détecter les sessions reprises (par exemple, après une mise en mémoire tampon, une pause ou un blocage dépassant 30 minutes) et de définir cet indicateur en conséquence.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.resume` |
| **champ de collection XDM** | [`mediaCollection.sessionDetails.hasResume`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obligatoire** | Non |
| **Envoyé avec** | Début de la session |

## SDK web

Définissez `hasResume` sur `true` dans `mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) pour la reprise de session :

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
        streamType: "video",
        hasResume: true
      },
      playhead: 60
    }
  }
});
```

## SDK mobile

Transmettez l’indicateur de reprise dans le cadre du lot de configuration facultatif de l’objet média sur `trackSessionStart`. Utilisez la clé `MediaConstants.MediaObjectKey.RESUMED` .

**iOS (Swift)**

```swift
var mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)
mediaObject?[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)
mediaInfo[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(mediaInfo, null)
```

## Roku (BrightScript)

Définissez `hasResume` sur `true` dans `mediaCollection.sessionDetails` lors de l’appel de `createMediaSession` pour la reprise de session :

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
                "streamType": "video",
                "hasResume": true
            },
            "playhead": 60
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `hasResume` défini sur `true` dans `mediaCollection.sessionDetails` :

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
          "hasResume": true
        },
        "playhead": 60
      }
    }
  }]
}
```

## SDK Media

Définissez la clé `RESUMED` sur l’objet d’informations sur le média avant d’appeler `trackSessionStart` :

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);
mediaInfo[ADB.Media.MediaObjectKey.Resumed] = true;

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Incluez `media.resume` dans l’objet `params` de votre `sessionStart` requête POST :

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.resume": true
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.
