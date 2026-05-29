---
title: Reprises du contenu
description: Marquez une session qui reprend une lecture précédemment interrompue afin que le serveur principal comptabilise un événement de reprise du contenu.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 7%

---


# Reprises du contenu

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Content resumes**. Voir [[!UICONTROL Reprises du contenu]](/help/reporting/metrics/content-resumes.md) pour la mesure de création de rapports correspondante.*

>[!ENDSHADEBOX]

La variable de reprise du contenu marque une session qui reprend une lecture précédemment interrompue. Définissez-le sur `media.sessionStart` afin que le serveur principal compte un événement [[!UICONTROL Content resumes]](/help/reporting/metrics/content-resumes.md) pour la session et l’exclut des nouveaux comptes de flux. Pour les implémentations directes d’API et d’API Edge, le client est chargé de détecter les sessions reprises (par exemple, après une mise en mémoire tampon, une pause ou un blocage dépassant 30 minutes) et de définir cet indicateur en conséquence.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.resume` |
| **champ de collection XDM** | [`xdm.mediaCollection.sessionDetails.hasResume`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | S.O. |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de la session](/help/implementation/events/session/session-start.md) |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

Définissez `hasResume` sur `true` dans `xdm.mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) pour la reprise de session :

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

>[!TAB iOS]

Transmettez l’indicateur de reprise dans le cadre du lot de configuration facultatif de l’objet média sur `trackSessionStart`. Utilisez la clé `MediaConstants.MediaObjectKey.RESUMED` .

```swift
var mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)
mediaObject?[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

Transmettez l’indicateur de reprise dans le cadre du lot de configuration facultatif de l’objet média sur `trackSessionStart`. Utilisez la clé `MediaConstants.MediaObjectKey.RESUMED` .

```kotlin
val mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)
mediaInfo[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku]

Définissez `hasResume` sur `true` dans `xdm.mediaCollection.sessionDetails` lors de l’appel de `createMediaSession` pour la reprise de session :

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

>[!TAB  API Media Edge ]

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `hasResume` défini sur `true` dans `xdm.mediaCollection.sessionDetails` :

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

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

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

>[!TAB  Chromecast ]

Définissez `MediaResumed` sur l’objet d’informations sur le média avant d’appeler `trackSessionStart` :

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
mediaInfo[ADBMobile.media.MediaObjectKey.MediaResumed] = true;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB  API Media Collection ]

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

>[!ENDTABS]
