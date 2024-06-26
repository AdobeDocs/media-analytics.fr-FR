---
title: Découvrez comment effectuer le suivi de la qualité de lʼexpérience à lʼaide de JavaScript 3.x
description: « Découvrez comment mettre en œuvre le suivi de la qualité de lʼexpérience (QoE, QoS) à lʼaide du SDK Media dans les applications de navigateur avec JavaScript 3x. »
exl-id: b5570e9c-8fb1-4458-bd1a-86ff6fce7813
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 99%

---

# Effectuer le suivi de la qualité de l’expérience à l’aide de JavaScript 3.x{#track-quality-of-experience-on-javascript}

Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x.

>[!IMPORTANT]
>
>Si vous mettez en œuvre une version précédente du kit SDK, vous pouvez télécharger les Guides du développeur dans la rubrique [Téléchargement des SDK.](/help/getting-started/download-sdks.md)

## Mise en oeuvre de l’assouplissement quantitatif

1. Identifiez le moment où le débit binaire change pendant la lecture du média et créez l’instance `qoeObject` à l’aide des informations QoE.

   Variables QoEObject :

   >[!TIP]
   >
   >Ces variables ne sont nécessaires que si vous envisagez de suivre QoS.

   | Variable | Type | Description |
   | --- | --- | --- |
   | `bitrate` | number | Débit actuel |
   | `startupTime` | number | Temps de démarrage |
   | `fps` | number | Valeur fps |
   | `droppedFrames` | number | Nombre de pertes d’images |

   Création d’objets QoE :

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and
   // <droppeFrames> with the current playback QoE values.
   var qoeObject = ADB.Media.createQoEObject(<bitrate>,
                                                  <startuptime>,
                                                  <fps>,
                                                  <droppedFrames>);
   tracker.updateQoEObject(qoeObject);
   ```

1. Lorsque la lecture change de débit binaire, appelez l’événement `BitrateChange` dans l’instance Media Heartbeat :

   ```js
   _onBitrateChange = function() {
       // If the new bitrate value is available provide it to the tracker.
       var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
       tracker.updateQoEObject(qoeObject);
   
       tracker.trackEvent(ADB.Media.Event.BitrateChange);
   };
   ```

   >[!IMPORTANT]
   >
   >Mettez à jour l’objet QoE et appelez l’événement de changement de débit binaire à chaque changement de débit binaire. Cette opération produit les données QoE les plus précises.

1. Veillez à appeler la méthode `updateQoEObject()` pour fournir au SDK les informations QoE les plus à jour.
1. Lorsque le lecteur multimédia rencontre une erreur et que l’événement d’erreur est disponible pour l’API du lecteur, utilisez l’événement `trackError()` pour capturer les informations d’erreur. (Voir [Aperçu](/help/use-cases/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Le suivi des erreurs du lecteur multimédia n’arrête pas la session de suivi multimédia. Si l’erreur du lecteur multimédia empêche la lecture de se poursuivre, veillez à ce que la session de suivi multimédia soit fermée en appelant `trackSessionEnd()` après avoir appelé `trackError()`.
