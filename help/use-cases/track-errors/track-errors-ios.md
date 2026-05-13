---
title: Découvrez comment effectuer le suivi des erreurs sur iOS
description: Cette rubrique décrit l’implémentation du suivi des erreurs à l’aide du SDK Media sur iOS.
uuid: 18ea93d3-5948-4375-bcdb-72309268e38d
exl-id: c4ce7092-a102-41da-80a6-a4359f925708
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/EOLvyCedoFoK4cOm9oM7-bqHJW6793mMvZPx7MMXZCQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 97
ht-degree: 100%

---

# Erreurs de suivi sur iOS{#track-errors-on-ios}

Les instructions suivantes fournissent des conseils pour la mise en œuvre sur tous les kits SDK 2.x.

>[!IMPORTANT]
>
>Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/getting-started/download-sdks.md)

## Mise en œuvre du suivi des erreurs

1. Pour effectuer le suivi des erreurs du lecteur multimédia :

   ```
   - (void)onPlayerError:(NSNotification *)notification {
       [_mediaHeartbeat trackError:@"mediaoErrorId"];
   }
   ```

>[!NOTE]
>
>Le suivi des erreurs du lecteur multimédia n’arrête pas la session de suivi multimédia. Si l’erreur du lecteur multimédia empêche la lecture de se poursuivre, veillez à ce que la session de suivi multimédia soit fermée en appelant `trackSessionEnd` après avoir appelé `trackError`.
