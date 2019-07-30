---
seo-title: Suivi de la qualité de l’expérience sur JavaScript
title: Suivi de la qualité de l’expérience sur JavaScript
uuid: 3 bc 762 a 2-9706-4 b 62-aa 91-747 f 461 dd 13 d
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Suivi de la qualité de l’expérience sur JavaScript{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

## QOS d'implémentation

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   Variables QoSObject :

   >[!TIP]
   >
   >Ces variables ne sont requises que si vous envisagez de suivre qos.

   | Variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `bitrate` | Débit actuel | Oui |
   | `startupTime` | Temps de démarrage | Oui |
   | `fps` | Valeur fps | Oui |
   | `droppedFrames` | Nombre de pertes d’images | Oui |

   Création de l’objet QoS :

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and  
   // <droppeFrames> with the current playback QoS values.  
   var qosObject = MediaHeartbeat.createQoSObject(<bitrate>,  
                                                  <startuptime>,  
                                                  <fps>,  
                                                  <droppedFrames>); 
   ```

1. Lorsque la lecture change de débit binaire, appelez l’événement `BitrateChange` dans l’instance Media Heartbeat :

   ```js
   _onBitrateChange = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
   };
   ```

   >[!IMPORTANT]
   >
   >Mettez à jour l'objet qos et appelez l'événement de changement de débit lors de chaque changement de débit. Ceci produit les données QoS les plus précises.

1. Assurez-vous que la méthode `getQoSObject()` renvoie les informations QoS les plus récentes.
1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (Voir [Aperçu](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Le suivi des erreurs du lecteur multimédia n'arrête pas la session de suivi des médias. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

