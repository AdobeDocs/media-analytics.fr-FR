---
title: Erreurs de suivi sur JavaScript
description: Cette rubrique décrit l’implémentation du suivi des erreurs à l’aide du SDK Media dans les applications de navigateur (JS).
uuid: 5a4fc5df-2677-4189-92af-5cd074847b39
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Erreurs de suivi sur JavaScript {#track-errors-on-javascript}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

## Mise en œuvre du suivi des erreurs

1. Pour effectuer le suivi des erreurs du lecteur multimédia :

   ```js
   onPlayerError = function() { 
       this._mediaHeartbeat.trackError("mediaErrorId"); 
   };
   ```

>[!NOTE]
>
>Le suivi des erreurs du lecteur multimédia n’arrête pas la session de suivi multimédia. Si l’erreur du lecteur multimédia empêche la lecture de se poursuivre, veillez à ce que la session de suivi multimédia soit fermée en appelant `trackSessionEnd` après avoir appelé `trackError`.

