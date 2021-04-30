---
title: Envoi d’événements ping
description: Envoi d’événements ping
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
translation-type: ht
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: ht
source-wordcount: '88'
ht-degree: 100%

---

# Envoi d’événements ping {#sending-ping-events}

**Pour le contenu principal, vous devez déclencher des événements ping toutes les 10 secondes, en commençant après 10 secondes de lecture, indépendamment des autres événements d’API que vous avez envoyés. Pour le suivi des publicités, vous devez déclencher des événements ping toutes les secondes.**

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
