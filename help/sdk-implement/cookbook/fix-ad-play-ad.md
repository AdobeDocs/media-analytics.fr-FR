---
title: Résolution du jeu principal apparaissant entre les publicités
description: Comment gérer les appels main:play inattendus entre publicités.
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Résolution des appels main:play apparaissant entre les publicités{#resolving-main-play-appearing-between-ads}

## Problème

Dans certains scénarios de suivi des publicités, vous pouvez rencontrer des appels `main:play` qui se produisent inopinément entre la fin d’une publicité et le début de la publicité suivante. If the delay between the ad complete call and the next ad start call is greater than 250 milliseconds, the Media SDK will fall back to sending `main:play` calls. Si ce retour à `main:play` survient au cours d’une coupure publicitaire preroll, la mesure de début du contenu peut être définie de façon précoce.

Un écart entre les publicités tel que décrit ci-dessus est interprété par le kit SDK Media comme du contenu principal, car il n’y a à ce niveau aucun chevauchement avec un contenu publicitaire. Le SDK Media ne contient aucune information de publicité définie, et le lecteur est à l’état de lecture. S’il n’y a aucune information de publicité et que le lecteur est à l’état de lecture, le kit SDK Media crédite la durée de l’écart en faveur du contenu principal par défaut. Il ne peut pas créditer la durée de l’écart en faveur d’informations de publicité nulles.

## IDENTIFICATION

Lors de l’utilisation d’Adobe Debug ou d’un renifleur de paquets réseau tel que Charles, si vous voyez les appels de pulsation suivants dans cet ordre pendant une coupure publicitaire preroll :

* Démarrage de la session: `s:event:type=start` &amp; `s:asset:type=main`
* Démarrage de publicité: `s:event:type=start` &amp; `s:asset:type=ad`
* Lecture de la publicité: `s:event:type=play` &amp; `s:asset:type=ad`
* Fin de la publicité: `s:event:type=complete` &amp; `s:asset:type=ad`
* Lecture du contenu principal : `s:event:type=play` &amp; `s:asset:type=main`**(inattendu)**

* Démarrage de publicité: `s:event:type=start` &amp; `s:asset:type=ad`
* Lecture de la publicité: `s:event:type=play` &amp; `s:asset:type=ad`
* Fin de la publicité: `s:event:type=complete` &amp; `s:asset:type=ad`
* Lecture du contenu principal : `s:event:type=play` &amp; `s:asset:type=main`**(attendu)**

## RÉSOLUTION

***Retardez le déclenchement de l’appel de fin de publicité.***

Gérez l’écart à partir du lecteur en appelant `trackEvent:AdComplete` pour la première publicité, suivi immédiatement de `trackEvent:AdStart` pour la deuxième publicité. L’application doit attendre d’appeler l’événement `AdComplete` après la fin de la première publicité. Assurez-vous d’appeler `trackEvent:AdComplete` pour la dernière publicité dans la coupure publicitaire. Si le lecteur peut identifier que la ressource publicitaire actuelle est la dernière dans la coupure publicitaire, appelez `trackEvent:AdComplete` immédiatement. Cette résolution aura pour résultat moins de 1 seconde de temps publicitaire supplémentaire passé attribué à l’unité de publicité précédente.

**Au démarrage de la coupure publicitaire, y compris preroll :**

* Créez l’instance d’objet `adBreak` pour la coupure publicitaire ; par exemple, `adBreakObject`.

* L’appel `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**À chaque démarrage de ressource publicitaire :**

* **appelez`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Appelez ceci uniquement si la publicité précédente n’était pas terminée. Pensez à une valeur booléenne pour conserver l’état "`isinAd`" de la publicité précédente.

* Créez l’instance d’objet publicitaire pour la ressource publicitaire : par exemple, `adObject`.
* Populate the ad metadata, `adCustomMetadata`.
* L’appel `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Call `trackPlay()` if this is the first ad in a pre-roll ad break.

**À chaque fin de ressource publicitaire :**

* **Ne pas passer d’appel**

   >[!NOTE]
   >
   >If the application knows it is the last ad in the ad break, call `trackEvent:AdComplete` here and skip setting `trackEvent:AdComplete` in the `trackEvent:AdBreakComplete`

**Lorsque la publicité est ignorée :**

* L’appel `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**À la fin de la coupure publicitaire :**

* **appelez`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >If this step is already performed above as part of the last `trackEvent:AdComplete` call then this can be skipped.

* L’appel `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.

