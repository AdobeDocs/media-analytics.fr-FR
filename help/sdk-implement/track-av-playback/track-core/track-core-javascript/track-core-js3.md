---
title: Suivi de la lecture principale à l’aide de JavaScript v3.x
description: Cette rubrique explique comment mettre en oeuvre le suivi de base à l’aide du SDK Media dans un navigateur utilisant des applications JavaScript 3.x.
translation-type: tm+mt
source-git-commit: 40d75ef32596e915ac07c173b4595bb78db3688d
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 81%

---


# Suivi de la lecture principale à l’aide de JavaScript 3.x{#track-core-playback-on-javascript}

>[!IMPORTANT]
>Cette documentation aborde le suivi dans la version 3.x du SDK. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs](/help/sdk-implement/download-sdks.md)

1. **Configuration initiale du suivi**

   Déterminez le moment où l’utilisateur déclenche l’intention de lecture (l’utilisateur clique sur le bouton de lecture et/ou la lecture automatique est activée) et créez une instance `MediaObject`.

   [API createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Nom de variable | Type | Description |
   | --- | --- | --- |
   | `name` | string | Chaîne non vide indiquant le nom du média. |
   | `id` | string | Chaîne non vide indiquant un identifiant de média unique. |
   | `length` | nombre | Nombre positif indiquant la longueur du média en secondes. Utilisez 0 si la longueur est inconnue. |
   | `streamType` | string |  |
   | `mediaType` |  | Type de média (audio ou vidéo). |

   **`StreamType`Constantes :**

   | Nom de constante | Description   |
   |---|---|
   | `VOD` | Type de diffusion pour la vidéo à la demande. |
   | `AOD` | Type de diffusion pour l’audio à la demande. |

   **`MediaType`Constantes :**

   | Nom de constante | Description |
   |---|---|
   | `Audio` | Type de média pour les diffusions audio. |
   | `Video` | Type de média pour les diffusions vidéo. |

   ```
   var mediaObject = ADB.Media.createMediaObject(<MEDIA_NAME>,
                                     <MEDIA_ID,
                                     <MEDIA_LENGTH>,
                                     <STREAM_TYPE>,
                                     <MEDIA_TYPE>);
   ```

1. **Ajout de métadonnées**

   Vous pouvez associer des métadonnées standard et/ou personnalisées à la session de suivi au moyen de variables de données contextuelles.

   * **Métadonnées standard**

      >[!NOTE]
      >
      >L’attachement des métadonnées standard est facultatif.

      * Référence à l’API des clés de métadonnées multimédia - [Clés de métadonnées standard - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         Consultez la liste complète des métadonnées disponibles dans la rubrique [Paramètres audio et vidéo](/help/metrics-and-metadata/audio-video-parameters.md).
   * **Métadonnées personnalisées**

      Créez un objet de variable pour les variables personnalisées et renseignez les données de ce média. Par exemple :

      ```js
      /* Set context data */
       var contextData = {};
      
       //Standard metadata
       contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
       contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
      
       //Custom metadata
       contextData["isUserLoggedIn"] = "false";
       contextData["tvStation"] = "Sample TV Station";
      ```


1. **Suivi de l’intention de démarrer la lecture**

   Pour commencer le suivi d’une session multimédia, appelez `trackSessionStart` sur l’instance Media Heartbeat :

   ```js
   var mediaObject = ADB.Media.createMediaObject("video-name",
                                                 "video-id",
                                                 60.0,
                                                 ADB.Media.StreamType.VOD,
                                                 ADB.Media.MediaType.Video);
   
   var contextData = {};
   
   //Standard metadata
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
   
   //Custom metadata
   contextData["isUserLoggedIn"] = "false";
   contextData["tvStation"] = "Sample TV Station";
   
   tracker.trackSessionStart(mediaObject, contextData);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` effectue le suivi de l’intention de lecture de l’utilisateur, et non du début de la lecture. Cette API est utilisée pour charger les données/métadonnées et estimer le temps jusqu’au démarrage de la mesure QoS (durée entre `trackSessionStart` et `trackPlay`).

   >[!NOTE]
   >
   >If you are not using contextData, simply send an empty object for the `data` argument in `trackSessionStart`.

1. **Suivi du début réel de la lecture**

   Identifiez l’événement du lecteur multimédia correspondant au début de la lecture, où la première image du média s’affiche à l’écran, et appelez `trackPlay` :

   ```js
   tracker.trackPlay();
   ```

1. **Suivi de la fin de la lecture**

   Identifiez l’événement du lecteur multimédia correspondant à la fin de la lecture, où l’utilisateur a visionné le contenu jusqu’à la fin, et appelez `trackComplete` :

   ```js
   tracker.trackComplete();
   ```

1. **Suivi de la fin de la session**

   Identifiez l’événement du lecteur multimédia correspondant au déchargement/à la fermeture de la lecture, où l’utilisateur ferme la vidéo et/ou le contenu média est terminé et déchargé, et appelez `trackSessionEnd` :

   ```js
   tracker.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marque la fin d’une session de suivi. Si la session a été visionnée jusqu’à la fin, où l’utilisateur a visionné le contenu jusqu’à la fin, assurez-vous que `trackComplete` est appelé avant `trackSessionEnd`. Tout autre appel à l’API `track*` est ignoré après `trackSessionEnd`, sauf `trackSessionStart` dans le cadre d’une nouvelle session de suivi.

1. **Suivi de tous les scénarios de mise en pause possibles**

   Identifiez l’événement du lecteur multimédia pour le mettre en pause et appelez `trackPause` :

   ```js
   tracker.trackPause();
   ```

   **Scénarios de mise en pause**

   Identifiez tous les scénarios dans lesquels le lecteur multimédia sera interrompu et assurez-vous que `trackPause` est correctement appelé. Les scénarios suivants exigent tous que votre application appelle `trackPause()` :

   * L’utilisateur appuie délibérément sur pause dans l’application.
   * Le lecteur se met en pause.
   * (*Applications mobiles*) : l’utilisateur place l’application en arrière-plan, mais vous souhaitez que l’application conserve la session ouverte.
   * (*Applications mobiles*) : tout type d’interruption système qui entraîne la mise en arrière-plan d’une application. Par exemple, l’utilisateur reçoit un appel ou une fenêtre contextuelle provenant d’une autre application apparaît, mais vous souhaitez que l’application conserve la session ouverte pour donner à l’utilisateur la possibilité de reprendre le média à partir du point d’interruption.

1. Identifiez l’événement du lecteur correspondant à la lecture et/ou à la reprise après une interruption et appelez `trackPlay` :

   ```js
   tracker.trackPlay();
   ```

   >[!TIP]
   >
   >Il peut s’agir de la même source d’événement utilisée à l’étape 4. Assurez-vous que chaque appel de l’API `trackPause()` est suivi d’un appel de l’API `trackPlay()` à la reprise de la lecture.

* Scénarios de suivi : [lecture VOD sans publicité](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Exemple de lecteur inclus avec le SDK JavaScript pour un exemple de suivi complet.