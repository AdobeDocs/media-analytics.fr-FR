---
title: Conditions préalables pour les implémentations Adobe Analytics uniquement
description: En savoir plus sur les conditions préalables à l’utilisation des médias en flux continu avec les mises en oeuvre d’Adobe Analytics uniquement
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 8a0f2c0b367b48ee5ac94e7fc6bcd0eadafbc5d8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 16%

---

# Conditions préalables pour les implémentations Edge

Les conditions préalables décrites dans cette section sont spécifiques à la mise en oeuvre de médias en flux continu avec des mises en oeuvre Edge.

1. **Remplir les conditions préalables générales**<br>
Que vous mettiez en oeuvre des médias en flux continu pour les mises en oeuvre d’Adobe Analytics uniquement ou pour les mises en oeuvre d’Edge, assurez-vous de respecter les conditions suivantes : [conditions préalables générales](/help/getting-started/prereqs.md).

1. **Confirmez que vous mettez en oeuvre une solution Adobe compatible avec Edge et Streaming Media.**<br>
Lors de l’implémentation de médias en flux continu avec Edge, vous devez également disposer d’un Customer Journey Analytics opérationnel, d’Adobe Analytics, de Adobe Journey Optimizer ou d’une implémentation Real-time Customer Data Platform. Pour plus d’informations, consultez les ressources de documentation suivantes :
   * [Guide de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=fr)
   * [Mise en œuvre d’Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=fr)
   * [Documentation Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=fr)
   * [Documentation Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=fr)

1. **Obtention de l’URL du serveur de suivi multimédia**<br>
Demandez à votre représentant Customer Journey Analytics l’URL du serveur de suivi multimédia. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Installation de Media Analytics avec Edge**<br>
Suivez les étapes décrites dans la section [Installation de Media Analytics avec Experience Platform Edge](/help/implementation/edge/implementation-edge.md).