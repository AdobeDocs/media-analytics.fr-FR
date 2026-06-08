---
title: Obtention des SDK Media, des extensions et des API
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
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 625
ht-degree: 30%

---

# Obtention des SDK Media, des extensions et des API

## Implémentations d’Edge (recommandé) {#edge-sdks}

Les implémentations d’Edge collectent des données une seule fois et les diffusent via Adobe Experience Platform Edge Network vers plusieurs destinations : Adobe Analytics, Customer Journey Analytics, Adobe Journey Optimizer et Real-Time CDP. Pour les plateformes sans SDK natif (telles que les Smart TV, les consoles de jeux et les décodeurs), utilisez l’API Media Edge.

| | Documentation | Exemple |
|:---:|---|---|
| [![Icône &#x200B;](assets/javascript-icon.png)](https://experienceleague.adobe.com/fr/docs/experience-platform/web-sdk/install/overview)<br>[Web SDK](https://experienceleague.adobe.com/fr/docs/experience-platform/web-sdk/install/overview) | [Configurer le SDK web pour les médias en flux continu](/help/implementation/edge/web-sdk.md) | [Exemple](https://github.com/adobe/alloy-samples/blob/main/media-collection/STANDALONE.md) |
| [![Icône d’extension](assets/plug.svg)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/web-sdk/overview.html?lang=fr)<br>[extension de balise Web SDK](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/web-sdk/overview.html?lang=fr) | [Configurer l’extension de balise Web SDK pour les médias en flux continu](/help/implementation/edge/web-sdk-tags.md) | [Exemple](https://github.com/adobe/alloy-samples/blob/main/media-collection/TAGS_IMPL.md) |
| [![Icône &#x200B;](assets/android.png)](https://github.com/adobe/aepsdk-media-android)<br>[Android SDK](https://github.com/adobe/aepsdk-media-android) | [Configuration d’Android pour les médias en flux continu](/help/implementation/edge/android.md) | [Exemple](https://github.com/adobe/aepsdk-media-android/tree/main/code/testapp) |
| [![Icône Apple iOS](assets/apple.png)](https://github.com/adobe/aepsdk-media-ios)<br>[iOS / tvOS SDK](https://github.com/adobe/aepsdk-media-ios) | [Configuration d’iOS pour les médias en flux continu](/help/implementation/edge/ios.md) | [Exemple](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| [![Icône d’extension](assets/plug.svg)](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)<br>[Extension de balise Android](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Configurer l’extension de balise Android pour les médias en flux continu](/help/implementation/edge/android-tags.md) | |
| [![Icône d’extension](assets/plug.svg)](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)<br>[Extension de balise iOS/tvOS](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Configurer l’extension de balise iOS pour les médias en flux continu](/help/implementation/edge/ios-tags.md) | |
| [![icône Roku](assets/roku-icon.png)](https://github.com/adobe/aepsdk-roku)<br>[SDK Edge Roku](https://github.com/adobe/aepsdk-roku) | [Configuration de Roku Edge pour les médias en flux continu](/help/implementation/edge/roku.md) | [Exemple](https://github.com/adobe/aepsdk-roku/tree/main/sample/simple-videoplayer-channel) |
| [![Icône API](assets/api.png)](https://developer.adobe.com/data-collection-apis/docs/api/media-edge)<br>[API Media Edge](https://developer.adobe.com/data-collection-apis/docs/api/media-edge) | [Configurer l’API Media Edge](/help/implementation/edge/media-edge-api.md) | [Exemple](https://developer.adobe.com/data-collection-apis/docs/getting-started/media-edge-examples) |

## Implémentations Analytics uniquement {#analytics-only-sdks}

Ces SDK et extensions envoient directement des données à Adobe Analytics. Pour les nouvelles mises en œuvre, utilisez les mises en œuvre d’Edge ci-dessus. Pour importer des données Analytics existantes dans Customer Journey Analytics ou d’autres applications Experience Platform, utilisez le [connecteur source Analytics](https://experienceleague.adobe.com/fr/docs/experience-platform/sources/connectors/adobe-applications/analytics).

| | Documentation | Exemple |
|:---:|---|---|
| [![Icône &#x200B;](assets/javascript-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2)<br>[Media SDK 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [Configuration de JavaScript pour les médias en flux continu](/help/implementation/analytics-only/javascript.md) | [Exemple](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| [![Icône d’extension](assets/plug.svg)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=fr)<br>[Extension Media](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=fr) | [Configuration de JavaScript à l’aide de balises pour les médias en flux continu](/help/implementation/analytics-only/javascript-tags.md) | [Exemple](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| [![Icône Chromecast](assets/chromecast-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3)<br>[Chromecast SDK 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Configurer Chromecast pour les médias en flux continu](/help/implementation/analytics-only/chromecast.md) | [Exemple](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/chromecast/samples/BasicPlayerSample) |
| [![Icône Roku](assets/roku-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.7)<br>[Roku SDK 2.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.7) | [Configuration de Roku 2.x pour les médias en flux continu](/help/implementation/analytics-only/roku-2x.md) | [Exemple](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/roku/samples) |
| [![Icône API](assets/api.png)](/help/implementation/media-collection-api/mc-api-overview.md)<br>[API Media Collection](/help/implementation/media-collection-api/mc-api-overview.md) | [Configurer l’API Media Collection](/help/implementation/analytics-only/media-collection-api.md) | |
