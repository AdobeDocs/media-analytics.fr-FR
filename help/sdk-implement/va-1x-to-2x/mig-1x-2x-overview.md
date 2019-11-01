---
title: Présentation de la migration
description: Cette rubrique présente un aperçu de la migration des versions 1.x à 2.x du SDK multimédia.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Présentation de la migration{#migration-overview}

La migration de VHL 1.x vers VHL 2.x est simple, grâce à la nouvelle version offrant des API simplifiées pour l’initialisation, la configuration et les délégués de lecteur.

Voici les différences principales entre les versions 1.x et 2.x :

* **Modules complémentaires, délégués** : Vous n’avez plus besoin de mettre en œuvre des modules externes et des délégués pour Analytics, VideoPlayer et Heartbeat.
* **Configuration** : Vous n’avez plus besoin d’instancier des configurations pour les modules complémentaires 1.x.

## Avantages de la version 2.x {#benefits-of-two-x}

* All of the public methods are consolidated into the `MediaHeartbeat` class to make implementation easier on developers.
* All configs are now consolidated into the `MediaHeartbeatConfig` class.
* Vous n’avez plus besoin d’instancier les configurations des modules externes Analytics, VideoPlayer et Heartbeat. Il vous suffit d’instancier la `MediaHeartbeat` classe avec `MediaHeartbeatDelegate` et `MediaHeartbeatConfig` les instances. Il s’agit de la seule implémentation requise pour initialiser Media Analytics.

   With the initialization of `MediaHeartbeat`, you can safely delete all of the implementation for Analytics Plugin, VideoPlayer Plugin, and Heartbeat Plugin. Supprimez également la mise en œuvre existante pour l’initialisation qui utilise divers modules en tant qu’entrée. You can see side-by-side comparisons of the 1.x and 2.x implementations here: [Code comparison: 1.x to 2.x.](./code-comparison-1x-2x.md)

Les nouvelles API de la version 2.x sont décrites en détail ici : [Conversion 1.x vers 2.x de l’API.](./1x-2x-api-change.md)
