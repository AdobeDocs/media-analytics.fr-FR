---
title: Liens d’accès au téléchargement des SDK Media Analytics
description: Liens vers les téléchargements du SDK pour les plateformes disponibles, dont Android, iOS, JavaScript, Chromecast et Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/-L2tSDNue-GheYE-krKkpnOh05s5GKZZBz5sFXsBJ3I
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 571
ht-degree: 84%

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
| ![Icône JavaScript &#x200B;](assets/javascript-icon.png)</br>**API JavaScript** | Adobe Analytics | Analytics uniquement | Web - [SDK Media pour JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [Référence de l’API JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [Installation de Media SDK à l’aide de JavaScript](/help/implementation/media-sdk/setup/web-implementation.md) | [Exemple de SDK Media pour JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![Icône JavaScript &#x200B;](assets/javascript-icon.png)</br>**API JavaScript** | Adobe Analytics | Analytics uniquement | Web - Extension Media |  | [Extension Adobe Media Analytics (SDK 3.x) for Audio and Video - à l’aide des balises (collecte de données)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=fr) | [Exemple d’extension Adobe Media Analytics (SDK 3.x) for Audio and Video](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| </br>**Web** | Adobe Analytics<p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Web - Experience Platform Edge |  | [Implémenter la collection de médias en flux continu Customer Journey Analytics à l’aide d’Edge Network](/help/implementation/edge/implementation-edge.md) <p>and</p><p>[Envoi de données web vers Edge avec Adobe Experience Platform Web SDK](/help/implementation/edge/edge-web-sdk.md)</p> | |

### Implémentation mobile {#get-mobile-extension}

| Plateforme prise en charge | Solutions prises en charge | Méthode de mise en œuvre | Version |  Documentation   |  Exemples  |
|:---:|---|---|---|---|---|
| ![icône Android &#x200B;](assets/android-icon.png)</br>**Android** | Adobe Analytics | Analytics uniquement | Android - Extension Media | [Documentation sur le SDK mobile](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Exemple Media Analytics for Audio and Video](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Icône Apple iOS &#x200B;](assets/ios-icon.png)<br>**tvOS** | Adobe Analytics | Analytics uniquement | iOS/tvOS - Extension Media | [Documentation sur le SDK mobile](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Exemple Media Analytics for Audio and Video](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| ![icône Android &#x200B;](assets/android-icon.png)</br>**Android** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Android - Experience Platform Edge | [Installation de Media SDK à l’aide de JavaScript](/help/implementation/edge/implementation-edge.md) | |
| ![Icône Apple iOS &#x200B;](assets/ios-icon.png)<br>**tvOS** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | iOS/tvOS - Experience Platform Edge | [Installation de Media SDK à l’aide de JavaScript](/help/implementation/edge/implementation-edge.md) |  |

### Implémentation over-the-top {#download-ott-libraries}

| Plateforme prise en charge | Solutions prises en charge | Méthode de mise en œuvre | Version |  API   |  Documentation  |
|:---:|---|---|---|---|---|
| ![icône Chromecast &#x200B;](assets/chromecast-icon.png)</br>**Chromecast** | Adobe Analytics | Analytics uniquement | [SDK pour Chromecast v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Référence de l’API Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [Configuration du SDK Mobile v3.x pour Chromecast](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![icône Roku &#x200B;](assets/roku-icon.png)</br>**Roku** | Adobe Analytics | Analytics uniquement | [SDK pour Roku v2.2.6](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) |  | [Configuration du SDK Mobile v2.x pour Roku](/help/implementation/media-sdk/setup/set-up-roku.md) |
| ![icône Roku &#x200B;](assets/roku-icon.png)</br>**Roku** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku/tree/main) |  | [Installation de Media SDK à l’aide de JavaScript](/help/implementation/edge/implementation-edge.md) |
