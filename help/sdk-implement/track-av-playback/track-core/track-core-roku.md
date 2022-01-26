---
title: 'Découvrez comment effectuer le suivi de la lecture principale sur Roku '
description: Cette rubrique décrit la mise en œuvre du suivi de base à l’aide du SDK Media sur Roku.
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
exl-id: 5272c0ce-4e3d-48c6-bfa6-94066ccbf9ac
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d7cb36c2dd6b35da4531ca975c7fc730e387b750
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 100%

---

# Suivi de la lecture principale sur Roku {#track-core-playback-on-roku}

Cette documentation aborde le suivi dans la version 2.x du SDK.

>[!IMPORTANT]
>Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK](/help/sdk-implement/download-sdks.md).

1. **Configuration initiale du suivi**

   Déterminez le moment où l’utilisateur déclenche l’intention de lecture (l’utilisateur clique sur le bouton de lecture et/ou la lecture automatique est activée) et créez une instance `MediaObject`.

   **`MediaObject`Référence :**

   | Nom de variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom de la vidéo | Oui |
   | `mediaid` | Identifiant unique de la vidéo | Oui |
   | `length` | Durée de la vidéo | Oui |
   | `streamType` | Type de diffusion (voir les constantes _StreamType_ ci-dessous) | Oui |
   | `mediaType` | Type de média (voir les constantes _MediaType_ ci-dessous) | Oui |

   **`StreamType`Constantes :**

   | Nom de constante | Description   |
   |---|---|
   | `MEDIA_STREAM_TYPE_VOD` | Type de diffusion pour la vidéo à la demande. |
   | `MEDIA_STREAM_TYPE_LIVE` | Type de diffusion pour le contenu en direct. |
   | `MEDIA_STREAM_TYPE_LINEAR` | Type de diffusion pour le contenu linéaire. |
   | `MEDIA_STREAM_TYPE_AOD` | Type de diffusion pour l’audio à la demande. |
   | `MEDIA_STREAM_TYPE_AUDIOBOOK` | Type de diffusion pour les livres audio. |
   | `MEDIA_STREAM_TYPE_PODCAST` | Type de diffusion pour les podcasts. |

   **`MediaType`Constantes :**

   | Nom de constante | Description |
   |---|---|
   | `MEDIA_STREAM_TYPE_AUDIO` | Type de média pour les diffusions audio. |
   | `MEDIA_STREAM_TYPE_VIDEO` | Type de média pour les diffusions vidéo. |

   **Créez un objet d’informations sur le média pour une vidéo avec du contenu VOD :**

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

   **Créez un objet d’informations sur le média pour une vidéo avec du contenu AOD :**

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

   Vous pouvez joindre des métadonnées standard et/ou de publicité à la session de suivi par le biais de variables de données contextuelles.

   * **Métadonnées standard**

[Mise en œuvre de métadonnées standard sur Roku ](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

      >[!NOTE]
      >Il est facultatif de joindre un objet de métadonnées vidéo standard à l’objet multimédia.

   * **Métadonnées personnalisées**

      Créez un objet de variable pour les variables personnalisées et renseignez les données de cette vidéo. Par exemple :

      ```
      mediaContextData = {}
      mediaContextData["cmk1"] = "cmv1"
      mediaContextData["cmk2"] = "cmv2"
      ```

1. **Suivi de l’intention de démarrer la lecture**

   Pour commencer le suivi d’une session multimédia, appelez `trackSessionStart` sur l’instance Media Heartbeat :

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >La deuxième valeur est le nom d’objet de métadonnées vidéo personnalisé que vous avez créé à l’étape 2.

   >[!IMPORTANT]
   >`trackSessionStart` effectue le suivi de l’intention de lecture de l’utilisateur, et non du début de la lecture. Cette API est utilisée pour charger les données/métadonnées de la vidéo et estimer le temps jusqu’au démarrage de la mesure QoS (durée entre `trackSessionStart` et `trackPlay`).

   >[!NOTE]
   >Si vous n’utilisez pas de métadonnées vidéo personnalisées, envoyez simplement un objet vide pour l’argument `data` dans `trackSessionStart`, tel que décrit dans la ligne commentée de l’exemple iOS ci-dessus.

1. **Suivi du début réel de la lecture**

   Identifiez l’événement du lecteur vidéo correspondant au début de la lecture vidéo, où la première image de la vidéo s’affiche à l’écran, et appelez `trackPlay` :

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **Mise à jour de la valeur de la tête de lecture**

   Lorsque la tête de lecture du média se déplace, informez le SDK en appelant lʼAPI `mediaUpdatePlayhead`. Pour les vidéos à la demande (VOD), la valeur est indiquée en secondes à partir du début de lʼélément média. Pour les vidéos en flux continu, la valeur est spécifiée comme le nombre de secondes écoulées depuis minuit UTC ce jour-là.

   ```
   ADBMobile().mediaUpdatePlayhead(position)
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
   >`trackSessionEnd` marque la fin d’une session de suivi vidéo. Si la session a été visionnée jusqu’à la fin, où l’utilisateur a visionné le contenu jusqu’à la fin, assurez-vous que `trackComplete` est appelé avant `trackSessionEnd`. Tout autre appel à l’API `track*` est ignoré après `trackSessionEnd`, sauf `trackSessionStart` dans le cadre d’une nouvelle session de suivi vidéo.

1. **Suivi de tous les scénarios de mise en pause possibles**

   Identifiez l’événement du lecteur vidéo correspondant à l’interruption de la vidéo et appelez `trackPause` :

   ```
   ADBMobile().mediaTrackPause()
   ```

   **Scénarios de mise en pause**

   Identifiez tous les scénarios dans lesquels le lecteur vidéo sera interrompu et assurez-vous que `trackPause` est correctement appelé. Les scénarios suivants exigent tous que votre application appelle `trackPause()` :

   * L’utilisateur appuie délibérément sur pause dans l’application.
   * Le lecteur se met en pause.
   * (*Applications mobiles*) : l’utilisateur place l’application en arrière-plan, mais vous souhaitez que l’application conserve la session ouverte.
   * (*Applications mobiles*) : tout type d’interruption système qui entraîne la mise en arrière-plan d’une application. Par exemple, l’utilisateur reçoit un appel ou une fenêtre contextuelle d’une autre application apparaît, mais vous souhaitez que l’application maintienne la session active afin que l’utilisateur ait l’opportunité de reprendre la vidéo à partir du point d’interruption.

1. Identifiez l’événement du lecteur correspondant à la lecture vidéo et/ou à la reprise vidéo après une interruption et appelez `trackPlay` :

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >Il peut s’agir de la même source d’événement utilisée à l’étape 4. Assurez-vous que chaque appel de l’API `trackPause()` est suivi d’un appel de l’API `trackPlay()` à la reprise de la lecture vidéo.

* Scénarios de suivi : [lecture VOD sans publicité](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Exemple de lecteur inclus dans le SDK Roku pour un exemple de suivi complet
