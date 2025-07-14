---
title: Découvrez comment effectuer le suivi de la mise en mémoire tampon sur Roku
description: Découvrez comment effectuer le suivi des événements de mise en mémoire tampon sur Roku.
uuid: 6666b270-9aa3-42ff-95a8-f12502022d47
exl-id: 73b10b42-02ab-47f8-8250-58f03c5e0dd1
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 100%

---

# Effectuer le suivi de la mise en mémoire tampon sur Roku{#track-buffering-on-roku}

Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x.

>[!IMPORTANT]
>
>Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/getting-started/download-sdks.md)

## Constantes de suivi de la mémoire tampon

| Nom de constante | Description     |
|---|---|
| `BufferStart` | Constante permettant d’effectuer le suivi de l’événement Début de la mémoire tampon |
| `BufferComplete` | Constante permettant d’effectuer le suivi de l’événement Fin de la mémoire tampon |

## Mettez en œuvre la mise en mémoire tampon

1. Prêtez attention aux événements de mise en mémoire tampon de la lecture se produisant dans le lecteur multimédia. Une fois que vous avez reçu la notification de début de la mise en mémoire tampon, effectuez-en le suivi à l’aide de l’événement `BufferStart`.

   ```
   bufferInfo = {}
   bufferContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_BUFFER_START, bufferInfo, bufferContextData)
   ```

1. Une fois que vous avez reçu la notification de fin de la mise en mémoire tampon, effectuez-en le suivi à l’aide de l’événement `BufferComplete`.

   ```
   bufferInfo = {}
   bufferContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_BUFFER_COMPLETE, bufferInfo, bufferContextData)
   ```

Consultez le scénario de suivi [Lecture VOD avec mise en mémoire tampon](/help/use-cases/tracking-scenarios/vod-buffering.md) pour en savoir plus.
