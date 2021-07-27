---
title: Découvrez comment effectuer le suivi de la qualité de lʼexpérience sur Android
description: « Découvrez comment mettre en œuvre le suivi de la qualité de lʼexpérience (QoE, QoS) à lʼaide du SDK Media sur Android. »
uuid: 81ff3939-48a6-45c1-8837-ddfa33490559
exl-id: cee8b119-bca2-4a5c-8111-2b49f7eede66
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: ht
source-wordcount: '158'
ht-degree: 100%

---

# Suivi de la qualité de l’expérience sur Android{#track-quality-of-experience-on-android}

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

   ```java
   MediaObject qosObject =  
     MediaHeartbeat.createQoSObject(<BITRATE>,  
                                    <STARTUP_TIME>,  
                                    <FPS>,  
                                    <DROPPED_FRAMES>);
   ```

1. Assurez-vous que la méthode `getQoSObject()` renvoie les informations QoS les plus récentes.
1. Lorsque la lecture change de débit binaire, appelez l’événement `BitrateChange` dans l’instance Media Heartbeat :

   ```java
   public void onBitrateChange(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, null, null);
   }
   ```

   >[!IMPORTANT]
   >
   >Mettez à jour l’objet QoS et appelez l’événement de changement de débit binaire à chaque changement de débit binaire. Ceci produit les données QoS les plus précises.
