---
seo-title: Suivi de la qualité de l’expérience sur iOS
title: Suivi de la qualité de l’expérience sur iOS
uuid: cae2c142-ed39-4234-a711-765dcabc5415
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Suivi de la qualité de l’expérience sur iOS{#track-quality-of-experience-on-ios}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

## Implemement QOS

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   Variables QoSObject :

   | Variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `bitrate` | Débit actuel | Oui |
   | `startupTime` | Temps de démarrage | Oui |
   | `fps` | Valeur fps | Oui |
   | `droppedFrames` | Nombre de pertes d’images | Oui |

   >[!TIP]
   >
   >Ces variables ne sont requises que si vous prévoyez d’effectuer le suivi de la qualité de service.

   Création de l’objet QoS :

   ```
   id qosObject = [ADBMediaHeartbeat createQoSObjectWithBitrate:[BITRATE] 
                                     startupTime:[STARTUP_TIME]  
                                     fps:[FPS]  
                                     droppedFrames:[DROPPED_FRAMES]];
   ```

1. Assurez-vous que la méthode `getQoSObject` renvoie les informations QoS les plus récentes.
1. Lorsque la lecture change de débit binaire, appelez l’événement `BitrateChange` dans l’instance Media Heartbeat :

   ```
   - (void)onBitrateChange:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBitrateChange  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

   >[!IMPORTANT]
   >
   >Update the QoS object and call the bitrate change event on every bitrate change. Ceci produit les données QoS les plus précises.

