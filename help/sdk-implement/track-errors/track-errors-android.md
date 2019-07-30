---
seo-title: Erreurs de suivi sur Android
title: Erreurs de suivi sur Android
uuid: 7 d 0 c 77 e 5-924 c -4619-8 e 29-3484748 ab 736
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Erreurs de suivi sur Android{#track-errors-on-android}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

1. Suivi des erreurs du lecteur multimédia :

   ```java
   public void onPlayerError(Observable observable, Object data) {  
       _heartbeat.trackError("mediaErrorID"); 
   }
   ```

>[!NOTE]
>
>Le suivi des erreurs du lecteur multimédia n'arrête pas la session de suivi des médias. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

