---
title: Suivi de la qualité de l’expérience sur Chromecast
description: Cette rubrique décrit l’implémentation du suivi de la qualité de l’expérience (QoE, QoS) à l’aide du SDK Media sur Chromecast.
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Suivi de la qualité de l’expérience sur Chromecast{#track-quality-of-experience-on-chromecast}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

## Aperçu {#overview}

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. Vous pouvez utiliser l’API du lecteur multimédia pour identifier les variables liées à la qualité de service et au suivi des erreurs.

## Événements du lecteur {#player-events}

### Sur tous les événements de changement de débit

* Créez/mettez à jour l’instance d’objet QoS pour la lecture, `qosObject`
* L’appel   `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### Erreurs du lecteur

L’appel   `trackError(“media error id”);`

## Mise en œuvre {#implement}

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   **Variables QoSObject :**

   >[!TIP]
   >
   >Ces variables ne sont requises que si vous prévoyez d’effectuer le suivi de la qualité de service.

   | Variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `bitrate` | Débit actuel | Oui |
   | `startupTime` | Temps de démarrage | Oui |
   | `fps` | Valeur fps | Oui |
   | `droppedFrames` | Nombre de pertes d’images | Oui |

   **Création d’objet QoS :** [createQoSObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createQoSObject)

   ```
   qosInfo = ADBMobile.media.createQoSObject(50000, 0, 24, 10); 
   ```

1. Lorsque la lecture change de débit binaire, appelez l’événement `BitrateChange` dans l’instance Media Heartbeat : [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange); 
   ```

   >[!IMPORTANT]
   >
   >Mettez à jour l’objet QoS et appelez l’événement de changement de débit à chaque changement de débit. Ceci produit les données QoS les plus précises.

1. Assurez-vous que la méthode `getQoSObject()` renvoie les informations QoS les plus récentes.
1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (Voir [Aperçu](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Le suivi des erreurs du lecteur multimédia n’arrête pas la session de suivi multimédia. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

