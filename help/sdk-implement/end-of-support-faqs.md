---
title: FAQ sur la fin du support du SDK Media Analytics
description: Cette rubrique comprend des questions fréquentes sur la fin de la prise en charge des SDK Media Analytics.
translation-type: tm+mt
source-git-commit: 38adc54438f85ca8ece8c77d9ff0d0aa14eb6605
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 3%

---


# FAQ sur la fin du support du SDK Media Analytics

Avec la fin de la prise en charge des SDK mobiles de la version 4 le 31 août 2021, Adobe cessera également de prendre en charge les SDK Media Analytics pour iOS et Android. Après le 31 août 2021, Adobe ne fournira ni correctifs, ni mises à jour liées au système d’exploitation, ni prise en charge du SDK Media Analytics.  Pendant le processus de migration vers ces nouveaux SDK de plateforme d’expérience, gardez à l’esprit que les extensions [](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) Media Analytics doivent être mises en oeuvre pour activer Adobe Analytics pour l’audio et la vidéo.

## 5 premières choses à savoir

1. Les kits SDK Mobile v4 ne seront plus pris en charge après le 31 août 2021. Vous devez migrer vers les kits SDK de la plateforme d’expérience Adobe (AEP) pour iOS et Android. Pour plus d’informations, voir FAQ [sur les kits SDK mobiles](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq)Version 4.

1. La mise en oeuvre d’Analytics pour l’audio et la vidéo requiert le SDK AEP et l’utilisation des extensions Analytics et Media Analytics. À compter du 1er septembre 2021, vous devez utiliser les nouveaux SDK AEP et les extensions.  Les extensions Media Analytics sont configurées à l’aide d’Adobe Launch.  Pour plus d’informations, voir [Migration du SDK multimédia autonome vers Adobe Launch](https://docs.adobe.com/content/help/fr-FR/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)

1. Le développement des fonctionnalités est terminé pour les kits SDK Media Analytics pour iOS et Android.  Les nouvelles fonctionnalités introduites à partir de l’automne 2019 sont activées à l’aide des extensions Media Analytics et de l’API Media Collection.

1. Les SDK Roku et Chromecast restent disponibles pour les clients Analytics pour l’audio et la vidéo. Les SDK Roku et Chromecast continueront d’être améliorés et pris en charge en tant que SDK autonomes.  Si vous utilisez le SDK JS pour Media Analytics, vous pouvez continuer à utiliser le SDK autonome ou activer l’extension Media Analytics à l’aide de Adobe Launch.

1. Avant le 1er septembre 2021, Adobe peut, à sa seule discrétion, mettre au point de nouveaux correctifs pour les problèmes d&#39;impact technique élevé ou d&#39;exposition commerciale. Sur la base des commentaires des clients, Adobe déterminera le degré d&#39;impact et d&#39;exposition ainsi que les activités qui en découlent.

Si vous avez des questions, contactez votre responsable de succès client Adobe.

## Questions fréquentes

1. **La prise en charge des SDK Roku et Chromecast sera-t-elle affectée ? &#x200B;**

   Non.  Les SDK Roku et Chromecast continueront à être pris en charge en tant que SDK autonomes pour le moment. &#x200B; &#x200B;
1. **Les implémentations du SDK JS Media Analytics seront-elles affectées par cette modification ? &#x200B;**

   Non.  Les clients qui utilisent le SDK JS pour Media Analytics peuvent continuer à utiliser le SDK ou l’activer via Adobe Launch.
&#x200B;
1. **Quel est le niveau d’effort de migration vers les extensions Media Analytics ? &#x200B;**

   La LOE dépend de la mise en oeuvre de chaque client, elle varie donc.  Après avoir examiné la documentation sur la migration ci-dessous, contactez le service de conseil et/ou le service clientèle pour obtenir une assistance supplémentaire.

   [Extensions Media Analytics : Migration Android](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Extensions Media Analytics : Migration iOS](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Extensions Media Analytics : nouvelles implémentations](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **Dois-je disposer du paramètre Lancer en tant que système de gestion des balises ? Que se passe-t-il si je ne souhaite pas utiliser Lancement ?**

   Dans le cas de l’utilisation d’une application mobile, le lancement n’est pas utilisé comme système de gestion des balises comme pour le Web.  L’utilisation de l’interface utilisateur de lancement est requise pour configurer les extensions du SDK. Cette méthode est similaire à celle utilisée dans l’interface utilisateur des services mobiles Adobe pour configurer le SDK mobile v4. Pour l&#39;installation, l&#39;avantage de l&#39;utilisation de Launch est qu&#39;il vous donne des instructions d&#39;installation personnalisées en fonction de l&#39;extension que vous choisissez.

1. **Cette fin de prise en charge a-t-elle un impact sur le SDK pour tvOS ?**

   Oui, pour tvOS (version 10+), la mise en oeuvre recommandée consiste à migrer vers les extensions Media Analytics.  La prise en charge du SDK AEP et de Media Analytics Extension est prévue pour juin 2020.  Pour plus d’informations, voir [Migration du SDK multimédia autonome vers Adobe Launch - iOS](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html).

1. **Cette fin de prise en charge a-t-elle un impact sur le SDK pour FireTV et AndroidTV ? &#x200B;**

   Oui, pour FireTV et AndroidTV, la mise en oeuvre recommandée consiste à migrer vers les extensions Media Analytics.  La prise en charge du SDK AEP et de Media Analytics Extension est prévue pour juin 2020.  Pour plus d’informations, voir [Migration depuis le SDK multimédia autonome vers Adobe Launch - Android](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html).
