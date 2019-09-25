---
seo-title: Événements de mise en file d’attente lorsque la réponse des sessions est lente
title: Événements de mise en file d’attente lorsque la réponse des sessions est lente
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Événements de mise en file d’attente lorsque la réponse des sessions est lente{#queueing-events-when-sessions-response-is-slow}

L’API Media Collection est une API RESTful, ce qui signifie que vous faites une requête HTTP et attendez la réponse. This is an important point only for when you make a [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) to obtain a Session ID at the beginning of video playback. Ceci est important car l’ID de session est requis pour tous les appels de suivi suivants.

It is possible that your player may fire events _before the Sessions response returns_ (with the Session ID parameter) from the backend. If this occurs, your app must queue any tracking events that arrive between the [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) and its response. When the Sessions response arrives, you should first process any queued [events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md), then you can start processing _live_ events with the [Events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) calls.

>[!NOTE]
>
>La [requête events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) ne renvoie pas de données au client au-delà d’un code de réponse HTTP.

Vérifiez le lecteur de référence de votre distribution pour trouver le moyen de traiter les événements avant de recevoir un ID de session. Par exemple :

```js
var eventData = {};            // JSON payload 
eventData.playerTime = getPlayerTime(); // Required 
eventData.eventType = "play";           // Required 
eventData.params = {};                  // Optional for events 
 
VideoPlayer.prototype._collectEvent =  
  function(eventData) { 
 
    // If we don't have a Session ID yet,  
    // queue the event and return... 
    if (!sessionStarted) { 
        console.log("[Player] Queueing event "); 
        _pendingEvents.push(eventData); 
        return; 
    } 
 
    // If we DO have a Session ID, process the 
    // tracking event...     
    apiClient.request({ 
        "baseUrl": "{endpoint}", 
        "path": "api/v1/{sid}/events", // events request 
        "method": "POST", 
        "data": eventData 
    }).then((response) => {   
        […] 
    } 
} 
 
VideoPlayer.prototype.collectEvent =  
  function (eventType, eventParams) { 
         
    if (typeof eventParams === 'undefined') {   
        eventParams = {}; 
    } 
 
    this._collectEvent({                   
        eventType: eventType,            // Required 
        playerTime: getPlayerTime(),     // Required 
        params: eventParams              // Optional  
    });                                    
}; 
 
VideoPlayer.prototype.getPlayerTime = function() { 
    return { 
        playhead: this.getPlayhead(),    // playhead value in seconds 
        ts: this.getCurrentTimestamp()   // timestamp value in milliseconds 
    }; 
};
```

**Traiter les événements mis en file d’attente -** Le lecteur de référence traite les événements mis en file d’attente comme suit :

```js
    […] 
    this._processPendingEvents();    // Once you have a Session ID, 
    […]                              // process any queued events 
 
VideoPlayer.prototype._processPendingEvents =  
  function() { 
    this._pendingEvents.forEach((eventData) => { 
        this._collectEvent(eventData); 
    }); 
 
    this._pendingEvents = []; 
}
```

Continuez à traiter les événements de suivi à mesure qu’ils se produisent.
