---
seo-title: Aperçu
title: Aperçu
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# Aperçu{#overview}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. Vous pouvez utiliser l’API du lecteur multimédia pour identifier les variables liées à la qualité de service et au suivi des erreurs. Voici les éléments clés du suivi de la qualité de l’expérience :

## Événements du lecteur {#player-events}

### À chaque changement de mesure QoS :

Créez ou mettez à jour l’instance d’objet QoS pour la lecture. [Référence de l’API QoS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### Sur tous les événements de changement de débit

L’appel   `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## Mise en oeuvre de QOS

1. Identify when any of QOS metrics change during media playback, create the `MediaObject` using the QoS information, and update the new QoS information.

   Variables QoSObject :

   >[!TIP]
   >
   >Ces variables ne sont requises que si vous prévoyez d’effectuer le suivi de la qualité de service.

   | Variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `bitrate` | Débit actuel | Oui |
   | `startupTime` | Temps de démarrage | Oui |
   | `fps` | Valeur fps | Oui |
   | `droppedFrames` | Nombre de pertes d’images | Oui |

1. Assurez-vous que la méthode `getQoSObject()` renvoie les informations QoS les plus récentes.
1. Lorsque la lecture change de débit binaire, appelez l’événement `BitrateChange` dans l’instance Media Heartbeat.

   >[!IMPORTANT]
   >
   >Mettez à jour l’objet QoS et appelez l’événement de changement de débit à chaque changement de débit. Ceci produit les données QoS les plus précises.

L’exemple de code suivant utilise le SDK JavaScript 2.x pour un lecteur de médias HTML5. Utilisez ce code avec le code de lecture du média principal.

```js
var mediaDelegate = new MediaHeartbeatDelegate(); 
...  
 
// This is called periodically by MediaHeartbeat instance 
mediaDelegate.prototype.getQoSObject = function() { 
    return this.qosInfo; 
}; 
 
if (e.type == "qos_update") { 
    var qosInfo = MediaHeartbeat.createQoSObject(<BITRATE>,<STARTUP_TIME>,<FPS>,<DROPPED_FRAMES>); 
    mediaDelegate.qosInfo = qosInfo; 
}; 
 
if (e.type == "bitrate_change") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
};
```

