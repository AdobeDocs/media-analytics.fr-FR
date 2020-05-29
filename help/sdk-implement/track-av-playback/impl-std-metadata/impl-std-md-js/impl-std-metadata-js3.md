---
title: Mise en oeuvre de métadonnées standard à l’aide de JavaScript 3.x
description: Décrit la définition des métadonnées vidéo et publicitaires standard à envoyer avec les appels de suivi dans les applications de navigateur (JS).
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '43'
ht-degree: 46%

---


# Mise en oeuvre de métadonnées standard à l’aide de JavaScript 3.x{#implement-standard-metadata-on-javascript}

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
