---
title: En savoir plus sur les périphériques et plateformes pris en charge
description: « Découvrez les principaux périphériques pris en charge par Adobe Analytics for Streaming Media, tels que les appareils iOS, Android, OTT et les navigateurs JavaScript. »
exl-id: 169ff7b9-e577-45b7-8927-74bdcccc0a77
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: f0abffb48a6c0babb37f16aff2e3302bf5dd0cb4
workflow-type: ht
source-wordcount: '338'
ht-degree: 100%

---

# Périphériques et plateformes pris en charge {#devices-supported}

>[!IMPORTANT]
>
>Avec l’abandon de la prise en charge des SDK mobiles de version 4 programmée au 31 août 2021, Adobe cessera également de prendre en charge le SDK Media Analytics pour iOS et Android.  Pour plus d’informations, reportez-vous à la [FAQ sur l’abandon de la prise en charge du SDK Media Analytics](/help/sdk-implement/end-of-support-faqs.md).

Adobe Analytics for Streaming Media prend en charge tous les principaux appareils, notamment :

* Smartphones et tablettes iOS et Android
* Appareils OTT pour ROKU, Apple TV, FireTV et Android TV
* Navigateur JavaScript pour ordinateur de bureau et ordinateur portable

Les SDK Media sont régulièrement mis à jour lorsque de nouvelles versions d’appareil sont commercialisées. Vous pouvez utiliser le SDK pour intégrer les lecteurs vidéo les plus courants y compris Brightcove et Ooyala.

Pour les périphériques ou plateformes qui ne prennent pas actuellement en charge le SDK ou dans les cas où vous ne souhaitez pas utiliser de SDK, vous pouvez mettre en oeuvre l’API Media Collection. L’API Media Collection vous permet d’effectuer des appels d’API RESTful directement depuis un périphérique ou une plate-forme vers le serveur principal Media Analytics.

Le tableau ci-dessous liste les périphériques et les plateformes actuellement pris en charge. Pour télécharger la dernière version du SDK, consultez [Téléchargement des SDK](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/download-sdks.html?lang=fr). Si un périphérique n’est pas répertorié, contactez l’assistance clientèle ou le consultant en solution pour connaître son état.

| Plateformes et périphériques de diffusion en continu |  | Collecte de données avec SDK AEP Mobile | SDK Media | API Media Collection |
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

Pour plus d’informations sur les versions minimum de plateforme prises en charge pour chaque SDK, voir [Prise en charge de version minimum de plateforme](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/setup/setup-overview.html?lang=fr).
