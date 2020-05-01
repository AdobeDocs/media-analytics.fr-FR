---
title: Périphériques pris en charge
description: null
uuid: null
translation-type: tm+mt
source-git-commit: 3a237ee31412784f708e772cc3a58047630e2184

---


# Périphériques pris en charge {#devices-supported}

Adobe Analytics pour l’audio et la vidéo garantit que chaque flux média est collecté et rapporté sur tous les périphériques.

Adobe Analytics pour l’audio et la vidéo prend en charge tous les principaux périphériques, notamment :

* Smartphones et tablettes iOS et Android
* Appareils OTT pour ROKU, Apple TV, FireTV et Android TV
* Navigateur JavaScript pour ordinateur de bureau et ordinateur portable

Le SDK Media est régulièrement mis à jour lorsque de nouvelles versions de périphériques sont publiées et vous pouvez utiliser le SDK pour l’intégrer aux plus grands lecteurs de médias actuels, y compris Brightcove et Ooyala.

Pour les périphériques ou plates-formes qui ne prennent pas actuellement en charge le SDK ou dans les cas où vous ne souhaitez pas utiliser de SDK, vous pouvez mettre en oeuvre l’API de collecte de médias. L’API de collecte de médias vous permet d’effectuer des appels d’API RESTful directement depuis un périphérique ou une plate-forme vers l’arrière-plan Media Analytics.

Le tableau ci-dessous liste les périphériques actuellement pris en charge. Pour télécharger la dernière version du SDK, consultez [Téléchargement des SDK](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/download-sdks.html). Si un périphérique n’est pas répertorié, contactez le service à la clientèle ou le consultant en solution pour connaître son état.


| Plateforme/périphérique de diffusion en continu |  | Extension Media Launch avec SDK AEP | SDK Media | API Media Collection |
|---------------------------|-----------------------------------------------|:----------------------------:|:-------------------:|:--------------------:|
| Web/Mobile Web |  |  |  |  |
|  | Navigateurs JavaScript | X | X | X |
| Application mobile |  |  |  |  |
|  | Appareils iOS | X | X | X |
|  | Appareils Android | X | X | X |
|  | Périphériques Windows |  |  | X |
| OTT |  |  |  |  |
|  | Apple TV (hérité, TVOS) |  | X | X |
|  | ROKU |  | X<br>(BrightScript) | X<br>(natif) |
|  | Téléviseur Fire (SE Fire) |  | X | X |
|  | Android TV |  | X | X |
|  | Chromecast |  | X | X |
|  | Consoles de jeux (ex. Xbox ONE, Sony PS3/PS4) |  |  | X |
|  | Définir les cadres supérieurs (ex. xfinity X1) |  |  | X |
|  | Smartphone (par exemple Samsung, LG, Sony, Vizio) |  | X<br>(Web) | X |
| Autre |  |  |  |  |
|  | Nouveaux périphériques connectés |  |  | X |


Pour le SDK Media, voir également [Prise en charge de version minimum de plateforme](/help/sdk-implement/setup/setup-overview.md#minimum-platform-version)
