---
seo-title: Erreurs de suivi sur Chromecast
title: Erreurs de suivi sur Chromecast
uuid: efa 9 de 8 d-c 626-4 cb 6-b 46 d -108495 dd 013 a
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Erreurs de suivi sur Chromecast{#track-errors-on-chromecast}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](../../sdk-implement/download-sdks.md)

## Mise en œuvre du suivi des erreurs

1. Track media player errors: [trackError](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackError)

   ```
   trackError(errorId)
   ```

>[!NOTE]
>
>Le suivi des erreurs du lecteur multimédia n'arrête pas la session de suivi des médias. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

