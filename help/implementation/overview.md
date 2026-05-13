---
title: Mise en œuvre de services de streaming multimédia pour Adobe Analytics ou Customer Journey Analytics
description: Découvrez les chemins d’implémentation des services de streaming multimédia d’Adobe.
uuid: null
feature: Streaming Media
role: User, Admin, Developer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
TQID: https://experienceleague.adobe.com/aFrxbzBLlf1ngetaM-GsNFXz6TUXi6Pic3quLVI297c
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c8add8f2-4250-4fd9-9cde-9707036c567did: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 522
ht-degree: 65%

---

# Mise en œuvre de services de streaming multimédia pour Adobe Analytics ou Customer Journey Analytics

Il existe différentes manières de mettre en œuvre les services de streaming multimédia d’Adobe. Pour une comparaison détaillée des appareils et plateformes pris en charge pour les méthodes d’implémentation décrites sur cette page, consultez [Appareils et plateformes pris en charge](/help/getting-started/supported-devices.md).

## Méthodes d’implémentation Edge

Nous vous recommandons d’utiliser Edge lors de la mise en œuvre des services de médias en flux continu pour tous les nouveaux clients Adobe Analytics ou Customer Journey Analytics.

Les méthodes d’implémentation d’Edge utilisent le module complémentaire Streaming Media Collection.

* **Media pour Edge Network SDK/Extension :** collecte des données à partir d’appareils web, iOS et Android, ou d’appareils Roku, et les envoie à Edge Network. Les données peuvent ensuite être envoyées à Customer Journey Analytics ou à Adobe Analytics.

  Pour plus d’informations sur l’extension Media for Edge Network SDK, voir [ Implémentation de la collection Streaming Media à l’aide d’Edge Network](/help/implementation/edge/implementation-edge.md).

* **API Media Edge :** peut être personnalisé pour collecter des données à partir de n’importe quel appareil ou format (y compris, mobile, web et appareils par contournement) et envoyer des données à Edge Network. Les données peuvent ensuite être envoyées à Customer Journey Analytics ou à Adobe Analytics.

  Pour plus d’informations sur l’API Media Edge, voir [Présentation de l’API Media Edge](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/).

![Workflow CJA](assets/streaming-media-edge.png)

## Méthodes d’implémentation Adobe Analytics uniquement

Les méthodes d’implémentation Edge décrites ci-dessus sont recommandées pour Customer Journey Analytics et Adobe Analytics, en particulier pour les nouvelles implémentations.

Outre les méthodes d’implémentation Edge, d’autres sont disponibles. Ces méthodes d’implémentation ont été conçues pour être utilisées avec Adobe Analytics. Cependant, la clientèle existante qui dispose de l’une des méthodes d’implémentation suivantes peut toujours rendre les données disponibles dans Customer Journey Analytics en créant une [connexion source Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html?lang=fr).

Les méthodes d’implémentation réservées à Adobe Analytics utilisent le module complémentaire Adobe Analytics for Streaming Media.

* **Extension Media avec des balises :** l’extension Adobe Media Analytics for Audio and Video permet d’ajouter l’instance de suivi Media à un site ou à un projet prenant en charge les balises. Les données sont envoyées à Adobe Analytics.

  Pour plus d’informations sur l’installation, la configuration et l’implémentation de l’extension Media avec des balises, consultez [Présentation de l’extension Adobe Media Analytics (SDK 3.x) for Audio and Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html?lang=fr).

* **SDK Media :** le SDK Media vous permet de mesurer plusieurs plateformes multimédias, notamment des sites web, des téléphones mobiles, des télévisions connectées, des tablettes, des appareils OTT, des décodeurs et des consoles de jeux. (Pour plus d’informations, consultez [Appareils et plateformes pris en charge](/help/getting-started/supported-devices.md).)

  Les SDK Media utilisent les API Media Collection pour effectuer le suivi. Les données sont envoyées à Adobe Analytics.

  Pour obtenir des informations sur le téléchargement et l’installation des SDK Media et des extensions, consultez [Obtention des SDK Media, des extensions à l’aide de balises et des SDK OTT](/help/getting-started/download-sdks.md).

* **API Media Collection :** les API Media Collection pouvant être personnalisées, elles peuvent être utilisées pour les applications nécessitant des fonctionnalités de suivi personnalisées et pour les appareils non pris en charge par les SDK Media. Les API Media Collection effectuent le suivi des événements audio et vidéo à l’aide d’appels HTTP RESTful. Les données sont envoyées à Adobe Analytics.

  Pour obtenir des informations sur l’utilisation des API Media Collection, consultez [API Media Collection](media-collection-api/mc-api-overview.md).


![Workflow Analytics](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->
