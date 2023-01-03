---
title: Envoi d’événements ping
description: Les événements ping sont la quintessence de Streaming Media Analytics. Découvrez comment envoyer un ping programmé pour effectuer le suivi du contenu principal ou/et des publicités.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '108'
ht-degree: 100%

---

# Envoi d’événements ping{#sending-ping-events}

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
