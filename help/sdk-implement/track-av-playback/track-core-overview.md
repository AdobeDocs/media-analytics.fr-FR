---
seo-title: Tracking Overview
title: Tracking Overview
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# Tracking Overview{#tracking-overview}

>[!IMPORTANT]
>
>This documentation covers tracking in version 2.x of the SDK. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

## Player Events

Le suivi de la lecture principale inclut le suivi du chargement du média, du démarrage du média, de la mise en pause du média et de la fin du média. Bien qu’il ne soit pas obligatoire, le suivi de la mise en mémoire tampon et de la recherche est également un composant principal du suivi de la lecture du contenu. Dans l’API de votre lecteur multimédia, identifiez les événements du lecteur qui correspondant aux appels de suivi du SDK Media, et codez vos gestionnaires d’événements pour appeler les API de suivi et renseigner les variables obligatoires et facultatives.

### On media load

* Créez l’objet multimédia.
* Renseignez les métadonnées.
* Call ; For example: `trackSessionStart``trackSessionStart(mediaObject, contextData)`

### On media start

* L’appel   `trackPlay`

### En pause/reprise

* L’appel   `trackPause`
* Call `trackPlay`   _when playback resumes_

### Sur le média terminé

* L’appel   `trackComplete`

### Abandon du média

* L’appel   `trackSessionEnd`

### Au démarrage du défilement

* L’appel   `trackEvent(SeekStart)`

### A l’issue du défilement

* L’appel   `trackEvent(SeekComplete)`

### Lorsque la mise en mémoire tampon commence

* L’appel   `trackEvent(BufferStart);`

### À la fin de la mise en mémoire tampon

* L’appel   `trackEvent(BufferComplete);`

