---
title: Présentation de la migration
description: Découvrez comment migrer des versions 1.x vers les versions 2.x du SDK Media.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/mM6vZFyx6BG5MZXrzOc5hkBM6pOdzBCLiSL3WgON9LU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c8add8f2-4250-4fd9-9cde-9707036c567did: e992d880-33bc-4949-a648-aa7d410276cd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 235
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
