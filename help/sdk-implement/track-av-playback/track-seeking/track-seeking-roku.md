---
seo-title: Suivi de la recherche sur Roku
title: Suivi de la recherche sur Roku
uuid: 0572252b-397f-4aa2-b4b5-c5346b75244a
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Suivi de la recherche sur Roku{#track-seeking-on-roku}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

## Rechercher des constantes de suivi

| Nom de constante | Description     |
|---|---|
| `SeekStart` | Constante permettant d’effectuer le suivi de l’événement Début de la recherche. |
| `SeekComplete` | Constante permettant d’effectuer le suivi de l’événement Fin de la recherche. |

## Mise en oeuvre de la recherche

1. Prêtez attention aux événements de recherche se produisant dans le lecteur multimédia. Une fois que vous avez reçu la notification de début de la recherche, effectuez-en le suivi à l’aide de l’événement `SeekStart`.

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_START, seekInfo, seekContextData)
   ```

1. Une fois que vous avez reçu la notification de fin de la recherche, effectuez-en le suivi à l’aide de l’événement `SeekComplete`.

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_COMPLETE, seekInfo, seekContextData)
   ```

Consultez le scénario de suivi [Lecture VOD avec recherche dans le contenu principal](/help/sdk-implement/tracking-scenarios/vod-seeking.md) pour en savoir plus.
