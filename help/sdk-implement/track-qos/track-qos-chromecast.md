---
title: Découvrez comment effectuer le suivi de la qualité de lʼexpérience sur Chromecast
description: « Apprenez en plus sur la mise en œuvre du suivi de la qualité de lʼexpérience (QoE, QoS) à lʼaide du SDK Media sur Chromecast. »
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
exl-id: 04b9b888-2727-4aa6-a934-94a02c85a490
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: ht
source-wordcount: '296'
ht-degree: 100%

---

# Suivi de la qualité de l’expérience sur Chromecast{#track-quality-of-experience-on-chromecast}

Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x.

>[!IMPORTANT]
>
>Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

## Aperçu  {#overview}

La qualité du suivi de l’expérience inclut la qualité du service (QoS) et le suivi des erreurs, ces deux éléments étant facultatifs et n’étant **pas** obligatoires pour les mises en œuvre de suivi multimédia principal. Vous pouvez utiliser l’API du lecteur multimédia pour identifier les variables liées à QoS et au suivi des erreurs.

## Événements du lecteur {#player-events}

### À chaque événement de changement de débit binaire

* Créez/mettez à jour l’instance d’objet QoS pour la lecture, `qosObject`
* Appel `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### Lors des erreurs du lecteur

L’appel `trackError(“media error id”);`

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
1. Lorsque le lecteur multimédia rencontre une erreur et que l’événement d’erreur est disponible pour l’API du lecteur, utilisez l’événement `trackError()` pour capturer les informations d’erreur. (Voir [Aperçu](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Le suivi des erreurs du lecteur multimédia n’arrête pas la session de suivi multimédia. Si l’erreur du lecteur multimédia empêche la lecture de se poursuivre, veillez à ce que la session de suivi multimédia soit fermée en appelant `trackSessionEnd()` après avoir appelé `trackError()`.
