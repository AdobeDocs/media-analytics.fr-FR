---
title: Présentation du suivi de la qualité de l’expérience
description: Présentation du suivi de la qualité de l’expérience (QoE, QoS) à l’aide du SDK Media.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 99%

---

# Aperçu {#overview}

Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x.

>[!IMPORTANT]
>
>Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/getting-started/download-sdks.md)

La qualité du suivi de l’expérience inclut la qualité du service (QoS) et le suivi des erreurs, ces deux éléments étant facultatifs et n’étant **pas** obligatoires pour les mises en œuvre de suivi multimédia principal. Vous pouvez utiliser l’API du lecteur multimédia pour identifier les variables liées à QoS et au suivi des erreurs. Voici les éléments clés du suivi de la qualité de l’expérience :

## Événements du lecteur {#player-events}

### À chaque changement de mesure QoS :

Créez ou mettez à jour l’instance d’objet QoS pour la lecture. [Référence de l’API QoS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### À chaque événement de changement de débit binaire

L’appel `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## Implémenter QOS

1. Identifiez le moment où une mesure QoS change lors de la lecture multimédia, créez `MediaObject` à l’aide des informations QoS et mettez à jour les nouvelles informations QoS.

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

1. Assurez-vous que la méthode `getQoSObject()` renvoie les informations QoS les plus récentes.
1. Lorsque la lecture change de débit binaire, appelez l’événement `BitrateChange` dans l’instance Media Heartbeat.

   >[!IMPORTANT]
   >
   >Mettez à jour l’objet QoS et appelez l’événement de changement de débit binaire à chaque changement de débit binaire. Ceci produit les données QoS les plus précises.

L’exemple de code suivant utilise le kit SDK JavaScript 2.x pour un lecteur multimédia HTML5. Utilisez ce code avec le code de lecture multimédia principal.

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
