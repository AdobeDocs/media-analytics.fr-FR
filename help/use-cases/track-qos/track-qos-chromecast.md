---
title: Découvrez comment effectuer le suivi de la qualité de lʼexpérience sur Chromecast
description: Découvrez l’implémentation du suivi de la qualité de l’expérience (QoE, QoS) à l’aide de Media SDK sur Chromecast.
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
exl-id: 04b9b888-2727-4aa6-a934-94a02c85a490
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/VR-udMMg3tOMsbxnt-f0zjkGVZNgnCON0diYrhhMuoE
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
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 303
ht-degree: 95%

---

# Suivre la qualité de l’expérience sur Chromecast{#track-quality-of-experience-on-chromecast}

Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x.

>[!IMPORTANT]
>
>Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/getting-started/download-sdks.md)

## Aperçu {#overview}

La qualité du suivi de l’expérience inclut la qualité du service (QoS) et le suivi des erreurs, ces deux éléments étant facultatifs et n’étant **pas** obligatoires pour les mises en œuvre de suivi multimédia principal. Vous pouvez utiliser l’API du lecteur multimédia pour identifier les variables liées à QoS et au suivi des erreurs.

## Événements du lecteur {#player-events}

### À chaque événement de changement de débit binaire

* Créez/mettez à jour l’instance d’objet QoS pour la lecture, `qosObject`
* Appel `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### Lors des erreurs du lecteur

Appelez `trackError("media error id");`

## Mise en œuvre {#implement}

1. Identifiez le moment où le débit binaire change pendant la lecture multimédia et créez l’instance `MediaObject` à l’aide des informations QoS.

   **Variables QoSObject :**

   >[!TIP]
   >
   >Ces variables ne sont nécessaires que si vous envisagez de suivre QoS.

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
   >Mettez à jour l’objet QoS et appelez l’événement de changement de débit binaire à chaque changement de débit binaire. Ceci produit les données QoS les plus précises.

1. Assurez-vous que la méthode `getQoSObject()` renvoie les informations QoS les plus récentes.
1. Lorsque le lecteur multimédia rencontre une erreur et que l’événement d’erreur est disponible pour l’API du lecteur, utilisez l’événement `trackError()` pour capturer les informations d’erreur. (Voir [Aperçu](/help/use-cases/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Le suivi des erreurs du lecteur multimédia n’arrête pas la session de suivi multimédia. Si l’erreur du lecteur multimédia empêche la lecture de se poursuivre, veillez à ce que la session de suivi multimédia soit fermée en appelant `trackSessionEnd()` après avoir appelé `trackError()`.
