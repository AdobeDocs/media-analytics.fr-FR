---
title: Découvrez comment effectuer le suivi de la lecture principale sur iOS
description: Cette rubrique décrit la mise en œuvre du suivi principal à l’aide du SDK Media sur iOS.
uuid: bdc0e05c-4fe5-430e-aee2-f331bc59ac6b
exl-id: 5c6b36b3-a421-45a4-a65e-4eb57513ca4a
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 100%

---

# Suivi de la lecture principale sur iOS{#track-core-playback-on-ios}

Cette documentation aborde le suivi dans la version 2.x du SDK.

>[!IMPORTANT]
>Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK](/help/getting-started/download-sdks.md).

1. **Configuration initiale du suivi**

   Déterminez le moment où l’utilisateur déclenche l’intention de lecture (l’utilisateur clique sur le bouton de lecture et/ou la lecture automatique est activée) et créez une instance `MediaObject`.

   [API createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType :)

   | Nom de variable | Description | Obligatoire |
   |---|---|---|
   | `name` | Nom de la vidéo | Oui |
   | `mediaid` | Identifiant unique de la vidéo | Oui |
   | `length` | Durée de la vidéo | Oui |
   | `streamType` | Type de diffusion (voir les constantes _StreamType_ ci-dessous) | Oui |
   | `mediaType` | Type de média (voir les constantes _MediaType_ ci-dessous) | Oui |

   **`StreamType`Constantes :**

   | Nom de constante | Description |
   |---|---|
   | `ADBMediaHeartbeatStreamTypeVOD` | Type de diffusion pour la vidéo à la demande. |
   | `ADBMediaHeartbeatStreamTypeLIVE` | Type de diffusion pour le contenu en direct. |
   | `ADBMediaHeartbeatStreamTypeLINEAR` | Type de diffusion pour le contenu linéaire. |
   | `ADBMediaHeartbeatStreamTypeAOD` | Type de diffusion pour l’audio à la demande. |
   | `ADBMediaHeartbeatStreamTypeAUDIOBOOK` | Type de diffusion pour les livres audio. |
   | `ADBMediaHeartbeatStreamTypePODCAST` | Type de diffusion pour les podcasts. |

   **`MediaType`Constantes :**

   | Nom de constante | Description |
   |---|---|
   | `ADBMediaTypeAudio` | Type de média pour les diffusions audio. |
   | `ADBMediaTypeVideo` | Type de média pour les diffusions vidéo. |

   Format général pour la création de `MediaObject` :

   ```
   ADBMediaObject *mediaObject =  
     [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME>
                                          mediaId:<MEDIA_ID>
                                           length:<MEDIA_LENGTH>                       
                                       streamType:<STREAM_TYPE>
                                        mediaType: <MEDIA_TYPE>];
   ```

