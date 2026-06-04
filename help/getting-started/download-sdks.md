---
title: Liens d’accès au téléchargement des SDK Media Analytics
description: Liens vers les téléchargements du SDK pour les plateformes disponibles, dont Android, iOS, JavaScript, Chromecast et Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/-L2tSDNue-GheYE-krKkpnOh05s5GKZZBz5sFXsBJ3I
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c77ba355-6681-41fe-b719-563d3f507fdbid: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 524
ht-degree: 81%

---

# Obtention des SDK Media, des extensions à l’aide des balises et des SDK OTT {#download-sdks}

Les informations de cette page comprennent des liens permettant de télécharger les SDK Media actuels et d’obtenir les extensions Media utilisant des balises.

Les balises dans Adobe Experience Platform constituent la nouvelle génération de fonctionnalités de gestion de SDK mobiles et de balises de sites web d’Adobe. Les balises offrent un moyen simple de déployer et de gérer toutes les solutions d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes. Pour plus d’informations sur les balises, voir la [présentation des balises](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=fr).

## SDK Media et bibliothèques mobiles {#media-sdks-libraries}

### Implémentation web {#download-web-sdk}

| Plateforme prise en charge | Solutions prises en charge | Méthode de mise en œuvre | Version |  API   |  Documentation  |  Exemple  |
|:---:|---|---|---|---| ---| ---|
| ![Icône JavaScript ](assets/javascript-icon.png)</br>**API JavaScript** | Adobe Analytics | Analytics uniquement | Web - [SDK Media pour JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [Référence de l’API JavaScript](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/APIReference.md) | [Configuration de JavaScript pour les médias en flux continu](/help/implementation/analytics-only/javascript.md) | [Exemple de SDK Media pour JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![Icône JavaScript ](assets/javascript-icon.png)</br>**API JavaScript** | Adobe Analytics | Analytics uniquement | Web - Extension Media |  | [Extension Adobe Media Analytics (SDK 3.x) for Audio and Video - à l’aide des balises (collecte de données)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=fr) | [Exemple d’extension Adobe Media Analytics (SDK 3.x) for Audio and Video](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| </br>**Web** | Adobe Analytics<p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Web - Experience Platform Edge |  | [Présentation de l’implémentation d’](/help/implementation/edge/overview.md) <p>et</p><p>[Configurer le SDK web pour les médias en flux continu](/help/implementation/edge/web-sdk.md)</p> | |

### Implémentation mobile {#get-mobile-extension}

| Plateforme prise en charge | Solutions prises en charge | Méthode de mise en œuvre | Version |  Documentation   |  Exemples  |
|:---:|---|---|---|---|---|
| ![icône Android ](assets/android-icon.png)</br>**Android** | Adobe Analytics | Analytics uniquement | Android - Extension Media | [Documentation sur le SDK mobile](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Exemple Media Analytics for Audio and Video](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Icône Apple iOS ](assets/ios-icon.png)<br>**tvOS** | Adobe Analytics | Analytics uniquement | iOS/tvOS - Extension Media | [Documentation sur le SDK mobile](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Exemple Media Analytics for Audio and Video](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| ![icône Android ](assets/android-icon.png)</br>**Android** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Android - Experience Platform Edge | [Configuration d’Android pour les médias en flux continu](/help/implementation/edge/android.md) | |
| ![Icône Apple iOS ](assets/ios-icon.png)<br>**tvOS** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | iOS/tvOS - Experience Platform Edge | [Configuration d’iOS pour les médias en flux continu](/help/implementation/edge/ios.md) |  |

### Implémentation over-the-top {#download-ott-libraries}

| Plateforme prise en charge | Solutions prises en charge | Méthode de mise en œuvre | Version |  API   |  Documentation  |
|:---:|---|---|---|---|---|
| ![icône Chromecast ](assets/chromecast-icon.png)</br>**Chromecast** | Adobe Analytics | Analytics uniquement | [SDK pour Chromecast v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Référence de l’API Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [Configuration de Chromecast SDK](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/docs/2.x/chromecast-setup.md) |
| ![icône Roku ](assets/roku-icon.png)</br>**Roku** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku/tree/main) |  | [Configuration de Roku pour les médias en flux continu](/help/implementation/edge/roku.md) |
