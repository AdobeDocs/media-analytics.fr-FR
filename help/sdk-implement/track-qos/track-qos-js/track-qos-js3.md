---
title: Suivi de la qualité de l’expérience à l’aide de JavaScript 3.x
description: Cette rubrique décrit la mise en oeuvre du suivi de la qualité de l’expérience (QoE, QoS) à l’aide du SDK Media dans les applications de navigateur utilisant JavaScript 3x.
translation-type: tm+mt
source-git-commit: fa161e2d41629fdfe77100d87d6a44728e23d77f
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 49%

---


# Suivi de la qualité de l’expérience à l’aide de JavaScript 3.x{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 3.x. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Mise en oeuvre de QOE

1. Identify when the bitrate changes during media playback and create the `qoeObject` instance using the QoE information.

   Variables QoEObject :

   >[!TIP]
   >
   >Ces variables ne sont nécessaires que si vous envisagez de suivre QoS.

   | Variable | Type | Description |
   | --- | --- | --- |
   | `bitrate` | nombre | Débit actuel |
   | `startupTime` | nombre | Temps de démarrage |
   | `fps` | nombre | Valeur fps |
   | `droppedFrames` | nombre | Nombre de pertes d’images |

   Création d&#39;objets QoE :

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
   >Mettez à jour l’objet QoE et appelez le événement de changement de débit à chaque changement de débit. Ceci fournit les données de QoE les plus précises.

1. Veillez à appeler `updateQoEObject()` la méthode pour fournir les informations de qualité de l’expérience les plus mises à jour au SDK.
1. Lorsque le lecteur multimédia rencontre une erreur et que l’événement d’erreur est disponible pour l’API du lecteur, utilisez l’événement `trackError()` pour capturer les informations d’erreur. (Voir [Aperçu](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Le suivi des erreurs du lecteur multimédia n’arrête pas la session de suivi multimédia. Si l’erreur du lecteur multimédia empêche la lecture de se poursuivre, veillez à ce que la session de suivi multimédia soit fermée en appelant `trackSessionEnd()` après avoir appelé `trackError()`.
