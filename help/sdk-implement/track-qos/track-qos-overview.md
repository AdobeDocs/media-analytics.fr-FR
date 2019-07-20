---
seo-title: Aperçu
title: Aperçu
uuid: 4 d 73 c 47 f-d 0 a 4-4228-9040-d 6432311 c 9 eb
translation-type: tm+mt
source-git-commit: 654aaef5d816e75429975d04c4e81ad4d4b6f706

---


# Aperçu{#overview}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](../../sdk-implement/download-sdks.md)

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. Vous pouvez utiliser l'API du lecteur multimédia pour identifier les variables liées à la qualité de service (qos) et le suivi des erreurs. Voici les éléments clés du suivi de la qualité de l’expérience :

## Player events {#player-events}

### À chaque changement de mesure QoS :

Créez ou mettez à jour l’instance d’objet QoS pour la lecture. [Référence de l'API qos](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### Sur tous les événements de changement de débit

L’appel   `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## QOS d'implémentation

1. Identify when any of QOS metrics change during media playback, create the `MediaObject` using the QoS information, and update the new QoS information.

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

1. Assurez-vous que la méthode `getQoSObject()` renvoie les informations QoS les plus récentes.
1. Lorsque la lecture change de débit binaire, appelez l’événement `BitrateChange` dans l’instance Media Heartbeat.

   >[!IMPORTANT]
   >
   >Mettez à jour l'objet qos et appelez l'événement de changement de débit lors de chaque changement de débit. Ceci produit les données QoS les plus précises.

L'exemple de code suivant utilise le SDK JavaScript 2. x pour un lecteur de médias HTML 5. Utilisez ce code avec le code de lecture de média principal.

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

## Validation {#section_F3174831408947A893F7E8C15659E5AA}

### Changement de débit binaire

À chaque changement de débit, un appel `bitrate_change` Heartbeat sera envoyé.

### Erreur

Lors d’une erreur du lecteur, un appel d’erreur Heartbeat est envoyé incluant la valeur d’erreur.
