---
title: Liens d’accès au téléchargement des SDK Media Analytics
description: Liens vers les téléchargements du SDK pour les plateformes disponibles, dont Android, iOS, JavaScript, Chromecast et Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 81%

---

# Obtention des SDK Media, des extensions à l’aide des balises et des SDK OTT {#download-sdks}

Les informations de cette page comprennent des liens permettant de télécharger les SDK Media actuels et d’obtenir les extensions Media utilisant des balises.

Les balises dans Adobe Experience Platform constituent la nouvelle génération de fonctionnalités de gestion de SDK mobiles et de balises de sites web d’Adobe. Les balises offrent un moyen simple de déployer et de gérer toutes les solutions d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes. Pour plus d’informations sur les balises, voir la [présentation des balises](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=fr).


>[!NOTE]
>
>Pour plus d’informations sur le téléchargement des SDK hérités, voir [Hérité - Téléchargement de SDK](/help/legacy/legacy-download-sdks.md).<br>
>Pour obtenir des informations importantes sur la fin de la prise en charge, voir les [FAQ sur la fin de la prise en charge](/help/additional-resources/end-of-support-faqs.md).

## SDK Media et bibliothèques mobiles {#media-sdks-libraries}

### Implémentation web {#download-web-sdk}

| Plateforme prise en charge | Solutions prises en charge | Méthode de mise en œuvre | Version |  API   |  Documentation  |  Exemple  |
|:---:|---|---|---|---| ---| ---|
| ![Icône JavaScript ](assets/javascript-icon.png)</br>**API JavaScript** | Adobe Analytics | Analytics uniquement | Web - [SDK Media pour JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [Référence de l’API JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [Installation du SDK Media à l’aide de JavaScript](/help/implementation/media-sdk/setup/web-implementation.md) | [Exemple de SDK Media pour JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![Icône JavaScript ](assets/javascript-icon.png)</br>**API JavaScript** | Adobe Analytics | Analytics uniquement | Web - Extension Media |  | [Extension Adobe Media Analytics (SDK 3.x) for Audio and Video - à l’aide des balises (collecte de données)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=fr) | [Exemple d’extension Adobe Media Analytics (SDK 3.x) for Audio and Video](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| </br>**Web** | Adobe Analytics<p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Web - Experience Platform Edge |  | [Implémentation du module complémentaire de collecte de médias en flux continu à l’aide de l’Edge Network](/help/implementation/edge/implementation-edge.md) <p>et</p><p>[Envoi de données Web à Edge avec le SDK Web Adobe Experience Platform](/help/implementation/edge/edge-web-sdk.md)</p> | |

### Implémentation mobile {#get-mobile-extension}

| Plateforme prise en charge | Solutions prises en charge | Méthode de mise en œuvre | Version |  Documentation  |  Exemples  |
|:---:|---|---|---|---|---|
| ![Icône Android ](assets/android-icon.png)</br>**Android** | Adobe Analytics | Analytics uniquement | Android - Extension Media | [Documentation sur le SDK mobile](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Exemple Media Analytics for Audio and Video](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Icône Apple iOS ](assets/ios-icon.png)<br>**tvOS** | Adobe Analytics | Analytics uniquement | iOS/tvOS - Extension Media | [Documentation sur le SDK mobile](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Exemple Media Analytics for Audio and Video](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| ![Icône Android ](assets/android-icon.png)</br>**Android** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Android - Experience Platform Edge | [Installation du SDK Media à l’aide de JavaScript](/help/implementation/edge/implementation-edge.md) | |
| ![Icône Apple iOS ](assets/ios-icon.png)<br>**tvOS** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | iOS/tvOS - Experience Platform Edge | [Installation du SDK Media à l’aide de JavaScript](/help/implementation/edge/implementation-edge.md) |  |

### Implémentation over-the-top {#download-ott-libraries}

| Plateforme prise en charge | Solutions prises en charge | Méthode de mise en œuvre | Version |  API   |  Documentation  |
|:---:|---|---|---|---|---|
| ![Icône Chromecast ](assets/chromecast-icon.png)</br>**Chromecast** | Adobe Analytics | Analytics uniquement | [SDK pour Chromecast v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Référence de l’API Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [Configuration du SDK Mobile v3.x pour Chromecast](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![Icône Roku ](assets/roku-icon.png)</br>**Roku** | Adobe Analytics | Analytics uniquement | [SDK pour Roku v2.2.6](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) |  | [Configuration du SDK Mobile v2.x pour Roku](/help/implementation/media-sdk/setup/set-up-roku.md) |
| ![Icône Roku ](assets/roku-icon.png)</br>**Roku** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | [SDK Adobe Experience Platform Roku](https://github.com/adobe/aepsdk-roku/tree/main) |  | [Installation du SDK Media à l’aide de JavaScript](/help/implementation/edge/implementation-edge.md) |
