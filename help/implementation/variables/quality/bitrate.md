---
title: Débit binaire
description: Définissez le débit de lecture actuel (en Kbits/s) sur l’objet QoE afin que le serveur principal puisse calculer les mesures de débit.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 5%

---


# Débit binaire

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Bitrate**. Voir [[!UICONTROL Débit moyen] (dimension)](/help/reporting/dimensions/average-bitrate.md) et [[!UICONTROL Débit moyen] (mesure)](/help/reporting/metrics/average-bitrate.md) pour les variables de rapports correspondantes.*

>[!ENDSHADEBOX]

La variable de débit est le débit de lecture actuel, en kilobits par seconde. Définissez-le sur l’objet QoE chaque fois que le lecteur négocie un débit, puis mettez à jour l’objet QoE lorsque le débit change. Le serveur principal utilise des valeurs de débit pour calculer la mesure [[!UICONTROL Débit moyen]](/help/reporting/metrics/average-bitrate.md), la dimension par débit-intervalle et la mesure [[!UICONTROL Modifications du débit]](/help/reporting/metrics/bitrate-changes.md).

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.qoe.bitrateAverageBucket` |
| **champ de collection XDM** | [`xdm.mediaCollection.qoeDataDetails.bitrate`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.qoe.bitrateAverageBucket` |
| **Obligatoire** | Non |
| **Envoyé avec** | Événements de qualité ([changement de débit](/help/implementation/events/playback/bitrate-change.md), [début de la mémoire tampon](/help/implementation/events/playback/buffer-start.md), [erreur](/help/implementation/events/error.md)), fermeture de la session |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

Définissez des `bitrate` internes `xdm.mediaCollection.qoeDataDetails` sur `media.bitrateChange` (ou tout événement lié à la qualité) lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

Transmettez le débit binaire comme premier argument à `createQoEObject`. Mettez à jour l’objet QoE sur le dispositif de suivi avant le déclenchement d’un événement de qualité.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

Transmettez le débit binaire comme premier argument à `createQoEObject`. Mettez à jour l’objet QoE sur le dispositif de suivi avant le déclenchement d’un événement de qualité.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku Edge]

Définissez des `bitrate` à l’intérieur des `xdm.mediaCollection.qoeDataDetails` lors de l’appel de `sendMediaEvent` pour des événements de qualité tels que `media.bitrateChange` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 90
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) avec `bitrate` à l’intérieur du `xdm.mediaCollection.qoeDataDetails` :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 3200
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

Transmettez le débit comme premier argument pour `ADB.Media.createQoEObject` et mettre à jour le dispositif de suivi :

```javascript
var qoeObject = ADB.Media.createQoEObject(
  3200,  // bitrate (kbps)
  0,     // startup time (ms)
  24,    // fps
  0      // dropped frames
);

tracker.updateQoEObject(qoeObject);
```

>[!TAB  Chromecast ]

Transmettez le débit en kbit/s comme premier argument pour `ADBMobile.media.createQoSObject` et mettre à jour le dispositif de suivi :

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate (kbps)
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Roku 2.x]

Transmettez le débit en kbit/s comme premier argument pour `adb_media_init_qosinfo` et mettre à jour le dispositif de suivi avec `mediaUpdateQoS` :

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(3200.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
```

>[!TAB  API Media Collection ]

Incluez `media.qoe.bitrate` dans l’objet `params` de votre `bitrateChange` requête POST :

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.bitrate": 3200
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
