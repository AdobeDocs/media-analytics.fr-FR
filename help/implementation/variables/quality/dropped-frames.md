---
title: Images perdues
description: Définissez le nombre d’images perdues en cours d’exécution sur l’objet QoE afin que le serveur principal puisse signaler la qualité de la perte d’images.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 5%

---


# Images perdues

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Images perdues**. Voir [Images perdues](/help/reporting/dimensions/dropped-frames.md) pour la dimension et la mesure de reporting correspondantes.*

>[!ENDSHADEBOX]

La variable images perdues correspond au nombre d’images perdues par le lecteur au cours de la session. Définissez-le sur l’objet QoE et mettez à jour la valeur à chaque fois que le lecteur signale de nouveaux abandons. Le serveur principal signale la dernière valeur à la fermeture de la session.

>[!NOTE]
>
>Transmettez toujours le **total cumulé** d’images perdues pour l’ensemble de la session jusqu’à ce point, et non un delta par intervalle. Si vous réinitialisez la valeur sur `0` entre les mises à jour, le serveur principal reçoit la `0` comme valeur finale et signale aucune image perdue pour la session, quelle que soit ce qui a été effectivement perdu précédemment.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.qoe.droppedFrameCount` |
| **champ de collection XDM** | [`xdm.mediaCollection.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.qoe.droppedFrameCount` |
| **Obligatoire** | Non |
| **Envoyé avec** | Événements de qualité ([changement de débit](/help/implementation/events/playback/bitrate-change.md), [début de la mémoire tampon](/help/implementation/events/playback/buffer-start.md), [erreur](/help/implementation/events/error.md)), fermeture de la session |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`droppedFrames` à l’intérieur des `xdm.mediaCollection.qoeDataDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 3
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

Transmettez les images perdues comme quatrième argument à `createQoEObject`. Mettez à jour le dispositif de suivi avant le déclenchement d’un événement de qualité.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 3)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

Transmettez les images perdues comme quatrième argument à `createQoEObject`. Mettez à jour le dispositif de suivi avant le déclenchement d’un événement de qualité.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      3L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku Edge]

`droppedFrames` à l’intérieur des `xdm.mediaCollection.qoeDataDetails` lors de l’appel de `sendMediaEvent` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 3
            },
            "playhead": 90
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) avec `droppedFrames` à l’intérieur du `xdm.mediaCollection.qoeDataDetails` :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "droppedFrames": 3
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Transmettez les images perdues comme quatrième argument à `ADB.Media.createQoEObject` :

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 3);
tracker.updateQoEObject(qoeObject);
```

>[!TAB  Chromecast ]

Transmettez le nombre cumulé d’images perdues comme quatrième argument pour `ADBMobile.media.createQoSObject` et mettre à jour le dispositif de suivi :

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate
  0,     // startupTime
  24,    // fps
  0      // droppedFrames (cumulative total)
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Roku 2.x]

Transmettez le nombre cumulé d’images perdues comme quatrième argument (`droppedFrames`) pour `adb_media_init_qosinfo` et mettre à jour le dispositif de suivi avec `mediaUpdateQoS` :

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(3200.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
```

>[!TAB  API Media Collection ]

Incluez `media.qoe.droppedFrames` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.droppedFrames": 3
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
