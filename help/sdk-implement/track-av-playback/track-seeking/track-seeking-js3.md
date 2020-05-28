---
title: Suivi de la recherche à l’aide de JavaScript 3.x
description: Cette rubrique décrit l’implémentation du suivi des recherches à l’aide du SDK Media dans les applications de navigateur (JS).
translation-type: tm+mt
source-git-commit: 5f274452b9ff5770908f7e2e450935be572a22ea
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 76%

---


# Suivi de la recherche à l’aide de JavaScript 3.x{#track-seeking-on-javascript}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 3.x. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Constantes de suivi de la recherche

| Nom de constante | Description     |
|---|---|
| `SeekStart` | Constante permettant d’effectuer le suivi de l’événement Début de la recherche. |
| `SeekComplete` | Constante permettant d’effectuer le suivi de l’événement Fin de la recherche. |

## Mise en œuvre de la recherche

1. Prêtez attention aux événements de recherche se produisant dans le lecteur multimédia. Une fois que vous avez reçu la notification de début de la recherche, effectuez-en le suivi à l’aide de l’événement `SeekStart` :

   ```js
   _onSeekStart = function() {
       tracker.trackEvent(ADB.Media.Event.SeekStart);
   };
   ```

1. Une fois que vous avez reçu la notification de fin de la recherche, effectuez-en le suivi à l’aide de l’événement `SeekComplete` :

   ```js
   _onSeekComplete = function() {
       tracker.trackEvent(ADB.Media.Event.SeekComplete);
   };
   ```

Consultez le scénario de suivi [Lecture VOD avec recherche dans le contenu principal](/help/sdk-implement/tracking-scenarios/vod-seeking.md) pour en savoir plus.
