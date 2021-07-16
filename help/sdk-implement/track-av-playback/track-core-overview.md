---
title: Explication du suivi de la lecture du contenu
description: '"Découvrez le suivi de la lecture principale, y compris le suivi du chargement du média, du démarrage du média, de la mise en pause du média et de la fin du média. "'
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 97%

---

# Présentation du suivi{#tracking-overview}

Cette documentation aborde le suivi dans la version 2.x du SDK.

>[!IMPORTANT]
>
>Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

## Événements du lecteur

Le suivi de la lecture principale comprend le suivi du chargement du média, du démarrage du média, de la mise en pause du média et de la fin du média. Bien que non obligatoire, la mise en mémoire tampon du suivi et la recherche sont également des composants essentiels du suivi de la lecture du contenu. Dans l’API de votre lecteur multimédia, identifiez les événements du lecteur correspondant aux appels de suivi du SDK Media, et codez vos gestionnaires d’événements pour appeler les API de suivi et renseigner les variables obligatoires et facultatives.

### Au chargement du média

* Créez l’objet multimédia
* Renseignez les métadonnées
* Appelez `trackSessionStart` ; Par exemple : `trackSessionStart(mediaObject, contextData)`

### Au démarrage du média

* Appelez `trackPlay`

### À la mise en pause/reprise

* Appelez `trackPause`
* Appelez `trackPlay`   _lorsque la lecture reprend_

### À la fin du média

* Appelez `trackComplete`

### À l’abandon du média

* Appelez `trackSessionEnd`

### Au début du défilement

* Appelez `trackEvent(SeekStart)`

### À la fin du défilement

* Appelez `trackEvent(SeekComplete)`

### Au début de la mise en mémoire tampon

* Appelez `trackEvent(BufferStart);`

### À la fin de la mise en mémoire tampon

* Appelez `trackEvent(BufferComplete);`

