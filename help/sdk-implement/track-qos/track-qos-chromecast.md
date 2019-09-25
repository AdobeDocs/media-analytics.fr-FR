---
seo-title: Suivi de la qualité de l’expérience sur Chromecast
title: Suivi de la qualité de l’expérience sur Chromecast
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Suivi de la qualité de l’expérience sur Chromecast{#track-quality-of-experience-on-chromecast}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

## Aperçu {#section_DDB8DFA47C5744AB9A04392AD5959BF7}

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. Vous pouvez utiliser l’API du lecteur multimédia pour identifier les variables liées à la qualité de service et au suivi des erreurs.

## Événements du lecteur {#player-events}

### Sur tous les événements de changement de débit

* Créez/mettez à jour l’instance d’objet QoS pour la lecture, `qosObject`
* L’appel   `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### Erreurs du lecteur

L’appel   `trackError(“media error id”);`

## Mise en œuvre {#section_3B8EBEB167624D0481E8AF4761F83047}

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
   >Update the QoS object and call the bitrate change event on every bitrate change. Ceci produit les données QoS les plus précises.

1. Assurez-vous que la méthode `getQoSObject()` renvoie les informations QoS les plus récentes.
1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (Voir [Aperçu](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Tracking media player errors will not stop the media tracking session. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