>[!TIP]
>
>La position du curseur de lecture est définie dans le cadre du code de configuration et de configuration. For more information about , see Overview: General Implementation Guidelines.`getCurrentPlayheadTime`[](/help/sdk-implement/setup/setup-overview.md#section_965A3B699A8248DDB9B2B3EA3CC20E41)

## Mise en œuvre {#section_BB217BE6585D4EDEB34C198559575004}

1. **Installation initiale du suivi :** Déterminez le moment où l’utilisateur déclenche l’intention de lecture (l’utilisateur clique sur lecture et/ou la lecture automatique est activée) et créez une instance `MediaObject` à l’aide des informations sur le média pour le nom du contenu, l’ID de contenu, la durée du contenu et le type de diffusion.

   **`MediaObject`référence :**

   | Nom de variable | Description | Obligatoire |
   |---|---|---|
   | `name` | Nom du contenu | Oui |
   | `mediaid` | Identifiant unique du contenu | Oui |
   | `length` | Durée du contenu | Oui |
   | `streamType` | Type de diffusion | Oui |
   | `mediaType` | Type de média (contenu audio ou vidéo) | Oui |

   **`StreamType`constantes :**

   | Nom de constante | Description |
   |---|---|
   | `VOD` | Type de diffusion pour la vidéo à la demande. |
   | `LIVE` | Type de diffusion pour le contenu en direct. |
   | `LINEAR` | Type de diffusion pour le contenu linéaire. |
   | `AOD` | Type de diffusion pour l’audio à la demande. |
   | `AUDIOBOOK` | Type de diffusion pour les livres audio. |
   | `PODCAST` | Type de diffusion pour les podcasts. |

   **`MediaType`constants:**

   | Nom de constante | Description |
   |---|---|
   | `Audio` | Type de média pour les diffusions audio. |
   | `Video` | Type de média pour les diffusions vidéo. |

   The general format for creating the `MediaObject` is `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **Joindre des métadonnées -** Vous pouvez joindre des métadonnées standard et/ou de publicité à la session de suivi par le biais de variables de données contextuelles.

   * **Métadonnées standard -**

      >[!NOTE]
      >
      >L’association de l’objet de métadonnées standard à l’objet multimédia est facultative.

      Instanciez un objet de métadonnées standard, renseignez les variables désirées et définissez l’objet de métadonnées sur l’objet Media Heartbeat.

      See the comprehensive list of metadata here: [Audio and video parameters.](/help/metrics-and-metadata/audio-video-parameters.md)

   * **Métadonnées personnalisées -** Créez un objet de variable pour les variables personnalisées et renseignez les données de ce contenu.

1. **Suivi de l’intention de démarrer la lecture -** Pour commencer le suivi d’une session, appelez `trackSessionStart` sur l’instance Media Heartbeat.

   >[!IMPORTANT]
   >
   >`trackSessionStart` effectue le suivi de l’intention de lecture de l’utilisateur, et non du début de la lecture. Cette API est utilisée pour charger les données/métadonnées et estimer le temps jusqu’au démarrage de la mesure QoS (durée entre `trackSessionStart` et `trackPlay`).

   >[!NOTE]
   >
   >If you are not using custom metadata, simply send an empty object for the `data` argument in `trackSessionStart`.

1. **Suivi du début effectif de la lecture -** Identifiez l’événement du lecteur multimédia correspondant au début de la lecture (la première image du contenu s’affiche à l’écran) et appelez `trackPlay`.

1. **Suivi de la fin de la lecture -** Identifiez l’événement du lecteur multimédia correspondant à la fin de la lecture, où l’utilisateur a visionné le contenu jusqu’à la fin, et appelez `trackComplete`.

1. **Suivi de la fin de la session -** Identifiez l’événement du lecteur multimédia correspondant au déchargement/à la fermeture de la lecture (l’utilisateur ferme le contenu et/ou le contenu est terminé et déchargé) et appelez `trackSessionEnd`.

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marks the end of a tracking session. Si la session a été visionnée jusqu’à la fin, où l’utilisateur a visionné le contenu jusqu’à la fin, assurez-vous que `trackComplete` est appelé avant `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.

1. **Suivi de tous les scénarios de mise en pause possibles -** Identifiez l’événement du lecteur multimédia qui provoque la pause et appelez `trackPause`.

   **Scénarios de pause :** Identifiez tous les scénarios dans lesquels le lecteur sera interrompu et assurez-vous que `trackPause` est correctement appelé. Les scénarios suivants exigent tous que votre application appelle `trackPause()`:

   * L’utilisateur appuie explicitement sur le bouton de pause dans l’application.
   * Le lecteur se place dans l’état de pause.
   * (*Applications mobiles*) - L’utilisateur place l’application en arrière-plan, mais vous souhaitez que l’application maintienne la session ouverte.
   * (*Applications mobiles*) - Tout type d’interruption système qui entraîne la mise en arrière-plan d’une application. Par exemple, l’utilisateur reçoit un appel ou une fenêtre contextuelle d’une autre application apparaît, mais vous souhaitez que l’application maintienne la session active afin que l’utilisateur ait l’opportunité de reprendre le contenu à partir du point d’interruption.

1. Identifiez l’événement du lecteur correspondant à la lecture et/ou à la reprise après une interruption et appelez `trackPlay`.

   >[!TIP]
   >
   >Il peut s’agir de la même source d’événement utilisée à l’étape 4. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the playback resumes.

1. Prêtez attention aux événements de recherche de la lecture se produisant dans le lecteur multimédia. Une fois que vous avez reçu la notification de début de la recherche, effectuez-en le suivi à l’aide de l’événement `SeekStart`.
1. Une fois que vous avez reçu la notification de fin de la recherche, effectuez-en le suivi à l’aide de l’événement `SeekComplete`.
1. Prêtez attention aux événements de mise en mémoire tampon de la lecture se produisant dans le lecteur multimédia. Une fois que vous avez reçu la notification de début de la mise en mémoire tampon, effectuez-en le suivi à l’aide de l’événement `BufferStart`.
1. Une fois que vous avez reçu la notification de fin de la mise en mémoire tampon, effectuez-en le suivi à l’aide de l’événement `BufferComplete`.

Consultez des exemples de chaque étape dans les rubriques suivantes spécifiques aux plates-formes, et examinez les exemples de lecteurs inclus dans vos SDK.

Voici un exemple simple de suivi de lecture à l’aide du SDK JavaScript 2.x dans un lecteur HTML5 :

```js
/* Call on media start */ 
if (e.type == "play") { 
 
    // Check for start of media 
    if (!sessionStarted) { 
        /* Set media info */     
        /* MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                            <MEDIA_ID>,  
                                            <MEDIA_LENGTH>, 
                                            <MEDIA_STREAMTYPE>,
                                            <MEDIA_MEDIATYPE>);*/ 
        var mediaInfo = MediaHeartbeat.createMediaObject( 
          document.getElementsByTagName('video')[0].getAttribute("name"),  
          document.getElementsByTagName('video')[0].getAttribute("id"),  
          video.duration, 
          MediaHeartbeat.StreamType.VOD); 
 
        /* Set custom context data */ 
        var customVideoMetadata = { 
            isUserLoggedIn: "false", 
            tvStation: "Sample TV station", 
            programmer: "Sample programmer" 
        }; 
 
        /* Set standard video metadata */     
        var standardVideoMetadata = {}; 
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode"; 
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show"; 
        mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,  
                           standardVideoMetadata);     
 
        // Start Session 
        this.mediaHeartbeat.trackSessionStart(mediaInfo, customVideoMetadata);    
 
        // Track play 
        this.mediaHeartbeat.trackPlay();  
        sessionStarted = true;     
 
    } else { 
        // Track play for resuming playack    
        this.mediaHeartbeat.trackPlay();  
    } 
}; 
 
/* Call on video complete */ 
if (e.type == "ended") { 
    console.log("video ended"); 
    this.mediaHeartbeat.trackComplete(); 
    this.mediaHeartbeat.trackSessionEnd(); 
    sessionStarted = false;     
}; 
 
/* Call on pause */ 
if (e.type == "pause") { 
    this.mediaHeartbeat.trackPause(); 
}; 
 
/* Call on scrub start */ 
if (e.type == "seeking") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
}; 
     
/* Call on scrub stop */ 
if (e.type == "seeked") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
}; 
 
/* Call on buffer start */ 
if (e.type == “buffering”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
}; 
 
/* Call on buffer complete */ 
if (e.type == “buffered”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
};
```

## Validation {#section_ABCFB92C587B4CAABDACF93452EFA78F}

For information on validating your implementation, see Validation.[](/help/sdk-implement/validation/validation-overview.md)