1. **Ajout de métadonnées vidéo**

   Vous pouvez joindre des objets de métadonnées vidéo standard et/ou personnalisés à la session de suivi vidéo par le biais de variables de données contextuelles.

   * **Métadonnées vidéo standard**

      * [Mise en œuvre de métadonnées standard sur iOS](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **Clés de métadonnées vidéo**

         [Clés de métadonnées iOS](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * Consultez la liste complète des métadonnées vidéo dans la rubrique [Paramètres audio et vidéo](/help/implementation/variables/audio-video-parameters.md).
      >[!NOTE]
      >
      >Il est facultatif de joindre un objet de métadonnées vidéo standard à l’objet multimédia.

   * **Métadonnées personnalisées**

      Créez un objet de variable pour les variables personnalisées et renseignez les données de cette vidéo. Par exemple :

      ```
      NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
      [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
      [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
      ```


1. **Suivi de l’intention de démarrer la lecture**

   Pour commencer le suivi d’une session multimédia, appelez `trackSessionStart` sur l’instance Media Heartbeat.

   >[!TIP]
   >
   >La deuxième valeur est le nom d’objet de métadonnées vidéo personnalisé que vous avez créé à l’étape 2.

   ```
   - (void)onMainVideoLoaded:(NSNotification *)notification {
   //    [_mediaHeartbeat trackSessionStart:mediaObject data:nil];
       [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata];
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` effectue le suivi de l’intention de lecture de l’utilisateur, et non du début de la lecture. Cette API est utilisée pour charger les données/métadonnées de la vidéo et estimer le temps jusqu’au démarrage de la mesure QoS (durée entre `trackSessionStart` et `trackPlay`).

   >[!NOTE]
   >
   >Si vous n’utilisez pas de métadonnées vidéo personnalisées, envoyez simplement un objet vide pour l’argument `data` dans `trackSessionStart`, tel que décrit dans la ligne commentée de l’exemple iOS ci-dessus.

1. **Suivi du début réel de la lecture**

   Identifiez l’événement du lecteur vidéo correspondant au début de la lecture vidéo, où la première image de la vidéo s’affiche à l’écran, et appelez `trackPlay` :

   ```
   - (void)onVideoPlay:(NSNotification *)notification {
       [_mediaHeartbeat trackPlay];
   }
   ```

1. **Suivi de la fin de la lecture**

   Identifiez l’événement du lecteur vidéo correspondant à la fin de la lecture vidéo, où l’utilisateur a visionné le contenu jusqu’à la fin, et appelez `trackComplete` :

   ```
   - (void)onVideoComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackComplete];
   }
   ```

1. **Suivi de la fin de la session**

   Identifiez l’événement du lecteur vidéo correspondant au déchargement/à la fermeture de la lecture vidéo, où l’utilisateur ferme la vidéo et/ou la vidéo est terminée et déchargée, et appelez `trackSessionEnd` :

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification {
       [_mediaHeartbeat trackSessionEnd];
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marque la fin d’une session de suivi vidéo. Si la session a été visionnée jusqu’à la fin, où l’utilisateur a visionné le contenu jusqu’à la fin, assurez-vous que `trackComplete` est appelé avant `trackSessionEnd`. Tout autre appel à l’API `track*` est ignoré après `trackSessionEnd`, sauf `trackSessionStart` dans le cadre d’une nouvelle session de suivi vidéo.

1. **Suivi de tous les scénarios de mise en pause possibles**

   Identifiez l’événement du lecteur vidéo correspondant à l’interruption de la vidéo et appelez `trackPause` :

   ```
   - (void)onVideoPause:(NSNotification *)notification {
       [_mediaHeartbeat trackPause];
   }
   ```

   **Scénarios de mise en pause**

   Identifiez tous les scénarios dans lesquels le lecteur vidéo sera interrompu et assurez-vous que `trackPause` est correctement appelé. Les scénarios suivants exigent tous que votre application appelle `trackPause()` :

   * L’utilisateur appuie délibérément sur pause dans l’application.
   * Le lecteur se met en pause.
   * (*Applications mobiles*) : l’utilisateur place l’application en arrière-plan, mais vous souhaitez que l’application conserve la session ouverte.
   * (*Applications mobiles*) : tout type d’interruption système qui entraîne la mise en arrière-plan d’une application. Par exemple, l’utilisateur reçoit un appel ou une fenêtre contextuelle d’une autre application apparaît, mais vous souhaitez que l’application maintienne la session active afin que l’utilisateur ait l’opportunité de reprendre la vidéo à partir du point d’interruption.

1. Identifiez l’événement du lecteur correspondant à la lecture vidéo et/ou à la reprise vidéo après une interruption et appelez `trackPlay` :

   ```
   - (void)onVideoPlay:(NSNotification *)notification {
       [_mediaHeartbeat trackPlay];
   }
   ```

   >[!TIP]
   >
   >Il peut s’agir de la même source d’événement utilisée à l’étape 4. Assurez-vous que chaque appel de l’API `trackPause()` est suivi d’un appel de l’API `trackPlay()` à la reprise de la lecture vidéo.

Consultez les ressources suivantes pour en savoir plus sur le suivi de la lecture principale :

* Scénarios de suivi : [lecture VOD sans publicité](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Exemple de lecteur inclus dans le SDK iOS pour un exemple de suivi complet
