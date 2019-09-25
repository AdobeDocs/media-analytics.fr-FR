---
seo-title: Suivi de la lecture principale sur Roku
title: Suivi de la lecture principale sur Roku
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Suivi de la lecture principale sur Roku{#track-core-playback-on-roku}

>[!IMPORTANT]
>Cette documentation couvre le suivi dans la version 2.x du SDK. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK](/help/sdk-implement/download-sdks.md).

1. **Configuration initiale du suivi**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   **`MediaObject`référence :**

   | Nom de variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom de la vidéo | Oui |
   | `mediaid` | Identifiant unique de la vidéo | Oui |
   | `length` | Durée de la vidéo | Oui |
   | `streamType` | Type de diffusion (voir les constantes _StreamType_ ci-dessous) | Oui |
   | `mediaType` | Type de média (voir les constantes _MediaType_ ci-dessous) | Oui |

   **`StreamType`constantes :**

   | Nom de constante | Description   |
   |---|---|
   | `MEDIA_STREAM_TYPE_VOD` | Type de diffusion pour la vidéo à la demande. |
   | `MEDIA_STREAM_TYPE_LIVE` | Type de diffusion pour le contenu LIVE. |
   | `MEDIA_STREAM_TYPE_LINEAR` | Type de diffusion pour le contenu LINEAR. |
   | `MEDIA_STREAM_TYPE_AOD` | Type de diffusion pour l’audio à la demande. |
   | `MEDIA_STREAM_TYPE_AUDIOBOOK` | Type de diffusion pour les livres audio. |
   | `MEDIA_STREAM_TYPE_PODCAST` | Type de diffusion pour les podcasts. |

   **`MediaType`constantes :**

   | Nom de constante | Description |
   |---|---|
   | `MEDIA_STREAM_TYPE_AUDIO` | Type de média pour les diffusions audio. |
   | `MEDIA_STREAM_TYPE_VIDEO` | Type de média pour les diffusions vidéo. |

   **Créez un objet d’informations sur le média pour une vidéo avec du contenu VOD :**

   ```
    mediaInfo = adb_media_init_mediainfo(
     "<MEDIA_NAME>",
     "<MEDIA_ID>",
     600,
     ADBMobile().MEDIA_STREAM_TYPE_VOD,
     ADBMobile().MEDIA_TYPE_VIDEO
   )
   ```

   ou

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_VOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_VIDEO
   ```

   **Créez un objet d’informations sur le média pour une vidéo avec du contenu AOD :**

   ```
   mediaInfo = adb_media_init_mediainfo(
    "<MEDIA_NAME>", 
    "<MEDIA_ID>", 
    600, 
    ADBMobile().MEDIA_STREAM_TYPE_AOD, 
    ADBMobile().MEDIA_TYPE_AUDIO
   )
   ```

   ou

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_AOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_AUDIO
   ```

