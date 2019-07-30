---
seo-title: Suivi de la mise en mémoire tampon sur Android
title: Suivi de la mise en mémoire tampon sur Android
uuid: f 16 ce 76 d -1 db 3-4 b 51-8 c 98-54 cb 781 f 71 d 7
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Suivi de la mise en mémoire tampon sur Android{#track-buffering-on-android}

>[!IMPORTANT]
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDks.](/help/sdk-implement/download-sdks.md)

## Constantes de suivi de la mémoire tampon

| Nom de constante | Description     |
|---|---|
| `MediaHeartbeat.Event.BufferStart` | Constante permettant d’effectuer le suivi de l’événement Début de la mémoire tampon |
| `MediaHeartbeat.Event.BufferComplete` | Constante permettant d’effectuer le suivi de l’événement Fin de la mémoire tampon |

## Mise en œuvre de la mise en mémoire tampon

1. Prêtez attention aux événements de mise en mémoire tampon de la lecture se produisant dans le lecteur multimédia. Une fois que vous avez reçu la notification de début de la mise en mémoire tampon, effectuez-en le suivi à l’aide de l’événement `BufferStart` :

   ```java
   public void onBufferStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null); 
   }
   ```

1. Une fois que vous avez reçu la notification de fin de la mise en mémoire tampon, effectuez-en le suivi à l’aide de l’événement `BufferComplete` :

   ```java
   public void onBufferComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete,null, null); 
   }
   ```

Consultez le scénario de suivi [Lecture VOD avec mise en mémoire tampon](/help/sdk-implement/tracking-scenarios/vod-buffering.md) pour en savoir plus.
