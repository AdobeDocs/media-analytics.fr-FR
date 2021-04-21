---
title: Suivi de la recherche à l’aide de JavaScript 3.x
description: Cette rubrique décrit l’implémentation du suivi des recherches à l’aide du SDK Media dans les applications de navigateur (JS).
exl-id: b7152436-520e-4f38-a8ad-1027ca3f1f6c
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '126'
ht-degree: 100%

---

# Suivi de la recherche à l’aide de JavaScript 3.x {#track-seeking-on-javascript}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 3.x. Si vous mettez en œuvre une version précédente du kit SDK, vous pouvez télécharger les Guides du développeur dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

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
