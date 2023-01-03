---
title: En savoir plus sur les FAQ relatives à l’abandon de la prise en charge du SDK Media Analytics
description: Cette rubrique comprend des questions fréquentes concernant l’abandon de la prise en charge des SDK Media Analytics.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '690'
ht-degree: 100%

---

# Media Analytics FAQ sur la fin de la prise en charge du SDK Mobile

Avec la fin de la prise en charge des SDK Mobile version 4 programmée pour le 31 août 2021, Adobe cessera également de prendre en charge les SDK Media Analytics Mobile pour iOS et Android. Après le 31 août 2021, Adobe ne fournira ni correctifs, ni mises à jour liées au système d’exploitation, ni prise en charge du SDK Media Analytics Mobile.  Pendant le processus de migration vers ces nouveaux SDK Experience Platform, les [extensions Media Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) doivent être mises en œuvre afin d’activer Adobe Analytics for Streaming Media.

>[!NOTE]
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=fr) suivant pour consulter une référence consolidée des modifications terminologiques.


## 5 choses à savoir

1. Les SDK mobiles v4 ne seront plus pris en charge après le 31 août 2021. Vous devez migrer vers les SDK mobiles Adobe Experience Platform (AEP) pour iOS et Android. Pour plus d’informations, reportez-vous à la [FAQ sur l’abandon de la prise en charge des SDK mobiles de version 4](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq).

1. La mise en œuvre d’Analytics for Streaming Media requiert le SDK mobile AEP ainsi que l’utilisation des extensions Analytics et Media Analytics. À compter du 1er septembre 2021, vous devrez utiliser les nouveaux SDK mobiles et extensions AEP.  Les extensions Media Analytics sont configurées à l’aide des balises Adobe (collecte de données).  Pour plus d’informations, voir [Migration du SDK Media autonome vers Adobe Launch](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md).

1. Le développement des fonctionnalités des SDK Media Analytics pour iOS et Android est terminé.  Les nouvelles fonctionnalités introduites à partir de l’automne 2019 sont activées à l’aide des extensions Media Analytics et de l’API Media Collection.

1. Les SDK Roku et Chromecast restent disponibles pour les clients d’Analytics for Streaming Media. Les SDK Roku et Chromecast continueront d’être améliorés et pris en charge en tant que SDK autonomes.  Si vous utilisez le SDK JS pour Media Analytics, vous pouvez continuer à utiliser le SDK autonome ou activer l’extension Media Analytics à l’aide d’Adobe Data Collection (autrefois Adobe Launch).

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

[Extensions Media Analytics : migration sous Android](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)

[Extensions Media Analytics : migration sous iOS](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)

   [Extensions Media Analytics : nouvelles mises en œuvre](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **Dois-je configurer Launch en tant que système de gestion des balises ? Que se passe-t-il si je ne souhaite pas utiliser Launch ?**

   Dans le cas de l’utilisation d’applications mobiles, Launch n’est pas employé en tant que système de gestion des balises comme c’est le cas pour le web.  L’utilisation de l’interface utilisateur de Launch est requise pour configurer les extensions du SDK. Cette utilisation est similaire à celle de l’interface utilisateur d’Adobe Mobile Services pour configurer le SDK mobile v4. L’utilisation de Launch pour l’installation a pour avantage de proposer des instructions d’installation personnalisées selon l’extension choisie.

1. **Cet abandon de la prise en charge a-t-il une incidence sur le SDK pour tvOS ?**

   Oui : pour tvOS (version 10+), il est recommandé de migrer vers les extensions Media Analytics.  Pour plus d’informations, voir [Migration du SDK Media autonome vers Adobe Launch — iOS](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md).

1. **Cet abandon de la prise en charge a-t-il une incidence sur le SDK pour Fire TV et Android TV ?**

   Oui : pour Fire TV et Android TV, il est recommandé de migrer vers les extensions Media Analytics.  Pour plus d’informations, voir [Migration du SDK Media autonome vers Adobe Launch - Android](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md).