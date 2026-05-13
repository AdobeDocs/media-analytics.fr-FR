---
title: Conditions préalables pour les implémentations Adobe Analytics uniquement
description: Découvrez les conditions préalables requises pour utiliser Streaming Media Collection avec des implémentations Adobe Analytics uniquement ou des implémentations Edge
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
TQID: https://experienceleague.adobe.com/OqimGafihuirpnAaZ4AvrX2lrOmCtr0FLXk3QwoVTew
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 212
ht-degree: 19%

---

# Conditions préalables pour les implémentations Edge

Les conditions préalables décrites dans cette section sont spécifiques à l’implémentation d’Adobe Streaming Media Collection avec les implémentations Edge.

1. **Remplir les conditions préalables générales**<br>
Que vous implémentiez Streaming Media Collection pour des implémentations Adobe Analytics uniquement ou pour des implémentations Edge, assurez-vous de respecter les [&#x200B; conditions préalables générales &#x200B;](/help/getting-started/prereqs.md).

1. **Confirmez que vous mettez en œuvre une solution Adobe compatible avec Edge Network et la collection Streaming Media**<br>
Lors de l’implémentation de Streaming Media Collection avec Edge, vous devez également disposer d’une implémentation Customer Journey Analytics, Adobe Analytics, Adobe Journey Optimizer ou Real-Time Customer Data Platform fonctionnelle. Consultez les ressources de documentation suivantes pour plus d’informations :
   * [Guide de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=fr)
   * [Mise en œuvre d’Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=fr)
   * [Documentation de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=fr)
   * [Documentation de Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=fr)

1. **Obtenir l’URL du serveur de suivi multimédia**<br>
Demandez à votre représentant Customer Journey Analytics l’URL du serveur de suivi multimédia. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Implémentation de Streaming Media Collection à l’aide d’Edge Network**<br>
Suivez les étapes de la section [Implémentation de la collection Streaming Media à l’aide d’Edge Network](/help/implementation/edge/implementation-edge.md).
