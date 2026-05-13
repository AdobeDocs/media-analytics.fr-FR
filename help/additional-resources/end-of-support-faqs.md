---
title: En savoir plus sur les FAQ relatives à l’abandon de la prise en charge du SDK Media Analytics
description: Cette rubrique comprend des questions fréquentes concernant l’abandon de la prise en charge des SDK Media Analytics.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/qfM2-x6s-SPf4gw2FpLlg7mPI-h-xZ3Y1TeeVALn3fQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c77ba355-6681-41fe-b719-563d3f507fdbid: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 639
ht-degree: 61%

---

# FAQ sur l’abandon de la prise en charge de Media Analytics Mobile SDK

Avec la fin de la prise en charge des SDK mobiles version 4 le 31 août 2021, Adobe a également arrêté la prise en charge des SDK Media Analytics Mobile pour iOS et Android. (Cela n’inclut pas les plateformes SDK for web (JS) et OTT de Media Analytics telles que Chromecast et Roku, qui sont toujours prises en charge.)

Cela signifie qu’Adobe ne fournit plus de correctifs, de mises à jour liées au système d’exploitation ni de prise en charge de Media Analytics Mobile SDK. Lors de la migration vers les nouveaux SDK Experience Platform, sachez que les [ extensions Media Analytics ](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) doivent être mises en œuvre pour activer les services de médias en flux continu Adobe.


## 5 choses à savoir

1. Les SDK Mobile v4 ne sont plus pris en charge à compter du 31 août 2021. Vous devez migrer vers les SDK mobiles Adobe Experience Platform (AEP) pour iOS et Android.

1. Une mise en œuvre Adobe de services de streaming multimédia nécessite le SDK Mobile AEP et l’utilisation des extensions Analytics et Media Analytics. Depuis le 1er septembre 2021, vous devez utiliser les nouveaux SDK et extensions AEP Mobile.  Les extensions Media Analytics sont configurées à l’aide des balises Adobe (collecte de données). Pour plus d’informations, voir [Migration du SDK Media autonome vers Adobe Launch](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md).

1. Le développement des fonctionnalités des SDK Media Analytics pour iOS et Android est terminé. Les nouvelles fonctionnalités introduites à partir de l’automne 2019 sont activées à l’aide des extensions Media Analytics et de l’API Media Collection.

1. Les SDK Roku et Chromecast restent disponibles pour les clients avec le module complémentaire Adobe Analytics for Streaming Media et le module complémentaire Customer Journey Analytics Streaming Media Collection. Les SDK Roku et Chromecast continueront d’être améliorés et pris en charge en tant que SDK autonomes. Si vous utilisez le SDK JS pour Media Analytics, vous pouvez continuer à utiliser le SDK autonome ou activer l’extension Media Analytics à l’aide d’Adobe Data Collection (autrefois Adobe Launch).

Pour toute question, veuillez contacter l’équipe chargée de votre compte Adobe.

## Questions fréquentes

1. **La prise en charge des SDK Roku et Chromecast sera-t-elle affectée ?&#x200B;**

   Non.  Pour le moment, les SDK Roku et Chromecast continueront à être pris en charge en tant que SDK autonomes&#x200B;
&#x200B;
1. **Les mises en œuvre du SDK Media Analytics pour JS seront-elles affectées par cette modification ?&#x200B;**

   Non.  Les clients qui utilisent JS SDK pour Media Analytics peuvent continuer à utiliser SDK ou l’activer via Adobe Launch.
&#x200B;
1. **Quel est le niveau d’effort demandé par la migration vers les extensions Media Analytics ?&#x200B;**

   Le niveau d’effort dépend de l’implémentation de chaque client et peut donc varier.  Après avoir consulté la documentation concernant la migration ci-dessous, rapprochez-vous du service de nos conseillers et/ou de l’assistance clientèle pour obtenir une assistance supplémentaire.

   [Extensions Media Analytics : migration sous Android](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)

   [Extensions Media Analytics : migration sous iOS](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)

   [Extensions Media Analytics : nouvelles mises en œuvre](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

1. **Dois-je configurer Launch en tant que système de gestion des balises ? Que se passe-t-il si je ne souhaite pas utiliser Launch ?**

   Dans le cas de l’utilisation d’applications mobiles, Launch n’est pas employé en tant que système de gestion des balises comme c’est le cas pour le web. L’utilisation de l’interface utilisateur de Launch est requise pour configurer les extensions du SDK. Cette utilisation est similaire à celle de l’interface utilisateur d’Adobe Mobile Services pour configurer le SDK mobile v4. L’utilisation de Launch pour l’installation a pour avantage de proposer des instructions d’installation personnalisées selon l’extension choisie.

1. **Cet abandon de la prise en charge a-t-il une incidence sur le SDK pour tvOS ?**

   Oui : pour tvOS (version 10+), il est recommandé de migrer vers les extensions Media Analytics. Pour plus d’informations, voir [Migration du SDK Media autonome vers Adobe Launch — iOS](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md).

1. **Cet abandon de la prise en charge a-t-il une incidence sur le SDK pour Fire TV et Android TV ?**

   Oui : pour Fire TV et Android TV, il est recommandé de migrer vers les extensions Media Analytics. Pour plus d’informations, voir [Migration du SDK Media autonome vers Adobe Launch - Android](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md).
