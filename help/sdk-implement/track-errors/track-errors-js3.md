---
title: Suivi des erreurs à l’aide de JavaScript 3.x
description: Cette rubrique décrit l’implémentation du suivi des erreurs à l’aide du SDK Media dans les applications de navigateur (JS).
translation-type: tm+mt
source-git-commit: 5f274452b9ff5770908f7e2e450935be572a22ea
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 69%

---


# Suivi des erreurs à l’aide de JavaScript 3.x{#track-errors-on-javascript}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 3.x. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

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
