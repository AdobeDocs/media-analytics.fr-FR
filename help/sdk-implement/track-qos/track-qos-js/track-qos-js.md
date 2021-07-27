---
title: Découvrez comment effectuer le suivi de la qualité de lʼexpérience à lʼaide de JavaScript 2.x
description: « Découvrez comment mettre en œuvre le suivi de la qualité de lʼexpérience (QoE, QoS) à lʼaide du SDK Media dans les applications de navigateur avec JavaScript 2.x. »
uuid: 3bc762a2-9706-4b62-aa91-747f461dd13d
exl-id: 5924eba4-15a9-405b-9a05-8a7308ddec47
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: ht
source-wordcount: '222'
ht-degree: 100%

---

# Suivi de la qualité de l’expérience à l’aide de JavaScript 2.x{#track-quality-of-experience-on-javascript}

Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x.

>[!IMPORTANT]
>
>Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

## Mise en œuvre de QoS

1. Identifiez le moment où le débit binaire change pendant la lecture multimédia et créez l’instance `MediaObject` à l’aide des informations QoS.

   Variables QoSObject :

   >[!TIP]
   >
   >Ces variables ne sont nécessaires que si vous envisagez de suivre QoS.

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
   >Mettez à jour l’objet QoS et appelez l’événement de changement de débit binaire à chaque changement de débit binaire. Ceci produit les données QoS les plus précises.

1. Assurez-vous que la méthode `getQoSObject()` renvoie les informations QoS les plus récentes.
1. Lorsque le lecteur multimédia rencontre une erreur et que l’événement d’erreur est disponible pour l’API du lecteur, utilisez l’événement `trackError()` pour capturer les informations d’erreur. (Voir [Aperçu](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Le suivi des erreurs du lecteur multimédia n’arrête pas la session de suivi multimédia. Si l’erreur du lecteur multimédia empêche la lecture de se poursuivre, veillez à ce que la session de suivi multimédia soit fermée en appelant `trackSessionEnd()` après avoir appelé `trackError()`.
