---
title: Découvrez comment effectuer le suivi des erreurs sur Android
description: Découvrez comment mettre en œuvre le suivi des erreurs à lʼaide du SDK Media sur Android.
uuid: 7d0c77e5-924c-4619-8e29-3484748ab736
exl-id: 6c4f693d-45c0-4a9c-bda1-c8721afe31f5
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 100%

---

# Erreurs de suivi sur Android {#track-errors-on-android}

Les instructions suivantes fournissent des conseils pour la mise en œuvre à l’aide des kits SDK 2.x.

>[!IMPORTANT]
>
>Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/getting-started/download-sdks.md)

1. Pour effectuer le suivi des erreurs du lecteur multimédia :

   ```java
   public void onPlayerError(Observable observable, Object data) {  
       _heartbeat.trackError("mediaErrorID");
   }
   ```

>[!NOTE]
>
>Le suivi des erreurs du lecteur multimédia n’arrête pas la session de suivi multimédia. Si l’erreur du lecteur multimédia empêche la lecture de se poursuivre, veillez à ce que la session de suivi multimédia soit fermée en appelant `trackSessionEnd` après avoir appelé `trackError`.
