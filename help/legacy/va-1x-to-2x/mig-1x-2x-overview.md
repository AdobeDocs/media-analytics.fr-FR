---
title: Présentation de la migration
description: Découvrez comment migrer des versions 1.x vers les versions 2.x du SDK Media.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 87%

---

# Présentation de la migration héritée : VHL 1.x vers VHL 2.x {#migration-overview}

La migration de VHL 1.x vers VHL 2.x est simple grâce à la nouvelle version qui offre des API simplifiées pour l’initialisation, la configuration et les délégués de lecteur.

Voici les différences principales entre les versions 1.x et 2.x :

* **Modules externes, délégués -** vous n’avez plus besoin d’implémenter de modules externes et de délégués pour Analytics, VideoPlayer et Heartbeat.
* **Configuration -** Vous n’avez plus besoin d’instancier les configurations pour les modules externes 1.x.

## Avantages de la version 2.x {#benefits-of-two-x}

* Toutes les méthodes publiques sont consolidées dans la classe `MediaHeartbeat` pour faciliter la mise en œuvre par les développeurs.
* Toutes les configurations sont désormais consolidées dans la classe `MediaHeartbeatConfig`.
* Vous n’avez plus besoin d’instancier des configurations pour les modules complémentaires Analytics, VideoPlayer et Heartbeat. Il vous suffit d’instancier la classe `MediaHeartbeat` avec les instances `MediaHeartbeatDelegate` et `MediaHeartbeatConfig`. Il s’agit de la seule mise en œuvre nécessaire pour initialiser Media Analytics.

  Suite à l’initialisation de `MediaHeartbeat`, vous pouvez supprimer la mise en œuvre des modules Analytics, VideoPlayer et Heartbeat en toute sécurité. Supprimez également la mise en œuvre existante pour l’initialisation qui utilise divers modules en tant qu’entrée. Vous pouvez afficher des comparaisons côte à côte des mises en œuvre 1.x et 2.x dans la rubrique [Comparaison de code : 1.x vers 2.x](./code-comparison-1x-2x.md)..

Les nouvelles API de la version 2.x sont décrites en détail ici : [Conversion 1.x vers 2.x de l’API.](./1x-2x-api-change.md)