1. **Ajout de métadonnées**

   Vous pouvez associer des objets de métadonnées standard et/ou personnalisés à la session de suivi au moyen de variables de données contextuelles.

   * **Métadonnées standard**

      [Mise en œuvre de métadonnées standard sur JavaScript](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >L’association de l’objet de métadonnées standard à l’objet multimédia est facultative.

      * Référence à l’API des clés de métadonnées multimédia - [Clés de métadonnées standard - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         See the comprehensive set of available metadata here: [Audio and video parameters](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Métadonnées personnalisées**

      Créez un objet variable pour les variables personnalisées et renseignez les données de ce média. Par exemple :

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```


1. **Suivi de l’intention de démarrer la lecture**

   Pour commencer le suivi d’une session multimédia, appelez `trackSessionStart` l’instance Media Heartbeat :

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >La seconde valeur est le nom d’objet de métadonnées de média personnalisé que vous avez créé à l’étape 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` effectue le suivi de l’intention de lecture de l’utilisateur, et non du début de la lecture. Cette API est utilisée pour charger les données/métadonnées et estimer le temps jusqu’au démarrage de la mesure QoS (durée entre `trackSessionStart` et `trackPlay`).

   >[!NOTE]
   >
   >If you are not using custom metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **Suivi du début réel de la lecture**

   Identify the event from the media player for the beginning of the playback, where the first frame of the media is rendered on the screen, and call `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **Suivi de la fin de la lecture**

   Identify the event from the media player for the completion of the playback, where the user has watched the content until the end, and call `trackComplete`:

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **Suivi de la fin de la session**

   Identify the event from the media player for the unloading/closing of the playback, where the user closes the media and/or the media is completed and has been unloaded, and call `trackSessionEnd`:

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >A `trackSessionEnd` marks the end of a tracking session. Si la session a été visionnée jusqu’à la fin, où l’utilisateur a visionné le contenu jusqu’à la fin, assurez-vous que `trackComplete` est appelé avant `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.  Méthode de suivi de lecture de média pour suivre le chargement du média et définir la session actuelle sur active :

   ```
   ‘ Create a media info object
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.id = <MEDIA_ID>
   mediaInfo.playhead = "0"
   mediaInfo.length = "600"
   ```

1. **Ajout de métadonnées vidéo**

   Vous pouvez associer des objets de métadonnées vidéo standard et/ou personnalisés à la session de suivi vidéo au moyen de variables de données contextuelles.

   * **Métadonnées vidéo standard**

      [Mise en œuvre de métadonnées standard sur Roku](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

      >[!NOTE]
      >L’association de l’objet de métadonnées vidéo standard à l’objet multimédia est facultative.

   * **Métadonnées personnalisées**

      Créez un objet variable pour les variables personnalisées et renseignez les données de cette vidéo. Par exemple :

      ```
      mediaContextData = {}
      mediaContextData["cmk1"] = "cmv1"
      mediaContextData["cmk2"] = "cmv2"
      ```

1. **Suivi de l’intention de démarrer la lecture**

   Pour commencer le suivi d’une session multimédia, appelez `trackSessionStart` l’instance Media Heartbeat :

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >La seconde valeur est le nom d’objet de métadonnées vidéo personnalisé que vous avez créé à l’étape 2.

   >[!IMPORTANT]
   >`trackSessionStart` effectue le suivi de l’intention de lecture de l’utilisateur, et non du début de la lecture. Cette API est utilisée pour charger les données/métadonnées de la vidéo et estimer le temps jusqu’au démarrage de la mesure QoS (durée entre `trackSessionStart` et `trackPlay`).

   >[!NOTE]
   >If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **Suivi du début réel de la lecture**

   Identifiez l’événement du lecteur vidéo correspondant au début de la lecture vidéo, où la première image de la vidéo s’affiche à l’écran, et appelez `trackPlay` :

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **Suivi de la fin de la lecture**

   Identifiez l’événement du lecteur vidéo correspondant à la fin de la lecture vidéo, où l’utilisateur a visionné le contenu jusqu’à la fin, et appelez `trackComplete` :

   ```
   ADBMobile().mediaTrackComplete()
   ```

1. **Suivi de la fin de la session**

   Identifiez l’événement du lecteur vidéo correspondant au déchargement/à la fermeture de la lecture vidéo, où l’utilisateur ferme la vidéo et/ou la vidéo est terminée et déchargée, et appelez `trackSessionEnd` :

   ```
   ADBMobile().mediaTrackSessionEnd()
   ```

   >[!IMPORTANT]
   >`trackSessionEnd` marque la fin d’une session de suivi vidéo. Si la session a été visionnée jusqu’à la fin, où l’utilisateur a visionné le contenu jusqu’à la fin, assurez-vous que `trackComplete` est appelé avant `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **Suivi de tous les scénarios de mise en pause possibles**

   Identifiez l’événement du lecteur vidéo correspondant à l’interruption de la vidéo et appelez `trackPause`:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **Suspendre les scénarios**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. Les scénarios suivants exigent tous que votre application appelle `trackPause()`:

   * L’utilisateur appuie explicitement sur le bouton de pause dans l’application.
   * Le lecteur se place dans l’état de pause.
   * (*Applications mobiles*) - L’utilisateur place l’application en arrière-plan, mais vous souhaitez que l’application maintienne la session ouverte.
   * (*Applications mobiles*) - Tout type d’interruption système qui entraîne la mise en arrière-plan d’une application. Par exemple, l’utilisateur reçoit un appel ou une fenêtre contextuelle d’une autre application apparaît, mais vous souhaitez que l’application maintienne la session active afin que l’utilisateur ait l’opportunité de reprendre la vidéo à partir du point d’interruption.

1. Identifiez l’événement du lecteur correspondant à la lecture vidéo et/ou à la reprise vidéo après une interruption et appelez `trackPlay` :

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >Il peut s’agir de la même source d’événement utilisée à l’étape 4. Assurez-vous que chaque appel de l’API `trackPause()` est suivi d’un appel de l’API `trackPlay()` à la reprise de la lecture vidéo.

* Scénarios de suivi : [Lecture VOD sans publicité](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Exemple de lecteur inclus dans le SDK Roku pour un exemple de suivi complet

