---
title: Prise en main
description: Prise en main d’Adobe Analytics for Streaming Media.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 6%

---


# Prise en main {#getting-started}

Adobe Analytics for Streaming Media offre deux méthodes principales de mise en oeuvre, les SDK Media et les API Media Collection.

![methods](assets/getting-started2.png)

Utilisation de la logique intégrée de la variable **SDK Media**, vous pouvez mesurer avec précision plusieurs plateformes multimédias, notamment des sites web, des téléphones mobiles, des télévisions connectées, des tablettes, des appareils OTT, des décodeurs et des consoles de jeux. Vous pouvez même mesurer le contenu téléchargé. Les insights que vous obtenez vont profondément dans l’engagement de l’utilisateur à consulter, afin que vous puissiez comprendre combien de temps, quand et où les visiteurs s’engagent. Les SDK Media utilisent la variable **API Media Collection** pour le suivi. Les API Media Collection peuvent être personnalisées si votre application requiert des fonctionnalités de suivi personnalisées. Pour les appareils non pris en charge par les SDK Media, vous pouvez utiliser les API Media Collection.

La solution Adobe Analytics Streaming Media est fournie pour les plateformes multimédias suivantes :

* Web
* Mobile
* En haut
* Tout appareil connecté pouvant être utilisé pour la diffusion en continu de médias ou une intégration serveur à serveur

Pour plus d’informations, voir [Périphériques et plateformes pris en charge](#_Supported_devices_and).

>[!IMPORTANT]
>
>Pour mettre en oeuvre Adobe Analytics Streaming Media, contactez votre représentant commercial ou votre gestionnaire de compte Adobe pour vous assurer que Streaming Media fait partie de votre portefeuille de produits.

## SDK Media pour les médias en flux continu {#media-sdks}

Les SDK Media pour les médias en flux continu sont disponibles pour les plateformes JavaScript, Android, iOS, tvOS, Chromecast et Roku.

Pour plus d’informations sur le téléchargement et l’installation des SDK Media, voir [Obtention des SDK Media, des extensions à l’aide de balises et des SDK OTT](/help/getting-started/download-sdks.md).


## API Media Collection {#media-collection-apis}

Le **API Media Collection** vous permettent de personnaliser votre implémentation de media analytics. Utilisez les API Media Collection pour appeler directement les serveurs d’Adobe afin d’effectuer pratiquement toute action que vous pouvez effectuer à l’aide des SDK, etc. Personnalisez votre collecte de données afin de créer des rapports qui explorent vos données multimédia en flux continu, y obtiennent des informations ou répondent à des questions importantes.

Pour plus d’informations sur l’utilisation des API Media Collection, voir [Documentation de l’API de média dynamique](/help/implementation/media-collection-api/mc-api-overview.md).

## Extensions Adobe {#adobe-extensions}

>[!NOTE]
>
>INTRO REQUIS POUR LES EXTENSIONS

* Le [**Extension Adobe Medium Analytics for Audio and Video**](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=en) (Extension Media Analytics), est requis pour les mises en oeuvre d’iOS et de tvOS. Il permet d’ajouter l’instance de suivi à un site ou à un projet de balise. L’extension MA requiert également l’extension Analytics et l’extension d’ID Experience Cloud.

* [Extension Analytics v1.6 ou version ultérieure](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en): cette extension vous permet de charger la bibliothèque JavaScript du SDK Web de Adobe Experience Platform pour envoyer des données aux solutions Adobe.

* [Extension d’ID Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en): cette extension met en oeuvre le service d’identification des Experience Cloud qui identifie les visiteurs dans toutes les solutions Experience Cloud. Le service d’ID Experience Cloud est une extension de personnalisation de Adobe Experience Platform.
