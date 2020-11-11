---
title: FAQ sur l’abandon de la prise en charge du SDK Media Analytics
description: Cette rubrique comprend des questions fréquentes concernant l’abandon de la prise en charge des SDK Media Analytics.
translation-type: tm+mt
source-git-commit: 82b38f7870b6f890aaa812de30fa2d02d4f3ba8a
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 90%

---


# FAQ sur l’abandon de la prise en charge du SDK Media Analytics

Avec l’abandon de la prise en charge des SDK mobiles de version 4 programmée au 31 août 2021, Adobe cessera également de prendre en charge les SDK Media Analytics pour iOS et Android. Après le 31 août 2021, Adobe ne fournira ni correctifs, ni mises à jour liées au système d’exploitation, ni prise en charge du SDK Media Analytics.  Pendant le processus de migration vers ces nouveaux SDK Experience Platform, gardez à l’esprit que les [extensions Media Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) doivent être implémentées pour activer Adobe Analytics for Streaming Media.

## 5 choses à savoir

1. Les SDK mobiles v4 ne seront plus pris en charge après le 31 août 2021. Vous devez migrer vers les SDK Adobe Experience Platform (AEP) pour iOS et Android. Pour plus d’informations, reportez-vous à la [FAQ sur l’abandon de la prise en charge des SDK mobiles de version 4](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq).

1. La mise en oeuvre d’Analytics pour la diffusion en continu des médias nécessite le SDK AEP et l’utilisation des extensions Analytics et Media Analytics. À compter du 1er septembre 2021, vous devrez utiliser les nouveaux SDK et extensions AEP.  Les extensions Media Analytics sont configurées à l’aide d’Adobe Launch.  Pour plus d’informations, voir [Migration du SDK Media autonome vers Adobe Launch](https://docs.adobe.com/content/help/fr-FR/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html).

1. Le développement des fonctionnalités des SDK Media Analytics pour iOS et Android est terminé.  Les nouvelles fonctionnalités introduites à partir de l’automne 2019 sont activées à l’aide des extensions Media Analytics et de l’API Media Collection.

1. Les SDK Roku et Chromecast restent disponibles pour les clients Analytics pour les médias en flux continu. Les SDK Roku et Chromecast continueront d’être améliorés et pris en charge en tant que SDK autonomes.  Si vous utilisez le SDK JS pour Media Analytics, vous pouvez continuer à utiliser le SDK autonome ou activer l’extension Media Analytics à l’aide d’Adobe Launch.

1. Avant le 1er septembre 2021, Adobe peut, à sa seule discrétion, élaborer de nouveaux correctifs pour les problèmes présentant une forte incidence sur le plan technique ou un risque pour l’entreprise. En fonction des données fournies par le client, Adobe déterminera l’incidence et le risque ainsi que les activités qui en découlent.

Contactez votre gestionnaire de la réussite client Adobe si vous avez des questions.

## Questions fréquentes

1. **La prise en charge des SDK Roku et Chromecast sera-t-elle affectée ?&#x200B;**

   Non.  Pour le moment, les SDK Roku et Chromecast continueront à être pris en charge en tant que SDK autonomes.

1. **Les mises en œuvre du SDK Media Analytics pour JS seront-elles affectées par cette modification ?&#x200B;**

   Non.  Les clients qui utilisent le SDK JS pour Media Analytics peuvent continuer à utiliser le SDK ou l’activer par le biais d’Adobe Launch.
&#x200B;
1. **Quel est le niveau d’effort demandé par la migration vers les extensions Media Analytics ?&#x200B;**

   Le niveau d’effort dépend de la mise en œuvre de chaque client : il est donc variable.  Après avoir consulté la documentation concernant la migration ci-dessous, rapprochez-vous du service de nos conseillers et/ou de l’assistance clientèle pour obtenir une assistance supplémentaire.

   [Extensions Media Analytics : migration sous Android](https://docs.adobe.com/content/help/fr-FR/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Extensions Media Analytics : migration sous iOS](https://docs.adobe.com/content/help/fr-FR/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Extensions Media Analytics : nouvelles mises en œuvre](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **Dois-je configurer Launch en tant que système de gestion des balises ? Que se passe-t-il si je ne souhaite pas utiliser Launch ?**

   Dans le cas de l’utilisation d’applications mobiles, Launch n’est pas employé en tant que système de gestion des balises comme c’est le cas pour le web.  L’utilisation de l’interface utilisateur de Launch est requise pour configurer les extensions du SDK. Cette utilisation est similaire à celle de l’interface utilisateur d’Adobe Mobile Services pour configurer le SDK mobile v4. L’utilisation de Launch pour l’installation a pour avantage de proposer des instructions d’installation personnalisées selon l’extension choisie.

1. **Cet abandon de la prise en charge a-t-il une incidence sur le SDK pour tvOS ?**

   Oui : pour tvOS (version 10+), il est recommandé de migrer vers les extensions Media Analytics.  Pour plus d’informations, voir [Migration du SDK Media autonome vers Adobe Launch — iOS](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html).

1. **Cet abandon de la prise en charge a-t-il une incidence sur le SDK pour FireTV et AndroidTV ?&#x200B;**

   Oui : pour FireTV et AndroidTV, il est recommandé de migrer vers les extensions Media Analytics.  Pour plus d’informations, voir [Migration du SDK Media autonome vers Adobe Launch - Android](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html).
