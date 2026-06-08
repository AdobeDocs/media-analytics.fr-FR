---
title: Heure de début
description: Définissez l’heure de démarrage du lecteur, en millisecondes, de sorte que le serveur principal puisse signaler la qualité du délai de première image.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 5%

---


# Heure de début

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Time to start**. Voir [[!UICONTROL Heure de début]](/help/reporting/dimensions/time-to-start.md) pour la dimension et la mesure de reporting correspondantes.*

>[!ENDSHADEBOX]

La variable time to start correspond au temps écoulé, en millisecondes, entre le lancement de la lecture par le lecteur et le premier rendu d’image. Définissez-le sur l’objet QoE avant que l’événement de début de session ne se déclenche. Adobe stocke et signale la valeur en secondes ; transmettez les millisecondes et Adobe convertit au moment de l’ingestion.

>[!IMPORTANT]
>
>Une fois que le lecteur commence à effectuer le rendu des images de contenu, arrêtez la mise à jour `timeToStart`. Cette valeur peut augmenter au cours de la phase de mise en mémoire tampon ou de chargement initiale, mais doit être considérée comme fixe dès le début de la lecture. Si vous continuez à la mettre à jour après le rendu de la première image, une mesure [[!UICONTROL Heure de début]](/help/reporting/metrics/time-to-start.md) exagérée ou incorrecte est générée.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.qoe.timeToStart` |
| **champ de collection XDM** | [`xdm.mediaCollection.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.qoe.timeToStart` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

Définissez `timeToStart` à l’intérieur du `xdm.mediaCollection.qoeDataDetails` sur `media.sessionStart` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

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
      qoeDataDetails: {
        timeToStart: 30000
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Transmettez l’heure de démarrage comme deuxième argument (`startupTime`) à `createQoEObject`.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 30000,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

Transmettez l’heure de démarrage comme deuxième argument (`startupTime`) à `createQoEObject`.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      30000.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku Edge]

Définissez `timeToStart` à l’intérieur du `xdm.mediaCollection.qoeDataDetails` sur `media.sessionStart` lors de l’appel de `createMediaSession` :

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
            "qoeDataDetails": {
                "timeToStart": 30000
            },
            "playhead": 0
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `timeToStart` à l’intérieur du `xdm.mediaCollection.qoeDataDetails` :

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
        "qoeDataDetails": {
          "timeToStart": 30000
        },
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

Transmettez l’heure de début comme deuxième argument à `ADB.Media.createQoEObject` :

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 30000, 24, 0);
tracker.updateQoEObject(qoeObject);
```

>[!TAB  Chromecast ]

Transmettez l’heure de démarrage en millisecondes comme deuxième argument (`startupTime`) pour `ADBMobile.media.createQoSObject` et mettre à jour le dispositif de suivi :

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,   // bitrate
  0,      // startupTime (ms)
  24,     // fps
  0       // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Roku 2.x]

Transmettez l’heure de démarrage comme deuxième argument (`startupTime`) pour `adb_media_init_qosinfo` et mettre à jour le suivi avec `mediaUpdateQoS` :

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(3200.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
```

>[!TAB  API Media Collection ]

Incluez `media.qoe.timeToStart` dans l’objet `params` sur `sessionStart` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.qoe.timeToStart": 30000
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
