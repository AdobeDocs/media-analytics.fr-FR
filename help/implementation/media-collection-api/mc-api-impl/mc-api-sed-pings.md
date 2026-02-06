---
title: Envoi d’événements ping
description: Les événements ping sont le pouls des services de streaming multimédia Adobe. Découvrez comment envoyer un ping programmé pour effectuer le suivi du contenu principal ou/et des publicités.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 50%

---

# Envoi d’événements ping{#sending-ping-events}

**Vous devez déclencher des événements ping toutes les 10 secondes, à partir de 10 secondes de lecture, quels que soient les autres événements API que vous avez envoyés. Cela s’applique à la fois au suivi du contenu principal et des annonces publicitaires.**

Les événements ping sont le « heartbeat » des services de médias en flux continu Adobe. Les seuls paramètres requis pour un appel ping sont `eventType: ping` avec l’objet `playerTime` (position du curseur de lecture et horodatage).

L’extrait de code suivant illustre une méthode de mise en œuvre d’un mécanisme ping chronométré pour le contenu principal (intervalle de 10 secondes) :

```js
... 
Pinger.init(10000); 
... 
Pinger.kill();

var Pinger = { 
    init: function(interval) { 
        this._timer = window.setInterval(function() { 
                $.event.trigger({type: "onPing", _data: ""}); 
            }, interval); 
    }, 
     
    kill: function() { 
        window.clearInterval(this._timer); 
    } 
}
```
