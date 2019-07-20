---
seo-title: Suivi de la lecture principale sur Android
title: Suivi de la lecture principale sur Android
uuid: ab 5 fab 95-76 ed -4 ae 6-aedb -2 e 66 eece 7607
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Suivi de la lecture principale sur Android{#track-core-playback-on-android}

>[!IMPORTANT]
>Cette documentation couvre le suivi dans la version 2. x du SDK. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger le Guide du développeur 1.x pour Android dans la rubrique [Téléchargement des SDK](../../../sdk-implement/download-sdks.md).

1. **Configuration initiale du suivi**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [API createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)

   | Nom de variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom du média | Oui |
   | `mediaId` | Identifiant unique du média | Oui |
   | `length` | Durée du média | Oui |
   | `streamType` | Stream type (see _StreamType constants_ below) | Oui |
   | `mediaType` | Media type (see _MediaType constants_ below) | Oui |

   **`StreamType`constantes :**

   | Nom de constante | Description |
   |---|---|
   | `VOD` | Type de diffusion pour la vidéo à la demande. |
   | `LIVE` | Type de diffusion pour le contenu en direct. |
   | `LINEAR` | Type de diffusion pour le contenu linéaire. |
   | `AOD` | Type de diffusion pour l’audio à la demande. |
   | `AUDIOBOOK` | Type de diffusion pour les livres audio. |
   | `PODCAST` | Type de diffusion pour les podcasts. |

   **`MediaType`constantes :**

   | Nom de constante | Description |
   |---|---|
   | `Audio` | Type de média pour les diffusions audio. |
   | `Video` | Type de média pour les diffusions vidéo. |

   ```
   MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
     <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);
   ```

1. **Ajout de métadonnées**

   Vous pouvez éventuellement joindre des objets de métadonnées standard et/ou personnalisés à la session de suivi par le biais de variables de données contextuelles.

   * **Métadonnées standard**

      [Mise en œuvre de métadonnées standard sur Android](../../../sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)

      >[!NOTE]
      >
      >L'ajout de l'objet de métadonnées standard à l'objet media est facultatif.

      * Référence de l’API des clés de métadonnées multimédia - [Clés de métadonnées standard - Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
      * Consultez la liste complète des métadonnées vidéo disponibles dans la rubrique [Paramètres audio et vidéo](../../../metrics-and-metadata/audio-video-parameters.md).
   * **Métadonnées personnalisées**

      Créez un dictionnaire pour les variables personnalisées et renseignez les données de ce média. Par exemple :

      ```java
      HashMap<String, String> mediaMetadata =  
        new HashMap<String, String>(); 
      mediaMetadata.put("isUserLoggedIn", "false"); 
      mediaMetadata.put("tvStation", "Sample TV Station"); 
      mediaMetadata.put("programmer", "Sample programmer");
      ```


1. **Suivre l'intention de commencer la lecture**

   To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance. Par exemple :

   ```java
   public void onVideoLoad(Observable observable, Object data) {  
       _heartbeat.trackSessionStart(mediaInfo, mediaMetadata); 
   }
   ```

   >[!TIP]
   >
   >La seconde valeur correspond au nom d'objet de métadonnées de média personnalisé créé à l'étape 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` effectue le suivi de l’intention de lecture de l’utilisateur, et non du début de la lecture. Cette API est utilisée pour charger les données/métadonnées du média et estimer le temps jusqu’au démarrage de la mesure QoS (durée entre `trackSessionStart` et `trackPlay`).

   >[!NOTE]
   >
   >If you are not using custom media metadata, simply send an empty object for the second argument in `trackSessionStart`.

1. **Suivi du début réel de la lecture**

   Identify the event from the media player for the beginning of the media playback, where the first frame of the media is rendered on the screen, and call `trackPlay`:

   ```java
   // Video is rendered on the screen) and call trackPlay.  
   public void onVideoPlay(Observable observable, Object data) { 
       _heartbeat.trackPlay(); 
   }
   ```

1. **Suivi de la fin de la lecture**

   Identify the event from the media player for the completion of the media playback, where the user has watched the content until the end, and call `trackComplete`:

   ```java
   public void onVideoComplete(Observable observable, Object data) { 
       _heartbeat.trackComplete(); 
   }
   ```

1. **Suivi de la fin de la session**

   Identify the event from the media player for the unloading/closing of the media playback, where the user closes the media and/or the media is completed and has been unloaded, and call `trackSessionEnd`:

   ```java
   // Closes the media and/or the media completed and unloaded,  
   // and call trackSessionEnd().  
   public void onMainVideoUnload(Observable observable, Object data) {  
       _heartbeat.trackSessionEnd(); 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marque la fin d'une session de suivi multimédia. Si la session a été visionnée jusqu’à la fin, où l’utilisateur a visionné le contenu jusqu’à la fin, assurez-vous que `trackComplete` est appelé avant `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new media tracking session.

1. **Suivre tous les scénarios de mise en pause possibles**

   Identify the event from the media player for media pause and call `trackPause`:

   ```java
   public void onVideoPause(Observable observable, Object data) {  
       _heartbeat.trackPause(); 
   }
   ```

   **Scénarios de pause**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. Les scénarios suivants exigent tous que votre application appelle `trackPause()`:

   * L’utilisateur appuie explicitement sur le bouton de pause dans l’application.
   * Le lecteur se place dans l’état de pause.
   * (*Applications mobiles*) - L’utilisateur place l’application en arrière-plan, mais vous souhaitez que l’application maintienne la session ouverte.
   * (*Applications mobiles*) - Tout type d’interruption système qui entraîne la mise en arrière-plan d’une application. Par exemple, l’utilisateur reçoit un appel ou une fenêtre contextuelle d’une autre application apparaît, mais vous souhaitez que l’application maintienne la session active afin que l’utilisateur ait l’opportunité de reprendre le média à partir du point d’interruption.

1. Identifiez l’événement du lecteur correspondant à la lecture multimédia et/ou à la reprise multimédia après une interruption et appelez `trackPlay`.

   ```java
   // trackPlay() 
   public void onVideoPlay(Observable observable, Object data) {  
       _heartbeat.trackPlay(); 
   }
   ```

   >[!TIP]
   >
   >Il peut s'agir de la même source d'événement utilisée à l'étape 4. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the media playback resumes.

Consultez les ressources suivantes pour en savoir plus sur le suivi de la lecture principale :

* Scénarios de suivi : [Lecture VOD sans publicité](../../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Exemple de lecteur inclus dans le SDK Android pour un exemple de suivi complet

