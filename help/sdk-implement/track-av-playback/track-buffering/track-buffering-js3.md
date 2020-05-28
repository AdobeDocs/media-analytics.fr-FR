---
title: Suivi de la mise en mémoire tampon à l’aide de JavaScript 3.x
description: Décrit le suivi des événements de mise en mémoire tampon dans les applications de navigateur (JS).
translation-type: tm+mt
source-git-commit: 8235fee973623c168dbf83f43aa85f13b4e06cff
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 74%

---


# Suivi de la mise en mémoire tampon à l’aide de JavaScript 3.x{#track-buffering-on-javascript}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 3.x. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Constantes de suivi de la mémoire tampon

| Nom de constante | Description     |
|---|---|
| `BufferStart` | Constante permettant d’effectuer le suivi de l’événement Début de la mémoire tampon |
| `BufferComplete` | Constante permettant d’effectuer le suivi de l’événement Fin de la mémoire tampon |

## Mettez en œuvre la mise en mémoire tampon

1. Prêtez attention aux événements de mise en mémoire tampon de la lecture se produisant dans le lecteur multimédia. Une fois que vous avez reçu la notification de début de la mise en mémoire tampon, effectuez-en le suivi à l’aide de l’événement `BufferStart`.

   ```js
   _onBufferStart = function() {
       tracker.trackEvent(ADB.Media.Event.BufferStart);
   };
   ```

1. Une fois que vous avez reçu la notification de fin de la mise en mémoire tampon, effectuez-en le suivi à l’aide de l’événement `BufferComplete`.

   ```js
   _onBufferComplete = function() {
       tracker.trackEvent(ADB.Media.Event.BufferComplete);
   };
   ```

Consultez le scénario de suivi [Lecture VOD avec mise en mémoire tampon](/help/sdk-implement/tracking-scenarios/vod-buffering.md) pour en savoir plus.
