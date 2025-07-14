---
title: Conditions préalables pour les implémentations Adobe Analytics uniquement
description: Découvrez les conditions préalables requises pour utiliser Streaming Media Collection avec des implémentations Adobe Analytics uniquement ou des implémentations Edge
feature: Streaming Media, Workspace Basics
role: User, Admin, Data Engineer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
source-git-commit: 0b0b4a373b15191dcb37dc436413f68cdc70768e
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 10%

---

# Conditions préalables pour les implémentations Edge

Les conditions préalables décrites dans cette section sont spécifiques à l’implémentation d’Adobe Streaming Media Collection avec les implémentations Edge.

1. **Remplir les conditions préalables générales**<br>
Que vous implémentiez Streaming Media Collection pour des implémentations Adobe Analytics uniquement ou pour des implémentations Edge, assurez-vous de respecter les [ conditions préalables générales ](/help/getting-started/prereqs.md).

1. **Confirmez que vous mettez en œuvre une solution Adobe compatible avec Edge Network et la collection Streaming Media**<br>
Lors de l’implémentation de Streaming Media Collection avec Edge, vous devez également disposer d’une implémentation Customer Journey Analytics, Adobe Analytics, Adobe Journey Optimizer ou Real-Time Customer Data Platform fonctionnelle. Consultez les ressources de documentation suivantes pour plus d’informations :
   * [Guide de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=fr)
   * [Mise en œuvre d’Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=fr)
   * [Documentation Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=fr)
   * [Documentation Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=fr)

1. **Obtenir l’URL du serveur de suivi multimédia**<br>
Demandez à votre représentant Customer Journey Analytics l’URL du serveur de suivi multimédia. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Implémenter Streaming Media Collection à l’aide d’Edge Network**<br>
Suivez les étapes de la section [Implémentation de la collection Streaming Media à l’aide d’Edge Network](/help/implementation/edge/implementation-edge.md).
