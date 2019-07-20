---
seo-title: Suivi de la mise en mémoire tampon sur iOS
title: Suivi de la mise en mémoire tampon sur iOS
uuid: 4 f 4 db 23 a -489 b -4 b 41-bb 6 e -393 ec 64 d 52 a 2
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Suivi de la mise en mémoire tampon sur iOS{#track-buffering-on-ios}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](../../../sdk-implement/download-sdks.md)

## Constantes de suivi de la mémoire tampon


| Nom de constante | Description     |
|---|---|
| `ADBMediaHeartbeatEventBufferStart` | Constante permettant d’effectuer le suivi de l’événement Début de la mémoire tampon |
| `ADBMediaHeartbeatEventBufferComplete` | Constante permettant d’effectuer le suivi de l’événement Fin de la mémoire tampon |

## Mise en œuvre de la mise en mémoire tampon

1. Prêtez attention aux événements de mise en mémoire tampon de la lecture se produisant dans le lecteur multimédia. Une fois que vous avez reçu la notification de début de la mise en mémoire tampon, effectuez-en le suivi à l’aide de l’événement `BufferStart` :

   ```
   - (void)onBufferStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Une fois que vous avez reçu la notification de fin de la mise en mémoire tampon, effectuez-en le suivi à l’aide de l’événement `BufferComplete` :

   ```
   - (void)onBufferComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

Consultez le scénario de suivi [Lecture VOD avec mise en mémoire tampon](../../../sdk-implement/tracking-scenarios/vod-buffering.md) pour en savoir plus.
