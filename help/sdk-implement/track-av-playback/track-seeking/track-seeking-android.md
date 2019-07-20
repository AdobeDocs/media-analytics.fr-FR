---
seo-title: Suivi de la recherche sur Android
title: Suivi de la recherche sur Android
uuid: 65 addd 99-eebf -4 a 80-8 b 4 a-d 5 fbdff 8 ab 06
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Suivi de la recherche sur Android{#track-seeking-on-android}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](../../../sdk-implement/download-sdks.md)

## Constantes de suivi de recherche

| Nom de constante | Description     |
|---|---|
| `MediaHeartbeat.Event.SeekStart` | Constante permettant d’effectuer le suivi de l’événement Début de la recherche. |
| `MediaHeartbeat.Event.SeekComplete` | Constante permettant d’effectuer le suivi de l’événement Fin de la recherche. |

## Mettre en œuvre la recherche

1. Prêtez attention aux événements de recherche se produisant dans le lecteur multimédia. Une fois que vous avez reçu la notification de début de la recherche, effectuez-en le suivi à l’aide de l’événement `SeekStart` :

   ```java
   public void onSeekStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 
   }
   ```

1. Une fois que vous avez reçu la notification de fin de la recherche, effectuez-en le suivi à l’aide de l’événement `SeekComplete` :

   ```java
   public void onSeekComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 
   }
   ```

Consultez le scénario de suivi [Lecture VOD avec recherche dans le contenu principal](../../../sdk-implement/tracking-scenarios/vod-seeking.md) pour en savoir plus.
