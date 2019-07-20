---
seo-title: Présentation de la migration
title: Présentation de la migration
uuid: d 84 f 55 bc-fa 90-45 c 1-b 97 d-cb 5 fe 58 e 80 c 0 c
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Présentation de la migration{#migration-overview}

La migration de VHL 1.x vers VHL 2.x est simple, grâce à la nouvelle version offrant des API simplifiées pour l’initialisation, la configuration et les délégués de lecteur.

Voici les différences principales entre les versions 1.x et 2.x :

* **Modules complémentaires, délégués** : Vous n’avez plus besoin de mettre en œuvre des modules externes et des délégués pour Analytics, VideoPlayer et Heartbeat.
* **Configuration** : Vous n’avez plus besoin d’instancier des configurations pour les modules complémentaires 1.x.

## Benefits of 2.x {#benefits-of-two-x}

* All of the public methods are consolidated into the `MediaHeartbeat` class to make implementation easier on developers.
* All configs are now consolidated into the `MediaHeartbeatConfig` class.
* Vous n'avez plus besoin d'instancier des configurations pour les modules externes Analytics, videoplayer et Heartbeat. You only need to instantiate the `MediaHeartbeat` class with `MediaHeartbeatDelegate` and `MediaHeartbeatConfig` instances. Il s'agit de la seule implémentation requise pour initialiser Media Analytics.

   With the initialization of `MediaHeartbeat`, you can safely delete all of the implementation for Analytics Plugin, VideoPlayer Plugin, and Heartbeat Plugin. Supprimez également la mise en œuvre existante pour l’initialisation qui utilise divers modules en tant qu’entrée. You can see side-by-side comparisons of the 1.x and 2.x implementations here: [Code comparison: 1.x to 2.x.](./code-comparison-1x-2x.md)

Les nouvelles API de la version 2.x sont décrites en détail ici : [Conversion 1.x vers 2.x de l’API.](./1x-2x-api-change.md)
