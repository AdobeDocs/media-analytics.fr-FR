---
title: Présentation de la migration
description: Cette rubrique présente un aperçu de la migration des versions 1.x vers 2.x du SDK Media.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '213'
ht-degree: 100%

---

# Présentation de la migration {#migration-overview}

La migration de VHL 1.x vers VHL 2.x est simple, grâce à la nouvelle version offrant des API simplifiées pour l’initialisation, la configuration et les délégués de lecteur.

Voici les différences principales entre les versions 1.x et 2.x :

* **Modules complémentaires, délégués** : Vous n’avez plus besoin de mettre en œuvre des modules externes et des délégués pour Analytics, VideoPlayer et Heartbeat.
* **Configuration** : Vous n’avez plus besoin d’instancier des configurations pour les modules complémentaires 1.x.

## Avantages de la version 2.x {#benefits-of-two-x}

* Toutes les méthodes publiques sont consolidées dans la classe `MediaHeartbeat` pour faciliter la mise en œuvre par les développeurs.
* Toutes les configurations sont désormais consolidées dans la classe `MediaHeartbeatConfig`.
* Vous n’avez plus besoin d’instancier des configurations pour les modules complémentaires Analytics, VideoPlayer et Heartbeat. Il vous suffit d’instancier la classe `MediaHeartbeat` avec les instances `MediaHeartbeatDelegate` et `MediaHeartbeatConfig`. Il s’agit de la seule mise en œuvre nécessaire pour initialiser Media Analytics.

   Suite à l’initialisation de `MediaHeartbeat`, vous pouvez supprimer la mise en œuvre des modules Analytics, VideoPlayer et Heartbeat en toute sécurité. Supprimez également la mise en œuvre existante pour l’initialisation qui utilise divers modules en tant qu’entrée. Vous pouvez afficher des comparaisons côte à côte des mises en œuvre 1.x et 2.x dans la rubrique [Comparaison de code : 1.x vers 2.x](./code-comparison-1x-2x.md)..

Les nouvelles API de la version 2.x sont décrites en détail ici : [Conversion 1.x vers 2.x de l’API.](./1x-2x-api-change.md)
