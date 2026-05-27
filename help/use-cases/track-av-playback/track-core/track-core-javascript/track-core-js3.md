---
title: Découvrez comment effectuer le suivi de la lecture principale à lʼaide de JavaScript v3.x
description: Découvrez comment mettre en œuvre le suivi principal à lʼaide du SDK Media dans un navigateur à lʼaide des applications JavaScript 3.x.
exl-id: f3145450-82ba-4790-91a4-9d2cc97bbaa5
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/bIOfr94Q7wJLH9LfRg9VLIEJuS6JPvcgSWS62YCVguc
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 759
ht-degree: 85%

---

# Effectuer le suivi de la lecture principale à l’aide de JavaScript 3.x{#track-core-playback-on-javascript}

Cette documentation aborde le suivi dans la version 3.x du SDK.

>[!IMPORTANT]
>
>Si vous mettez en œuvre une version précédente du kit SDK, vous pouvez télécharger les Guides du développeur dans la rubrique [Téléchargement des SDK](/help/getting-started/download-sdks.md)

1. **Configuration initiale du suivi**

   Déterminez le moment où l’utilisateur déclenche l’intention de lecture (l’utilisateur clique sur le bouton de lecture et/ou la lecture automatique est activée) et créez une instance `MediaObject`.

   [API createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Nom de variable | Type | Description |
   | --- | --- | --- |
   | `name` | string | Chaîne non vide désignant le nom du média. |
   | `id` | string | Chaîne non vide désignant l’identifiant de média unique. |
   | `length` | number | Nombre positif désignant la longueur du média en secondes. Indiquez 0 si la longueur est inconnue. |
   | `streamType` | string |   |
   | `mediaType` | | Type de média (audio ou vidéo). |

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

   Vous pouvez joindre des métadonnées standard et/ou personnalisées à la session de suivi par le biais de variables de données contextuelles.

   * **Métadonnées standard**

     >[!NOTE]
     >
     >Il est facultatif de joindre les métadonnées standard.

      * Référence à l’API des clés de métadonnées multimédia - [Clés de métadonnées standard - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

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
   >Si vous n’utilisez pas de données contextuelles, envoyez simplement un objet vide pour l’argument `data` dans `trackSessionStart`.

1. **Suivi du début réel de la lecture**

   Identifiez l’événement du lecteur multimédia correspondant au début de la lecture, où la première image du média s’affiche à l’écran, et appelez `trackPlay` :

   ```js
   tracker.trackPlay();
   ```

1. **Mettre à jour la valeur du curseur de lecture**

   Lorsque le curseur de lecture du média change, avertissez le SDK en appelant l’API `mediaUpdatePlayhead`. <br /> Pour la vidéo à la demande (VOD), la valeur est spécifiée en secondes à partir du début de l’élément média. <br /> Pour la diffusion en direct, si le lecteur ne fournit pas d’informations sur la durée du contenu, la valeur peut être spécifiée comme le nombre de secondes écoulées depuis minuit UTC de ce jour.

   ```
   tracker.updatePlayhead(position)
   ```

   >[!NOTE]
   >
   >Tenez compte des points suivants lors de l’appel de l’API `tracker.updatePlayhead` :
   >* Lors de l’utilisation de marques de progression, la durée du contenu est une donnée obligatoire et le curseur de lecture doit être mis à jour en tant que nombre de secondes écoulées depuis le début de l’élément média, en commençant par 0.
   >* Lors de l’utilisation de SDK Media, vous devez appeler l’API `tracker.updatePlayhead` au moins une fois par seconde.

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

* Scénarios de suivi : [lecture VOD sans publicité](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Exemple de lecteur inclus avec le SDK JavaScript pour un exemple de suivi complet.
