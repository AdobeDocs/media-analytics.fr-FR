---
title: Mise en oeuvre de médias en flux continu pour Adobe Analytics ou Customer Journey Analytics
description: Découvrez les chemins d’implémentation de Streaming Media.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: 355b3b079d53ae8e83822f61fc79e60e47f6d715
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 13%

---

# Implémentation de Streaming Media for Adobe Analytics ou Customer Journey Analytics

Il existe plusieurs façons de mettre en oeuvre les médias en flux continu. Pour une comparaison détaillée des appareils et plateformes pris en charge pour les méthodes d’implémentation décrites sur cette page, voir [Périphériques et plateformes pris en charge](/help/getting-started/supported-devices.md).

## Méthodes de mise en oeuvre Edge

Dans la plupart des cas, il est recommandé d’utiliser Edge lors de la mise en oeuvre de Media Analytics pour tous les nouveaux clients Adobe Analytics ou Customer Journey Analytics.

* **Media for Edge Network SDK/Extension :** Collecte des données à partir des appareils iOS et Android et les envoie à Edge. Les données peuvent ensuite être envoyées à Customer Journey Analytics ou à Adobe Analytics.

  Pour plus d’informations sur le SDK/l’extension Media for Edge Network, voir [Installation de Media Analytics avec Experience Platform Edge](/help/implementation/implementation-edge.md).

  >[!NOTE]
  >
  >Cette méthode de mise en oeuvre ne prend actuellement pas en charge le SDK Web ou Roku. Toutefois, les deux sont pris en charge lors de l’implémentation avec l’API Media Edge.

* **API Media Edge :** Peut être personnalisé pour collecter des données à partir de n’importe quel appareil ou format (y compris les appareils mobiles, web et de bureau) et envoyer des données à Edge. Les données peuvent ensuite être envoyées à Customer Journey Analytics ou à Adobe Analytics.

  <!-- For more information about the Media Edge API, see (link to John's docs when they're ready) -->

![Workflow CJA](assets/cja-implementation.png)

## Autres méthodes de mise en oeuvre

Dans la plupart des cas, les méthodes d’implémentation Edge décrites ci-dessus sont recommandées pour Customer Journey Analytics et Adobe Analytics, en particulier pour les nouvelles implémentations.

Outre les méthodes de mise en oeuvre Edge, d’autres méthodes de mise en oeuvre sont disponibles. Ces méthodes d’implémentation ont été initialement conçues pour être utilisées avec Adobe Analytics. Cependant, les clients qui utilisent l’une des méthodes de mise en oeuvre suivantes peuvent toujours rendre les données disponibles dans Customer Journey Analytics en créant une [Connexion source Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html?lang=fr).

* **Extension Media avec des balises :** L’extension Adobe Medium Analytics for Audio and Video permet d’ajouter l’instance de suivi Media à un site ou à un projet prenant en charge les balises. Les données sont envoyées à Adobe Analytics.

  Pour plus d’informations sur l’installation, la configuration et la mise en oeuvre de Media Extension avec des balises, voir [Présentation de l’extension Adobe Medium Analytics (SDK 3.x) for Audio and Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html).

* **SDK Media :**  Les données sont envoyées à Adobe Analytics.

  Pour obtenir de plus amples informations sur le téléchargement et l’installation des SDK Media et des extensions, consultez [Obtention des SDK Media, des extensions à l’aide de balises et des SDK OTT](/help/getting-started/download-sdks.md).

* **API Media Collection :** Effectuez le suivi des événements audio et vidéo à l’aide d’appels HTTP RESTful. Les données sont envoyées à Adobe Analytics.

  Pour obtenir de plus amples informations sur l’utilisation des API Media Collection, consultez [API Media Collection](media-collection-api/mc-api-overview.md).


![Processus Analytics](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->
