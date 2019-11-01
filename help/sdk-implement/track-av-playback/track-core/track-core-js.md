---
title: Suivi de la lecture principale sur JavaScript
description: Cette rubrique décrit la mise en oeuvre du suivi de base à l’aide du SDK multimédia dans les applications de navigateur (JS).
uuid: 3d6e0ab1-899a-43c3-b632-8276e84345ab
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Suivi de la lecture principale sur JavaScript{#track-core-playback-on-javascript}

>[!IMPORTANT]
>Cette documentation couvre le suivi dans la version 2.x du SDK. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK](/help/sdk-implement/download-sdks.md).

1. **Configuration initiale du suivi**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [API createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Nom de variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom du média | Oui |
   | `mediaid` | Identifiant unique du média | Oui |
   | `length` | Durée du média | Oui |
   | `streamType` | Type de diffusion (voir les constantes _StreamType_ ci-dessous) | Oui |
   | `mediaType` | Type de média (voir les constantes _MediaType_ ci-dessous) | Oui |

   **`StreamType`constantes :**

   | Nom de constante | Description   |
   |---|---|
   | `VOD` | Type de diffusion pour la vidéo à la demande. |
   | `LIVE` | Type de diffusion pour le contenu LIVE. |
   | `LINEAR` | Type de diffusion pour le contenu LINEAR. |
   | `AOD` | Type de diffusion pour Audio à la demande. |
   | `AUDIOBOOK` | Type de diffusion pour le livre audio. |
   | `PODCAST` | Type de diffusion pour Podcast. |

   **`MediaType`constantes :**

   | Nom de constante | Description |
   |---|---|
   | `Audio` | Type de média pour les diffusions audio. |
   | `Video` | Type de média pour les diffusions vidéo. |

   ```
   var mediaObject =  
     MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>, 
                                     MediaHeartbeat.StreamType.VOD,
                                     <MEDIA_TYPE>);
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
   >`trackSessionEnd` marque la fin d’une session de suivi. Si la session a été visionnée jusqu’à la fin, où l’utilisateur a visionné le contenu jusqu’à la fin, assurez-vous que `trackComplete` est appelé avant `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.

1. **Suivi de tous les scénarios de mise en pause possibles**

   Identifiez l'événement du lecteur multimédia pour le mettre en pause et l'appeler `trackPause`:

   ```js
   mediaHeartbeat.trackPause();
   ```

   **Suspendre les scénarios**

   Identify any scenario in which the media player will pause and make sure that `trackPause` is properly called. Les scénarios suivants exigent tous que votre application appelle `trackPause()`:

   * L’utilisateur appuie explicitement sur le bouton de pause dans l’application.
   * Le lecteur se place dans l’état de pause.
   * (*Applications mobiles*) - L’utilisateur place l’application en arrière-plan, mais vous souhaitez que l’application maintienne la session ouverte.
   * (*Applications mobiles*) - Tout type d’interruption système qui entraîne la mise en arrière-plan d’une application. Par exemple, l’utilisateur reçoit un appel ou une fenêtre contextuelle d’une autre application apparaît, mais vous souhaitez que l’application maintienne la session active afin que l’utilisateur ait l’opportunité de reprendre le média à partir du point d’interruption.

1. Identifiez l’événement du lecteur correspondant à la lecture et/ou à la reprise après une interruption et appelez `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >Il peut s’agir de la même source d’événement utilisée à l’étape 4. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the playback resumes.

* Scénarios de suivi : [Lecture VOD sans publicité](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Exemple de lecteur inclus dans le SDK JavaScript pour un exemple de suivi complet

