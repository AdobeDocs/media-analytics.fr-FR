---
title: Envoi d’événements ping
description: Les événements ping sont la pulsation du module complémentaire Collection de médias en flux continu. Découvrez comment envoyer un ping programmé pour effectuer le suivi du contenu principal ou/et des publicités.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 50%

---

# Envoi d’événements ping{#sending-ping-events}

**Vous devez déclencher des événements ping toutes les 10 secondes, en commençant après 10 secondes de lecture, indépendamment des autres événements API que vous avez envoyés. Cela s&#39;applique à la fois au contenu principal et au suivi des publicités.**

Les événements ping sont la &quot;pulsation&quot; du module complémentaire Collection de médias en flux continu. Les seuls paramètres requis pour un appel ping sont `eventType: ping` avec l’objet `playerTime` (position du curseur de lecture et horodatage).

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
