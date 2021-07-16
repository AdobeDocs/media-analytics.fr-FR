---
title: Découvrez comment effectuer le suivi des erreurs sur Android
description: Découvrez l’implémentation du suivi des erreurs à l’aide du SDK Media sur Android.
uuid: 7d0c77e5-924c-4619-8e29-3484748ab736
exl-id: 6c4f693d-45c0-4a9c-bda1-c8721afe31f5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 80%

---

# Erreurs de suivi sur Android{#track-errors-on-android}

Les instructions suivantes fournissent des conseils pour la mise en œuvre à l’aide des kits SDK 2.x.

>[!IMPORTANT]
>
>Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

1. Pour effectuer le suivi des erreurs du lecteur multimédia :

   ```java
   public void onPlayerError(Observable observable, Object data) {  
       _heartbeat.trackError("mediaErrorID");
   }
   ```

>[!NOTE]
>
>Le suivi des erreurs du lecteur multimédia n’arrête pas la session de suivi multimédia. Si l’erreur du lecteur multimédia empêche la lecture de se poursuivre, veillez à ce que la session de suivi multimédia soit fermée en appelant `trackSessionEnd` après avoir appelé `trackError`.
