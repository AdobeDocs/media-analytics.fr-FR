---
title: Découvrez comment effectuer le suivi de la lecture principale sur Chromecast
description: Découvrez comment implémenter le suivi principal à l’aide du SDK Media sur Chromecast.
uuid: a9fc59d8-a2f4-4889-bdec-55c42a835d06
exl-id: 9812d06d-9efd-460c-a626-6a15f61a4c35
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 88%

---

# Suivre la lecture principale sur Chromecast {#track-core-playback-on-chromecast}

Cette documentation aborde le suivi dans la version 2.x du SDK.

>[!IMPORTANT]
>
>Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK](/help/getting-started/download-sdks.md).

1. **Configuration initiale du suivi**

   Déterminez le moment où l’utilisateur déclenche l’intention de lecture (l’utilisateur clique sur le bouton de lecture et/ou la lecture automatique est activée) et créez une instance `MediaObject`.

   **`MediaObject`Référence d’API :**

   [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

   ```
   mediaObject = ADBMobile.media.createMediaObject(<name>, <id>, <duration>, <streamType>, <mediaType>);
   ```

   **`StreamType`Constantes :**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.StreamType)

   **`MediaType`Constantes :**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.MediaType)

1. **Ajout de métadonnées vidéo**

   Vous pouvez joindre des objets de métadonnées vidéo standard et/ou personnalisés à la session de suivi vidéo par le biais de variables de données contextuelles.

   * **Métadonnées vidéo standard**

     [Mise en œuvre de métadonnées standard sur Chromecast](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)

     >[!NOTE]
     >
     >Il est facultatif de joindre un objet de métadonnées vidéo standard à l’objet multimédia.

   * **Métadonnées personnalisées**

     Créez un objet de variable pour les variables personnalisées et renseignez les données de cette vidéo. Par exemple :

     ```js
     /* Set custom context data */
     var customVideoMetadata = {
         isUserLoggedIn: "false",
         tvStation: "Sample TV station",
         programmer: "Sample programmer"
     };
     ```

1. **Suivi de l’intention de démarrer la lecture**

   Pour commencer le suivi d’une session multimédia, appelez [trackSessionStart](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionStart) sur l’objet `media`.

   ```
   ADBMobile.media.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` effectue le suivi de l’intention de lecture de l’utilisateur, et non du début de la lecture. Cette API est utilisée pour charger les données/métadonnées de la vidéo et estimer le temps jusqu’au démarrage de la mesure QoS (durée entre `trackSessionStart` et `trackPlay`).

   >[!NOTE]
   >
   >La deuxième valeur est le nom d’objet de métadonnées vidéo personnalisé que vous avez créé à l’étape 2. Si vous n’utilisez pas de métadonnées vidéo personnalisées, envoyez simplement un objet vide pour l’argument `data` dans `trackSessionStart`, tel que décrit dans la ligne commentée de l’exemple iOS ci-dessus.

1. **Suivi du début réel de la lecture**

   Identifiez l’événement du lecteur vidéo correspondant au début de la lecture vidéo, où la première image de la vidéo s’affiche à l’écran, et appelez [trackPlay](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPlay) :

   ```
   ADBMobile.media.trackPlay();
   ```

1. **Mettre à jour la valeur du curseur de lecture**

   Mettez à jour la valeur de la position du `mediaUpdatePlayhead` plusieurs fois lorsque le curseur de lecture change. <br /> Pour les vidéos à la demande (VOD), la valeur est indiquée en secondes à partir du début de lʼélément média. <br /> Pour la diffusion en direct, si le lecteur ne fournit pas d’informations sur la durée du contenu, la valeur peut être spécifiée comme le nombre de secondes écoulées depuis minuit UTC de ce jour.

   ```
   ADBMobile().media.updatePlayhead(position)
   ```

   >[!NOTE]
   >
   >Tenez compte des points suivants lors de l’appel de l’API `media.updatePlayhead` :
   >* Lors de l’utilisation de marques de progression, la durée du contenu est une donnée obligatoire et le curseur de lecture doit être mis à jour en tant que nombre de secondes écoulées depuis le début de l’élément média, en commençant par 0.
   >* Lors de l’utilisation de SDK Media, vous devez appeler l’API `media.updatePlayhead` au moins une fois par seconde.

1. **Suivi de la fin de la lecture**

   Identifiez l’événement du lecteur vidéo correspondant à la fin de la lecture vidéo, où l’utilisateur a visionné le contenu jusqu’à la fin, et appelez [trackComplete](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete) :

   ```
   ADBMobile.media.trackComplete();
   ```

1. **Suivi de la fin de la session**

   Identifiez l’événement du lecteur vidéo correspondant au déchargement/à la fermeture de la lecture vidéo, où l’utilisateur ferme la vidéo et/ou la vidéo est terminée et déchargée, et appelez [trackSessionEnd](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionEnd) :

   ```
   ADBMobile.media.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marque la fin d’une session de suivi vidéo. Si la session a été visionnée jusqu’à la fin, où l’utilisateur a visionné le contenu jusqu’à la fin, assurez-vous que `trackComplete` est appelé avant `trackSessionEnd`. Tout autre appel à l’API `track*` est ignoré après `trackSessionEnd`, sauf `trackSessionStart` dans le cadre d’une nouvelle session de suivi vidéo.

1. **Suivi de tous les scénarios de mise en pause possibles**

   Identifiez l’événement du lecteur vidéo correspondant à l’interruption de la vidéo et appelez [trackPause:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPause)

   ```
   ADBMobile.media.trackPause();
   ```

   **Scénarios de mise en pause**

   Identifiez tous les scénarios dans lesquels le lecteur vidéo sera interrompu et assurez-vous que `trackPause` est correctement appelé. Les scénarios suivants exigent tous que votre application appelle `trackPause()` :

   * L’utilisateur appuie délibérément sur pause dans l’application.
   * Le lecteur se met en pause.
   * (*Applications mobiles*) : l’utilisateur place l’application en arrière-plan, mais vous souhaitez que l’application conserve la session ouverte.
   * (*Applications mobiles*) : tout type d’interruption système qui entraîne la mise en arrière-plan d’une application. Par exemple, l’utilisateur reçoit un appel ou une fenêtre contextuelle d’une autre application apparaît, mais vous souhaitez que l’application maintienne la session active afin que l’utilisateur ait l’opportunité de reprendre la vidéo à partir du point d’interruption.

1. Identifiez l’événement du lecteur correspondant à la lecture vidéo et/ou à la reprise vidéo après une interruption et appelez [trackPlay](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete) :

   ```
   ADBMobile.media.trackPlay();
   ```

   >[!TIP]
   >
   >Il peut s’agir de la même source d’événement utilisée à l’étape 4. Assurez-vous que chaque appel de l’API `trackPause()` est suivi d’un appel de l’API `trackPlay()` à la reprise de la lecture vidéo.

* Scénarios de suivi : [lecture VOD sans publicité](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Exemple de lecteur inclus dans le SDK Chromecast pour un exemple de suivi complet
