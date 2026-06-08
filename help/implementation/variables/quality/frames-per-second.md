---
title: Images par seconde
description: Définissez la fréquence d’image actuelle sur l’objet QoE afin que le serveur principal dispose d’un contexte de fréquence d’image pour les rapports de qualité.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 7%

---


# Images par seconde

La variable images par seconde est la fréquence d’images actuelle du flux. Définissez-le sur l’objet QoE à côté du débit et des images perdues afin que le serveur principal dispose d’un contexte de qualité complète pour chaque session de lecture. Adobe Analytics ne crée pas automatiquement de variable de création de rapports pour la fréquence d’image ; créez une règle de traitement personnalisée si vous souhaitez qu’elle apparaisse sous la forme d’un rapport.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | Aucune (Adobe Analytics n’attribue pas de clé de données contextuelles réservée pour la fréquence d’image) |
| **champ de collection XDM** | [`xdm.mediaCollection.qoeDataDetails.framesPerSecond`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Caractéristique** | S.O. |
| **Obligatoire** | Non |
| **Envoyé avec** | Événements de qualité ([changement de débit](/help/implementation/events/playback/bitrate-change.md), [début de la mémoire tampon](/help/implementation/events/playback/buffer-start.md), [erreur](/help/implementation/events/error.md)), fermeture de la session |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`framesPerSecond` à l’intérieur des `xdm.mediaCollection.qoeDataDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        framesPerSecond: 24
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

Transmettez la fréquence d’image comme troisième argument (`fps`) à `createQoEObject`.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

Transmettez la fréquence d’image comme troisième argument (`fps`) à `createQoEObject`.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku Edge]

`framesPerSecond` à l’intérieur des `xdm.mediaCollection.qoeDataDetails` lors de l’appel de `sendMediaEvent` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "framesPerSecond": 24
            },
            "playhead": 90
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) avec `framesPerSecond` à l’intérieur du `xdm.mediaCollection.qoeDataDetails` :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "framesPerSecond": 24
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

Transmettez la fréquence d’image comme troisième argument à `ADB.Media.createQoEObject` :

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
```

>[!TAB  Chromecast ]

Transmettez la fréquence d’image comme troisième argument (`fps`) pour `ADBMobile.media.createQoSObject` et mettre à jour le dispositif de suivi :

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Roku 2.x]

Transmettez la fréquence d’image comme troisième argument (`fps`) pour `adb_media_init_qosinfo` et mettre à jour le dispositif de suivi avec `mediaUpdateQoS` :

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(3200.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
```

>[!TAB  API Media Collection ]

Incluez `media.qoe.framesPerSecond` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.framesPerSecond": 24
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
