---
title: Résolution des appels main:play apparaissant entre les publicités
description: « Découvrez comment gérer les appels main:play inattendus entre les publicités. »
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
exl-id: f27ce2ba-7584-4601-8837-d8316c641708
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 100%

---


# Gérer les écarts qui apparaissent entre les publicités{#resolving-main-play-appearing-between-ads}

## Problème

Dans certains scénarios de suivi des publicités, vous pouvez rencontrer des appels `main:play` qui se produisent inopinément entre la fin d’une publicité et le début de la publicité suivante. Si le délai entre l’appel de fin de publicité et l’appel de démarrage de la publicité suivante est supérieur à 250 millisecondes, le SDK Media retourne à l’envoi d’appels `main:play`. Si ce retour à `main:play` survient au cours d’une coupure publicitaire preroll, la mesure de début du contenu peut être définie de façon précoce.

Un écart entre les publicités tel que décrit ci-dessus est interprété par le kit SDK Media comme du contenu principal, car il n’y a à ce niveau aucun chevauchement avec un contenu publicitaire. Le SDK Media ne contient aucune information de publicité définie, et le lecteur est à l’état de lecture. S’il n’y a aucune information de publicité et que le lecteur est à l’état de lecture, le kit SDK Media crédite la durée de l’écart en faveur du contenu principal par défaut. Il ne peut pas créditer la durée de l’écart en faveur d’informations de publicité nulles.

## IDENTIFICATION

Pendant que vous utilisez Adobe Debug ou un renifleur de paquets réseau tel que Charles, si les appels Heartbeat suivants apparaissent dans cet ordre pendant une coupure publicitaire preroll :

* Démarrage de la session : `s:event:type=start` &amp; `s:asset:type=main`
* Démarrage de publicité : `s:event:type=start` &amp; `s:asset:type=ad`
* Lecture de la publicité : `s:event:type=play` &amp; `s:asset:type=ad`
* Fin de la publicité : `s:event:type=complete` &amp; `s:asset:type=ad`
* Lecture du contenu principal : `s:event:type=play` &amp; `s:asset:type=main` **(inattendu)**

* Démarrage de publicité : `s:event:type=start` &amp; `s:asset:type=ad`
* Lecture de la publicité : `s:event:type=play` &amp; `s:asset:type=ad`
* Fin de la publicité : `s:event:type=complete` &amp; `s:asset:type=ad`
* Lecture du contenu principal : `s:event:type=play` &amp; `s:asset:type=main` **(attendu)**

## RÉSOLUTION

***Retardez le déclenchement de l’appel de fin de publicité.***

Gérez l’écart à partir du lecteur en appelant `trackEvent:AdComplete` pour la première publicité, suivi immédiatement de `trackEvent:AdStart` pour la deuxième publicité. L’application doit attendre d’appeler l’événement `AdComplete` après la fin de la première publicité. Assurez-vous d’appeler `trackEvent:AdComplete` pour la dernière publicité dans la coupure publicitaire. Si le lecteur peut identifier que la ressource publicitaire actuelle est la dernière dans la coupure publicitaire, appelez `trackEvent:AdComplete` immédiatement. Cette résolution aura pour résultat moins de 1 seconde de temps publicitaire supplémentaire passé attribué à l’unité de publicité précédente.

**Au démarrage de la coupure publicitaire, y compris preroll :**

* Créez l’instance d’objet `adBreak` pour la coupure publicitaire ; par exemple, `adBreakObject`.

* L’appel `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**À chaque démarrage de ressource publicitaire :**

* **Appelez`trackEvent(MediaHeartbeat.Event.AdComplete);`**

  >[!NOTE]
  >
  >Appelez cette méthode uniquement si la publicité précédente n’était pas complète. Pensez à une valeur booléenne pour conserver l’état &quot;`isinAd`&quot; de la publicité précédente.

* Créez l’instance d’objet publicitaire pour la ressource publicitaire : par exemple, `adObject`.
* Renseignez les métadonnées de publicité, `adCustomMetadata`.
* L’appel `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Appelez `trackPlay()` s’il s’agit de la première publicité dans une coupure publicitaire preroll.

**À chaque fin de ressource publicitaire :**

* **Ne pas effectuer d’appel**

  >[!NOTE]
  >
  >Si l’application sait qu’il s’agit de la dernière publicité dans la coupure publicitaire, appelez `trackEvent:AdComplete` ici et ne définissez pas `trackEvent:AdComplete` dans `trackEvent:AdBreakComplete`.

**Lorsque la publicité est ignorée :**

* L’appel `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**À la fin de la coupure publicitaire :**

* **Appelez`trackEvent(MediaHeartbeat.Event.AdComplete);`**

  >[!NOTE]
  >
  >Si cette étape est déjà effectuée ci-dessus dans le cadre du dernier appel `trackEvent:AdComplete`, elle peut être ignorée.

* L’appel `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.
