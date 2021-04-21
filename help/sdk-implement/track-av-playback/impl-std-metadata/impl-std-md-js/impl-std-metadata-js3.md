---
title: Implémentation de métadonnées standard à l’aide de JavaScript 3.x
description: Décrit la définition des métadonnées vidéo et publicitaires standard à envoyer avec les appels de suivi dans les applications de navigateur (JS).
exl-id: 228ba000-10e2-4906-8417-265a03367a9b
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '43'
ht-degree: 100%

---

# Implémentation de métadonnées standard à l’aide de JavaScript 3.x {#implement-standard-metadata-on-javascript}

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