>[!TIP]
>
>La position du curseur de lecture est définie dans le cadre du code d’installation et de configuration. Pour plus d’informations sur `getCurrentPlayheadTime`, voir [Présentation : Instructions générales de mise en œuvre.](/help/sdk-implement/setup/setup-overview.md#general-implementation-guidelines)

## Mise en œuvre {#implement}

1. **Installation initiale du suivi :** Déterminez le moment où l’utilisateur déclenche l’intention de lecture (l’utilisateur clique sur lecture et/ou la lecture automatique est activée) et créez une instance `MediaObject` à l’aide des informations sur le média pour le nom du contenu, l’ID de contenu, la durée du contenu et le type de diffusion.

   **`MediaObject`Référence :**

   | Nom de variable | Description | Obligatoire |
   |---|---|---|
   | `name` | Nom du contenu | Oui |
   | `mediaid` | Identifiant unique du contenu | Oui |
   | `length` | Durée du contenu | Oui |
   | `streamType` | Type de diffusion | Oui |
   | `mediaType` | Type de média (contenu audio ou vidéo) | Oui |

   **`StreamType`Constantes :**

   | Nom de constante | Description |
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

   Le format général pour la création de `MediaObject` est `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **Joindre des métadonnées -** vous pouvez joindre des métadonnées standard et/ou de publicité à la session de suivi par le biais de variables de données contextuelles.

   * **Métadonnées standard -**

      >[!NOTE]
      >
      >Il est facultatif de joindre un objet de métadonnées standard à l’objet multimédia.

      Instanciez un objet de métadonnées standard, renseignez les variables désirées et définissez l’objet de métadonnées sur l’objet Media Heartbeat.

      Consultez la liste complète des métadonnées dans la rubrique [Paramètres audio et vidéo](/help/metrics-and-metadata/audio-video-parameters.md).

   * **Métadonnées personnalisées -** Créez un objet de variable pour les variables personnalisées et renseignez les données de ce contenu.

1. **Suivi de l’intention de démarrer la lecture -** Pour commencer le suivi d’une session, appelez `trackSessionStart` sur l’instance Media Heartbeat.

   >[!IMPORTANT]
   >
   >`trackSessionStart` effectue le suivi de l’intention de lecture de l’utilisateur, et non du début de la lecture. Cette API est utilisée pour charger les données/métadonnées et estimer le temps jusqu’au démarrage de la mesure QoS (durée entre `trackSessionStart` et `trackPlay`).

   >[!NOTE]
   >
   >Si vous n’utilisez pas de métadonnées personnalisées, envoyez simplement un objet vide pour l’argument `data` dans `trackSessionStart`.

1. **Suivi du début effectif de la lecture -** Identifiez l’événement du lecteur multimédia correspondant au début de la lecture (la première image du contenu s’affiche à l’écran) et appelez `trackPlay`.

1. **Suivi de la fin de la lecture -** Identifiez l’événement du lecteur multimédia correspondant à la fin de la lecture, où l’utilisateur a visionné le contenu jusqu’à la fin, et appelez `trackComplete`.

1. **Suivi de la fin de la session -** Identifiez l’événement du lecteur multimédia correspondant au déchargement/à la fermeture de la lecture (l’utilisateur ferme le contenu et/ou le contenu est terminé et déchargé) et appelez `trackSessionEnd`.

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marque la fin d’une session de suivi. Si la session a été visionnée jusqu’à la fin, où l’utilisateur a visionné le contenu jusqu’à la fin, assurez-vous que `trackComplete` est appelé avant `trackSessionEnd`. Tout autre appel à l’API `track*` est ignoré après `trackSessionEnd`, sauf `trackSessionStart` dans le cadre d’une nouvelle session de suivi.

1. **Suivi de tous les scénarios de mise en pause possibles -** Identifiez l’événement du lecteur multimédia qui provoque la pause et appelez `trackPause`.

   **Scénarios de pause -** Identifiez tous les scénarios dans lesquels le lecteur sera interrompu et assurez-vous que `trackPause` est correctement appelé. Les scénarios suivants exigent tous que votre application appelle `trackPause()` :

   * L’utilisateur appuie délibérément sur pause dans l’application.
   * Le lecteur se met en pause.
   * (*Applications mobiles*) : l’utilisateur place l’application en arrière-plan, mais vous souhaitez que l’application conserve la session ouverte.
   * (*Applications mobiles*) : tout type d’interruption système qui entraîne la mise en arrière-plan d’une application. Par exemple, l’utilisateur reçoit un appel ou une fenêtre contextuelle provenant d’une autre application s’ouvre, mais vous souhaitez que l’application conserve la session ouverte pour donner à l’utilisateur la possibilité de reprendre le contenu à partir du point d’interruption.

1. Identifiez l’événement du lecteur correspondant à la lecture et/ou à la reprise après une interruption et appelez `trackPlay`.

   >[!TIP]
   >
   >Il peut s’agir de la même source d’événement utilisée à l’étape 4. Assurez-vous que chaque appel de l’API `trackPause()` est suivi d’un appel de l’API `trackPlay()` à la reprise de la lecture.

1. Prêtez attention aux événements de recherche de la lecture se produisant dans le lecteur multimédia. Une fois que vous avez reçu la notification de début de la recherche, effectuez-en le suivi à l’aide de l’événement `SeekStart`.
1. Une fois que vous avez reçu la notification de fin de la recherche, effectuez-en le suivi à l’aide de l’événement `SeekComplete`.
1. Prêtez attention aux événements de mise en mémoire tampon de la lecture se produisant dans le lecteur multimédia. Une fois que vous avez reçu la notification de début de la mise en mémoire tampon, effectuez-en le suivi à l’aide de l’événement `BufferStart`.
1. Une fois que vous avez reçu la notification de fin de la mise en mémoire tampon, effectuez-en le suivi à l’aide de l’événement `BufferComplete`.

Consultez des exemples de chaque étape dans les rubriques suivantes spécifiques aux plateformes, et examinez les exemples de lecteurs inclus dans vos SDK.

Voici un exemple simple de suivi de lecture à l’aide du SDK JavaScript 2.x dans un lecteur HTML5 :

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

## Validation {#validate}

Pour plus d’informations sur la validation de votre mise en œuvre, voir [Validation.](/help/sdk-implement/validation/validation-overview.md)
