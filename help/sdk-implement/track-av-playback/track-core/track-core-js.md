---
title: Suivi de la lecture principale à l’aide de JavaScript 2.x
description: Cette rubrique explique comment mettre en oeuvre le suivi de base à l’aide du SDK Media dans un navigateur utilisant des applications JavaScript 2.x.
uuid: 3d6e0ab1-899a-43c3-b632-8276e84345ab
translation-type: tm+mt
source-git-commit: 30ed54924c75a9c33e6122b2d7ddbb84c06b8c0c
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 95%

---


# Suivi de la lecture principale à l’aide de JavaScript 2.x{#track-core-playback-on-javascript}

>[!IMPORTANT]
>Cette documentation aborde le suivi dans la version 2.x du SDK. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK](/help/sdk-implement/download-sdks.md).

1. **Configuration initiale du suivi**

   Déterminez le moment où l’utilisateur déclenche l’intention de lecture (l’utilisateur clique sur le bouton de lecture et/ou la lecture automatique est activée) et créez une instance `MediaObject`.

   [API createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Nom de variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom du média | Oui |
   | `mediaid` | Identifiant unique du média | Oui |
   | `length` | Longueur du média | Oui |
   | `streamType` | Type de diffusion (voir les constantes _StreamType_ ci-dessous) | Oui |
   | `mediaType` | Type de média (voir les constantes _MediaType_ ci-dessous) | Oui |

   **`StreamType`Constantes :**

   | Nom de constante | Description   |
   |---|---|
   | `VOD` | Type de diffusion pour la vidéo à la demande. |
   | `LIVE` | Type de diffusion pour le contenu en direct. |
   | `LINEAR` | Type de diffusion pour le contenu linéaire. |
   | `AOD` | Type de diffusion pour l’audio à la demande. |
   | `AUDIOBOOK` | Type de diffusion pour les livres audio. |
   | `PODCAST` | Type de diffusion pour les podcasts. |

   **`MediaType`Constantes :**

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

   Vous pouvez joindre des métadonnées standard et/ou de publicité à la session de suivi par le biais de variables de données contextuelles.

   * **Métadonnées standard**

      [Mise en œuvre de métadonnées standard sur JavaScript](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >Il est facultatif de joindre un objet de métadonnées standard à l’objet multimédia.

      * Référence à l’API des clés de métadonnées multimédia - [Clés de métadonnées standard - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         Consultez la liste complète des métadonnées disponibles dans la rubrique [Paramètres audio et vidéo](/help/metrics-and-metadata/audio-video-parameters.md).
   * **Métadonnées personnalisées**

      Créez un objet de variable pour les variables personnalisées et renseignez les données de ce média. Par exemple :

      ```js
      /* Set custom context data */
      var customVideoMetadata = {
          isUserLoggedIn: "false",
          tvStation: "Sample TV station",
          programmer: "Sample programmer"
      };
      ```


1. **Suivi de l’intention de démarrer la lecture**

   Pour commencer le suivi d’une session multimédia, appelez `trackSessionStart` sur l’instance Media Heartbeat :

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >La deuxième valeur est le nom d’objet de métadonnées multimédia personnalisé que vous avez créé à l’étape 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` effectue le suivi de l’intention de lecture de l’utilisateur, et non du début de la lecture. Cette API est utilisée pour charger les données/métadonnées et estimer le temps jusqu’au démarrage de la mesure QoS (durée entre `trackSessionStart` et `trackPlay`).

   >[!NOTE]
   >
   >Si vous n’utilisez pas de métadonnées personnalisées, envoyez simplement un objet vide pour l’argument `data` dans `trackSessionStart`, tel que décrit dans la ligne commentée de l’exemple iOS ci-dessus.

1. **Suivi du début réel de la lecture**

   Identifiez l’événement du lecteur multimédia correspondant au début de la lecture, où la première image du média s’affiche à l’écran, et appelez `trackPlay` :

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **Suivi de la fin de la lecture**

   Identifiez l’événement du lecteur multimédia correspondant à la fin de la lecture, où l’utilisateur a visionné le contenu jusqu’à la fin, et appelez `trackComplete` :

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **Suivi de la fin de la session**

   Identifiez l’événement du lecteur multimédia correspondant au déchargement/à la fermeture de la lecture, où l’utilisateur ferme la vidéo et/ou le contenu média est terminé et déchargé, et appelez `trackSessionEnd` :

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marque la fin d’une session de suivi. Si la session a été visionnée jusqu’à la fin, où l’utilisateur a visionné le contenu jusqu’à la fin, assurez-vous que `trackComplete` est appelé avant `trackSessionEnd`. Tout autre appel à l’API `track*` est ignoré après `trackSessionEnd`, sauf `trackSessionStart` dans le cadre d’une nouvelle session de suivi.

1. **Suivi de tous les scénarios de mise en pause possibles**

   Identifiez l’événement du lecteur multimédia pour le mettre en pause et appelez `trackPause` :

   ```js
   mediaHeartbeat.trackPause();
   ```

   **Scénarios de mise en pause**

   Identifiez tous les scénarios dans lesquels le lecteur multimédia sera interrompu et assurez-vous que `trackPause` est correctement appelé. Les scénarios suivants exigent tous que votre application appelle `trackPause()` :

   * L’utilisateur appuie délibérément sur pause dans l’application.
   * Le lecteur se met en pause.
   * (*Applications mobiles*) : l’utilisateur place l’application en arrière-plan, mais vous souhaitez que l’application conserve la session ouverte.
   * (*Applications mobiles*) : tout type d’interruption système qui entraîne la mise en arrière-plan d’une application. Par exemple, l’utilisateur reçoit un appel ou une fenêtre contextuelle provenant d’une autre application apparaît, mais vous souhaitez que l’application conserve la session ouverte pour donner à l’utilisateur la possibilité de reprendre le média à partir du point d’interruption.

1. Identifiez l’événement du lecteur correspondant à la lecture et/ou à la reprise après une interruption et appelez `trackPlay` :

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >Il peut s’agir de la même source d’événement utilisée à l’étape 4. Assurez-vous que chaque appel de l’API `trackPause()` est suivi d’un appel de l’API `trackPlay()` à la reprise de la lecture.

* Scénarios de suivi : [lecture VOD sans publicité](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Exemple de lecteur inclus avec le SDK JavaScript pour un exemple de suivi complet.
