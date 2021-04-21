---
title: Suivi de la mise en mémoire tampon sur Roku
description: Décrit le suivi des événements de mise en mémoire tampon sur Roku.
uuid: 6666b270-9aa3-42ff-95a8-f12502022d47
exl-id: 73b10b42-02ab-47f8-8250-58f03c5e0dd1
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '112'
ht-degree: 100%

---

# Suivi de la mise en mémoire tampon sur Roku {#track-buffering-on-roku}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

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

Consultez le scénario de suivi [Lecture VOD avec mise en mémoire tampon](/help/sdk-implement/tracking-scenarios/vod-buffering.md) pour en savoir plus.
