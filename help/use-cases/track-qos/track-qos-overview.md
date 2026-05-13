---
title: Présentation du suivi de la qualité de l’expérience
description: Présentation du suivi de la qualité de l’expérience (QoE, QoS) à l’aide du SDK Media.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Cc5T13Z1S15MyG-CxpxMoHX-ckULmIe0dfUOe7650DE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889beid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 265
ht-degree: 99%

---

# Aperçu{#overview}

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
