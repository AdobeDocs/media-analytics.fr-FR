---
title: Événements de mise en file d’attente lorsque la réponse des sessions est lente
description: Événements de mise en file d’attente lorsque la réponse des sessions est lente
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
exl-id: 2c23c378-c104-4256-b6e7-8eb6871f62da
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 100%

---

# Événements de mise en file d’attente lorsque la réponse des sessions est lente {#queueing-events-when-sessions-response-is-slow}

L’API Media Collection est une API RESTful, ce qui signifie que vous faites une requête HTTP et attendez la réponse. Ceci est uniquement important lorsque vous effectuez une [requête sessions](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir un ID de session au début de la lecture vidéo. Ceci est important car l’ID de session est requis pour tous les appels de suivi suivants.

Il se peut que votre lecteur déclenche des événements _avant que la réponse sessions ne soit renvoyée_ (avec le paramètre d’ID de session) par le serveur principal. Dans ce cas, votre application doit mettre en file d’attente tout événement de suivi ayant lieu entre la [requête sessions](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) et sa réponse. Lorsque la réponse sessions arrive, vous devez d’abord traiter les [événements](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) mis en file d’attente, puis commencer à traiter les événements _en direct_ avec les appels [events.](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

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
