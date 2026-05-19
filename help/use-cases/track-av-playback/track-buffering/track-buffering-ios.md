---
title: Découvrez comment effectuer le suivi de la mise en mémoire tampon sur iOS
description: Découvrez comment effectuer le suivi des événements de mise en mémoire tampon sur iOS.
uuid: 4f4db23a-489b-4b41-bb6e-393ec64d52a2
exl-id: 5f0a3c4b-7c9e-499d-98d0-6fcf316c4d9c
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/yCZGk7-ylrZBW4q3c6e6f-5Eprtkm7ipg-yIykCo-Yo
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 120
ht-degree: 100%

---

# Effectuer le suivi de la mise en mémoire tampon sur iOS{#track-buffering-on-ios}

Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x.

>[!IMPORTANT]
>
>Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/getting-started/download-sdks.md)

## Constantes de suivi de la mémoire tampon


| Nom de constante | Description     |
|---|---|
| `ADBMediaHeartbeatEventBufferStart` | Constante permettant d’effectuer le suivi de l’événement Début de la mémoire tampon |
| `ADBMediaHeartbeatEventBufferComplete` | Constante permettant d’effectuer le suivi de l’événement Fin de la mémoire tampon |

## Mettez en œuvre la mise en mémoire tampon

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

Consultez le scénario de suivi [Lecture VOD avec mise en mémoire tampon](/help/use-cases/tracking-scenarios/vod-buffering.md) pour en savoir plus.
