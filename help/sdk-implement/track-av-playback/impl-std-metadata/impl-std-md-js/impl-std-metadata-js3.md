---
title: Découvrez comment mettre en oeuvre des métadonnées standard à l’aide de JavaScript 3.x
description: Découvrez comment définir des métadonnées vidéo et publicitaires standard à envoyer avec les appels de suivi dans les applications de navigateur (JS 3.x).
exl-id: 228ba000-10e2-4906-8417-265a03367a9b
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 44%

---

# Implémentation de métadonnées standard à l’aide de JavaScript 3.x{#implement-standard-metadata-on-javascript}

## Mise en œuvre

Instanciez un objet de données contextuelles, renseignez les variables de métadonnées standard de votre choix. Par exemple :

```js
_onVideoLoad = function () {
    //Create the Media Object
    var mediaObject =
      ADB.Media.createMediaObject(<MEDIA_NAME>,
                                       <MEDIA_ID,
                                       <MEDIA_LENGTH>,
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>);

    //Set standard Video Metadata
    var contextData = {};
    contextData = "Sample Show";
    contextData = "Sample Season";
    contextData = "Sample Episode";

    //Set standard Audio Metadata
    var contextData = {};
    contextData = "Sample Artist";
    contextData = "Sample Album";
    contextData = "Sample Label";

    this.tracker.trackSessionStart(mediaObject, contextData);
};
```
