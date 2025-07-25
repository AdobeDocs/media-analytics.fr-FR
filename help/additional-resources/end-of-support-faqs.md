---
title: En savoir plus sur les FAQ relatives à l’abandon de la prise en charge du SDK Media Analytics
description: Cette rubrique comprend des questions fréquentes concernant l’abandon de la prise en charge des SDK Media Analytics.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 75%

---

# FAQ sur l’abandon de la prise en charge de Media Analytics Mobile SDK

Avec la fin de la prise en charge des SDK mobiles version 4 le 31 août 2021, Adobe a également arrêté la prise en charge des SDK Media Analytics Mobile pour iOS et Android. (Cela n’inclut pas les plateformes SDK for web (JS) et OTT de Media Analytics telles que Chromecast et Roku, qui sont toujours prises en charge.)

Cela signifie qu’Adobe ne fournit plus de correctifs, de mises à jour liées au système d’exploitation ni de prise en charge de Media Analytics Mobile SDK. Lors de la migration vers les nouveaux SDK Experience Platform, sachez que les [ extensions Media Analytics ](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) doivent être mises en œuvre pour activer la collecte de médias en flux continu Adobe.


## 5 choses à savoir

1. Les SDK Mobile v4 ne sont plus pris en charge à compter du 31 août 2021. Vous devez migrer vers les SDK mobiles Adobe Experience Platform (AEP) pour iOS et Android.

1. La mise en œuvre d’Analytics for Streaming Media requiert le SDK mobile AEP ainsi que l’utilisation des extensions Analytics et Media Analytics. Depuis le 1er septembre 2021, vous devez utiliser les nouveaux SDK et extensions AEP Mobile.  Les extensions Media Analytics sont configurées à l’aide des balises Adobe (collecte de données). Pour plus d’informations, voir [Migration du SDK Media autonome vers Adobe Launch](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md).

1. Le développement des fonctionnalités des SDK Media Analytics pour iOS et Android est terminé. Les nouvelles fonctionnalités introduites à partir de l’automne 2019 sont activées à l’aide des extensions Media Analytics et de l’API Media Collection.

1. Les SDK Roku et Chromecast restent disponibles pour les clients d’Analytics for Streaming Media. Les SDK Roku et Chromecast continueront d’être améliorés et pris en charge en tant que SDK autonomes. Si vous utilisez le SDK JS pour Media Analytics, vous pouvez continuer à utiliser le SDK autonome ou activer l’extension Media Analytics à l’aide d’Adobe Data Collection (autrefois Adobe Launch).

Pour toute question, veuillez contacter l’équipe chargée de votre compte Adobe.

## Questions fréquentes

1. **La prise en charge des SDK Roku et Chromecast sera-t-elle affectée ?&#x200B;**

   Non.  Pour le moment, les SDK Roku et Chromecast continueront à être pris en charge en tant que SDK autonomes.
1. **Les mises en œuvre du SDK Media Analytics pour JS seront-elles affectées par cette modification ?&#x200B;**

   Non.  Les clients qui utilisent le SDK JS pour Media Analytics peuvent continuer à utiliser le SDK ou l’activer par le biais d’Adobe Launch.
&#x200B;
1. **Quel est le niveau d’effort demandé par la migration vers les extensions Media Analytics ?&#x200B;**

   Le niveau d’effort dépend de l’implémentation de chaque client et peut donc varier.  Après avoir consulté la documentation concernant la migration ci-dessous, rapprochez-vous du service de nos conseillers et/ou de l’assistance clientèle pour obtenir une assistance supplémentaire.

[Extensions Media Analytics : migration sous Android](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)

[Extensions Media Analytics : migration sous iOS](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)

   [Extensions Media Analytics : nouvelles mises en œuvre](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

1. **Dois-je configurer Launch en tant que système de gestion des balises ? Que se passe-t-il si je ne souhaite pas utiliser Launch ?**

   Dans le cas de l’utilisation d’applications mobiles, Launch n’est pas employé en tant que système de gestion des balises comme c’est le cas pour le web. L’utilisation de l’interface utilisateur de Launch est requise pour configurer les extensions du SDK. Cette utilisation est similaire à celle de l’interface utilisateur d’Adobe Mobile Services pour configurer le SDK mobile v4. L’utilisation de Launch pour l’installation a pour avantage de proposer des instructions d’installation personnalisées selon l’extension choisie.

1. **Cet abandon de la prise en charge a-t-il une incidence sur le SDK pour tvOS ?**

   Oui : pour tvOS (version 10+), il est recommandé de migrer vers les extensions Media Analytics. Pour plus d’informations, voir [Migration du SDK Media autonome vers Adobe Launch — iOS](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md).

1. **Cet abandon de la prise en charge a-t-il une incidence sur le SDK pour Fire TV et Android TV ?**

   Oui : pour Fire TV et Android TV, il est recommandé de migrer vers les extensions Media Analytics. Pour plus d’informations, voir [Migration du SDK Media autonome vers Adobe Launch - Android](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md).
