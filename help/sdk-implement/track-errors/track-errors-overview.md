---
seo-title: Aperçu
title: Aperçu
uuid: d 71429 e 6-ef 8 b -4 ea 2-8491-ff 3 cdbf 4357 f
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Aperçu{#overview}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](../../sdk-implement/download-sdks.md)

## Mise en œuvre du suivi des erreurs

1. Suivi des erreurs du lecteur multimédia.

   Pour les événements d’erreur, appelez `trackError` avec les informations d’erreur.

>[!NOTE]
>
>Le suivi des erreurs du lecteur multimédia n'arrête pas la session de suivi des médias. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

