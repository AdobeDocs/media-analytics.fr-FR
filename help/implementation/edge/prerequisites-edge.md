---
title: Conditions préalables pour les implémentations Adobe Analytics uniquement
description: En savoir plus sur les conditions préalables à l’utilisation du module complémentaire Collection de médias en flux continu avec les mises en oeuvre d’Adobe Analytics uniquement ou les mises en oeuvre d’Edge
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 10%

---

# Conditions préalables pour les implémentations Edge

Les conditions préalables décrites dans cette section sont spécifiques à la mise en oeuvre du module complémentaire Adobe de collecte de médias en flux continu avec les mises en oeuvre Edge.

1. **: remplir les conditions préalables générales**<br>
Que vous mettiez en oeuvre le module complémentaire de collecte de médias en flux continu pour les implémentations d’Adobe Analytics uniquement ou pour les implémentations d’Edge, assurez-vous de respecter les [conditions préalables générales](/help/getting-started/prereqs.md).

1. **Confirmez que vous mettez en oeuvre une solution d’Adobe compatible avec Edge Network et le module complémentaire de collecte de médias en flux continu**<br>
Lors de la mise en oeuvre du module complémentaire de collecte de médias en flux continu avec Edge, vous devez également disposer d’un Customer Journey Analytics opérationnel, d’Adobe Analytics, de Adobe Journey Optimizer ou d’une mise en oeuvre Real-Time Customer Data Platform. Pour plus d’informations, consultez les ressources de documentation suivantes :
   * [Guide de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=fr)
   * [Mise en œuvre d’Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=fr)
   * [Documentation Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=fr)
   * [Documentation Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=fr)

1. **Obtention de l’URL du serveur de suivi multimédia**<br>
Demandez à votre représentant Customer Journey Analytics l&#39;URL du serveur de suivi multimédia. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Implémentation du module complémentaire de collecte de médias en flux continu à l’aide de l’Edge Network**<br>
Suivez les étapes de la section [Mise en oeuvre du module complémentaire de collecte de médias en flux continu à l’aide de l’Edge Network](/help/implementation/edge/implementation-edge.md).
