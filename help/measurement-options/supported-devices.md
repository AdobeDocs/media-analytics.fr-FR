---
title: Périphériques et plateformes pris en charge
description: Adobe Analytics for Audio and Video garantit que chaque flux média est collecté et rapporté sur tous les périphériques.
translation-type: ht
source-git-commit: 4db4e4281ba9c7af078c18d03f73b6e1e007a0e8
workflow-type: ht
source-wordcount: '338'
ht-degree: 100%

---


# Périphériques et plateformes pris en charge {#devices-supported}

>[!IMPORTANT]
>
>Avec l’abandon de la prise en charge des SDK mobiles de version 4 programmée au 31 août 2021, Adobe cessera également de prendre en charge le SDK Media Analytics pour iOS et Android.  Pour plus d’informations, reportez-vous à la [FAQ sur l’abandon de la prise en charge du SDK Media Analytics](/help/sdk-implement/end-of-support-faqs.md).

Adobe Analytics for Audio and Video prend en charge tous les principaux périphériques, notamment :

* Smartphones et tablettes iOS et Android
* Appareils OTT pour ROKU, Apple TV, FireTV et Android TV
* Navigateur JavaScript pour ordinateur de bureau et ordinateur portable

Les SDK Media sont régulièrement mis à jour lorsque de nouvelles versions d’appareil sont commercialisées. Vous pouvez utiliser le SDK pour intégrer les lecteurs vidéo les plus courants y compris Brightcove et Ooyala.

Pour les périphériques ou plateformes qui ne prennent pas actuellement en charge le SDK ou dans les cas où vous ne souhaitez pas utiliser de SDK, vous pouvez mettre en oeuvre l’API Media Collection. L’API Media Collection vous permet d’effectuer des appels d’API RESTful directement depuis un périphérique ou une plate-forme vers le serveur principal Media Analytics.

Le tableau ci-dessous liste les périphériques et les plateformes actuellement pris en charge. Pour télécharger la dernière version du SDK, consultez [Téléchargement des SDK](https://docs.adobe.com/content/help/fr-FR/media-analytics/using/sdk-implement/download-sdks.html). Si un périphérique n’est pas répertorié, contactez l’assistance clientèle ou le consultant en solution pour connaître son état.

| Plateformes et périphériques de diffusion en continu |  | Extension Media Launch avec SDK AEP | SDK Media | API Media Collection |
|:---------------------------:|:-----------------------------------------------:|:----------------------------:|:-------------------:|:--------------------:|
| Web/Mobile Web |  |  |  |  |
|  | Navigateurs JavaScript | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
| Application mobile |  |  |  |  |
|  | Appareils iOS | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Appareils Android | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Appareils Windows |  |  | ![](/help/assets/icon-blue-check.png) |
| OTT |  |  |  |  |
|  | Apple TV (tvOS) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | ROKU |  | ![](/help/assets/icon-blue-check.png)   <br>(BrightScript)    | ![](/help/assets/icon-blue-check.png)<br>(natif) |
|  | Fire TV (Système d’exploitation Fire) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android TV | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Chromecast |  | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
|  | Consoles de jeux (ex. Xbox ONE, Sony PS3/PS4) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Décodeurs (ex. Xfinity X1) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Télévisions connectées (ex. Samsung, LG, Sony, Vizio) |  | ![](/help/assets/icon-blue-check.png)   <br>(Web)    | ![](/help/assets/icon-blue-check.png) |
| Autre |  |  |  |  |
|  | Nouveaux périphériques connectés |  |  | ![](/help/assets/icon-blue-check.png) |

1. La prise en charge de ces SDK sera abandonnée le 31 août 2021. Pour plus d’informations, reportez-vous à la [FAQ sur l’abandon de la prise en charge du SDK Media Analytics](/help/sdk-implement/end-of-support-faqs.md).

Pour plus d’informations sur les versions minimum de plateforme prises en charge pour chaque SDK, voir [Prise en charge de version minimum de plateforme](https://docs.adobe.com/content/help/fr-FR/media-analytics/using/sdk-implement/setup/setup-overview.html).
