---
title: Suivi de la recherche sur JavaScript
description: Cette rubrique décrit l’implémentation du suivi des recherches à l’aide du SDK Media dans les applications de navigateur (JS).
uuid: 089947fb-8bae-4ae8-b215-53793620efd7
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Suivi de la recherche sur JavaScript {#track-seeking-on-javascript}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

## Constantes de suivi de la recherche

| Nom de constante | Description     |
|---|---|
| `SeekStart` | Constante permettant d’effectuer le suivi de l’événement Début de la recherche. |
| `SeekComplete` | Constante permettant d’effectuer le suivi de l’événement Fin de la recherche. |

## Mise en œuvre de la recherche

1. Prêtez attention aux événements de recherche se produisant dans le lecteur multimédia. Une fois que vous avez reçu la notification de début de la recherche, effectuez-en le suivi à l’aide de l’événement `SeekStart` :

   ```js
   _onSeekStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
   };
   ```

1. Une fois que vous avez reçu la notification de fin de la recherche, effectuez-en le suivi à l’aide de l’événement `SeekComplete` :

   ```js
   _onSeekComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
   };
   ```

Consultez le scénario de suivi [Lecture VOD avec recherche dans le contenu principal](/help/sdk-implement/tracking-scenarios/vod-seeking.md) pour en savoir plus.
