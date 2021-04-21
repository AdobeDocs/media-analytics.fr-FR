---
title: Suivi des erreurs à l’aide de JavaScript 3.x
description: Cette rubrique décrit l’implémentation du suivi des erreurs à l’aide du SDK Media dans les applications de navigateur (JS).
exl-id: 3769fc47-fbc4-4498-9d2a-04c88cdd0e83
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '95'
ht-degree: 100%

---

# Suivi des erreurs à l’aide de JavaScript 3.x {#track-errors-on-javascript}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 3.x. Si vous mettez en œuvre une version précédente du kit SDK, vous pouvez télécharger les Guides du développeur dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

## Mise en œuvre du suivi des erreurs

1. Pour effectuer le suivi des erreurs du lecteur multimédia :

   ```js
   onPlayerError = function() {
       tracker.trackError("errorId");
   };
   ```

>[!NOTE]
>
>Le suivi des erreurs du lecteur multimédia n’arrête pas la session de suivi multimédia. Si l’erreur du lecteur multimédia empêche la lecture de se poursuivre, veillez à ce que la session de suivi multimédia soit fermée en appelant `trackSessionEnd` après avoir appelé `trackError`.
