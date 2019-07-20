---
seo-title: Envoi d’événements ping
title: Envoi d’événements ping
uuid: c 92 c 1 a 92-3 af 6-4474-9 e 42-ffb 8 f 6 c 94 b 33
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Envoi d’événements ping{#sending-ping-events}

**Pour le contenu principal, vous devez déclencher des événements ping toutes les 10 secondes, en commençant après 10 secondes de lecture, indépendamment des autres événements d’API que vous avez envoyés. For Ad tracking, you must fire ping events every 1 second.**

Les événements ping sont littéralement la « pulsation » de Media Analytics. Les seuls paramètres requis pour un appel ping sont `eventType: ping` avec l’objet `playerTime` (position du curseur de lecture et horodatage).

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

