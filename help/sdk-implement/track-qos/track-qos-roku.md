---
title: Suivi de la qualité de l’expérience sur Roku
description: Cette rubrique décrit l’implémentation du suivi de la qualité de l’expérience (QoE, QoS) à l’aide du SDK Media sur Roku.
uuid: a8b242ab-da3c-4297-9eef-f0b9684ef56a
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Suivi de la qualité de l’expérience sur Roku{#track-quality-of-experience-on-roku}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

## Mise en oeuvre de QOS

1. Déterminez le moment où le débit change lors de la lecture du média et utilisez l’ `mediaUpdateQoS` API pour mettre à jour les informations de qualité de service sur le SDK multimédia.

   Variables QoSObject :

   >[!TIP]
   >
   >Ces variables ne sont requises que si vous effectuez le suivi de la qualité de service.

   | Variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `bitrate` | Débit actuel | Oui |
   | `startupTime` | Temps de démarrage | Oui |
   | `fps` | Valeur fps | Oui |
   | `droppedFrames` | Nombre de pertes d’images | Oui |

   Par exemple :

   ```
   bitrate = 200000
   fps = 0
   droppedFrames = 1
   startupTime = 2
   qosinfo = adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)
   
   ADBMobile().mediaUpdateQoS(qosinfo)
   ```

   <!--
    QoS object creation:
 
    ```
    qosInfo=adb_media_init_qosinfo()
    qosInfo.bitrate = 200000
    qosInfo.fps = 0
    qosInfo.droppedFrames = 1
    qosInfo.startupTime = 2
    ```
    -->

1. Lorsque la lecture change de débit, appelez `trackEvent(BitrateChange)` pour informer le SDK multimédia que le débit a changé.

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_BITRATE_CHANGE)
   ```

   >[!NOTE]
   >
   >Vous devez appeler `updateQoSObject` avec la valeur de débit mise à jour.

   <!--
    ```
    qosContextData = {}
    ADBMobile().mediaTrackEvent(MEDIA_BITRATE_CHANGE, qosInfo, qosContextData)
    ```
 
    >[!IMPORTANT]
    >
    >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.
    -->

1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (Voir [Aperçu](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Le suivi des erreurs du lecteur multimédia n’arrête pas la session de suivi multimédia. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

