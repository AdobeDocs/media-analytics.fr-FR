---
title: Obtention d’un ID de session
description: Découvrez comment coder une requête sessions pour obtenir l’ID de session à partir de l’en-tête Emplacement dans une réponse.
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
exl-id: 4a1c4ade-4a5e-4af0-8117-19d718dd8bda
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 69%

---

# Obtention d’un ID de session{#obtaining-a-session-id}

Ce fragment de code du lecteur de référence affiche une méthode permettant de coder une [requête sessions](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md), ainsi que d’extraire l’ID de session (et la version de l’API Media Collection) de l’en-tête Emplacement de la réponse :

```js
var  
sessionData = { 
        ... 
        "media.contentType": "VOD", 
        "media.channel": "sample-channel", 
        ... 
    } 
}; 
...

const SESSION_ID_EXTRACTOR = /^\/api\/(.*)\/sessions\/(.*)/; 
    ...
    apiClient.request({ 
        "baseUrl": config.apiBaseUrl,   // The endpoint 
        "path": config.apiSessionsPath, // api/v1/sessions/ 
        "method": "POST",               // (Always POST) 
        "data": sessionData             // Mandatory params 
     }).then((response) => { 
        // Extract Session ID (and API version) 
        const [, apiVersion, sessionId] =  response.headers.Location.match(SESSION_ID_EXTRACTOR);  
        this.sessionId = sessionId;     // Session ID obtained 
        this._sessionStarted = true;    // Session started. 
    ...
```
