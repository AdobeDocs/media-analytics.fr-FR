---
title: Découvrez Comment Effectuer Le Suivi De La Mise En Mémoire Tampon À L’Aide De JavaScript 3.x
description: Découvrez comment effectuer le suivi des événements de mise en mémoire tampon dans les applications de navigateur (JS).
exl-id: c6941942-02f9-4f9c-99ad-0c52ed2f793b
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 85%

---

# Suivi de la mise en mémoire tampon à l’aide de JavaScript 3.x{#track-buffering-on-javascript}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 3.x. Si vous mettez en œuvre une version précédente du kit SDK, vous pouvez télécharger les Guides du développeur dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

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
