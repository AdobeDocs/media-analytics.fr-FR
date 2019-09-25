---
seo-title: Erreurs de suivi sur Roku
title: Erreurs de suivi sur Roku
uuid: 4e0165f9-9169-47ed-9f11-ea8a8778f663
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Erreurs de suivi sur Roku{#track-errors-on-roku}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

## Mise en oeuvre du suivi des erreurs

1. Suivi des erreurs du lecteur multimédia :

   ```
   ADBMobile().mediaTrackError(msg.GetMessage(), 
                               ADBMobile().ERROR_SOURCE_PLAYER)
   ```

>[!NOTE]
>
>Le suivi des erreurs du lecteur multimédia n’arrête pas la session de suivi multimédia. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

