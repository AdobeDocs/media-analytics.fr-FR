---
title: Nouveautés d’Analytics des médias
description: 'Nouveautés : contient des informations sur les nouvelles fonctionnalités et les notifications.'
translation-type: tm+mt
source-git-commit: dfffcf1e1d815ca178e0bdba881d973d60fe1631
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 66%

---


# Nouveautés de Media Analytics{#whats-new}

![Bannière](assets/media_analytics_banner.png)


Cette page décrit les nouvelles fonctionnalités, les correctifs et les avis importants dans Media Analytics. Il met également en évidence la documentation, les cours de formation et les didacticiels vidéo qui vous aideront à tirer le meilleur parti des analyses multimédia.


## Notes de mise à jour

Notes de mise à jour d’Adobe Experience Cloud

Les Notes de mise à jour de Adobe Experience Cloud décrivent les nouvelles fonctionnalités, les correctifs et les avis importants dans Adobe Experience Cloud. Ceci inclut les dernières modifications apportées à Media Analytics. Elle met également en évidence la nouvelle documentation, les formations et les tutoriels vidéo qui vous permettent de tirer le meilleur parti d’Experience Cloud.

## Nouvelles fonctionnalités

| Fonctionnalité | [Disponibilité générale](https://docs.adobe.com/content/help/fr-FR/analytics/landing/an-releases.html) - Date cible | Description |
| ----------- | ---------- | ---------- |
| [Panneau Visionneuse de contenu multimédia simultanée](media-reports/media-workspace-panels/media-concurrent-viewers.md) | 17 septembre 2020 | Le panneau Visionneuses simultanées de médias de Workspace vous permet de déterminer où s’est produit le pic d’accès simultané ou où des abandons ont eu lieu. Il fournit des informations importantes sur la qualité du contenu et l’engagement des observateurs et aide à la résolution des problèmes ou à la planification du volume/de l’échelle. |
| [Périphériques et plateformes pris en charge](https://docs.adobe.com/content/help/fr-FR/media-analytics/using/supported-devices.html) | 18 juin 2020 | L’[!UICONTROL extension Media Launch] avec SDK AEP Mobile prend désormais en charge les périphériques OTT suivants :<ul><li>Apple TV (tvOS)</li><li>Fire TV (Système d’exploitation Fire)</li><li>Android TV</li></ul> |
| [Suivi de l’état du lecteur](https://docs.adobe.com/content/help/fr-FR/media-analytics/using/player-state-tracking/player-state-overview.html) | 29 mai 2020 | Les clients [!UICONTROL Media Analytics] peuvent capturer l’interaction de la visionneuse au cours de la lecture à l’aide d’un jeu standard de variables de solution pour le mode Plein écran, le sous-titrage, le mode silencieux, l’incrustation dans l’image et le mode In-Focus. Vous pouvez également créer des états de lecteur personnalisés. [!UICONTROL Des comptes rendus des performances] sur les variables de suivi de l’état du lecteur sont désormais disponibles dans [!UICONTROL Analysis Workspace]. Cette fonctionnalité nécessite l’une des configurations suivantes : <ul><li>SDK Media [!DNL JavaScript] 3.0 ou version ultérieure</li><li>Utilisation avec le SDK [!DNL Adobe Experience Platform] (AEP) :</li><li>[!UICONTROL Extension Media Analytics] (pour le web) : [!UICONTROL Adobe Media Analytics] (SDK 3.x) pour Audio et Video v1.0 ou version ultérieure</li><li>[!UICONTROL Extension Media Analytics] (pour mobile) : [!UICONTROL Adobe Media Analytics pour Audio] et Vidéo v2.0 ou version ultérieure</li><li>[!UICONTROL Collection Médias]</li></ul> |


## Notifications importantes

| Fonctionnalité | [Disponibilité générale](https://docs.adobe.com/content/help/en/analytics/landing/an-releases.html) - Date cible | Description |
| ----------- | ---------- | ---------- |
| [Périphériques et plateformes pris en charge](https://docs.adobe.com/content/help/en/media-analytics/using/supported-devices.html) | 31 août 2021 | Avec l’abandon de la prise en charge des SDK mobiles de version 4 programmée au 31 août 2021, Adobe cessera également de prendre en charge le SDK Media Analytics pour iOS et Android. Pour plus d’informations, reportez-vous à la FAQ sur l’abandon de la prise en charge du SDK Media Analytics. |
| [FAQ sur l’abandon de la prise en charge du SDK Media Analytics](sdk-implement/end-of-support-faqs.md) | Automne 2019 | Le développement des fonctionnalités s’est terminé pour les kits SDK Media Analytics pour iOS et Android.  Les nouvelles fonctionnalités introduites à partir de l’automne 2019 sont activées à l’aide des extensions Media Analytics et de l’API Media Collection. |
| [Présentation du média](media-overview.md) | 20 février 2019 | Adobe ne prend en charge que TLS 1.1 ou version ultérieure. Avec cette modification, l’Adobe ne collectera plus de données auprès des utilisateurs finaux disposant d’anciens périphériques ou navigateurs Web qui déploient TLS 1.0. |
| [Périphériques et plateformes pris en charge](https://docs.adobe.com/content/help/en/media-analytics/using/supported-devices.html) | 19 février 2019 | Les versions minimales de plate-forme prises en charge pour chaque SDK sont répertoriées ci-dessous. <br>- iOS : iOS 6+  <br>- Android : Android 5.0+ - Lollipop  <br>- Chrome : v22+<br>- Mozilla : v27+<br>- Safari : v7+<br>- IE : v1+ |
| [Paramètres audio et vidéo ](metrics-and-metadata/audio-video-parameters.md) | 7 février 2019 | Adobe Analytics for Video and Audio a publié un changement de nom de mesure. La mesure <i>Démarrages de média</i> sera désormais appelée <i>Lancements de média</i>. Ce changement avait pour but d’appliquer les normes du secteur aux mesures et au reporting, ainsi que de rendre la mesure facilement identifiable dans les rapports. |
| [Paramètres audio et vidéo ](metrics-and-metadata/audio-video-parameters.md) | 13 septembre 2018 | Des modifications ont été apportées aux libellés de certaines dimensions, mesures et rapports, afin de permettre le suivi de contenu croisé des analyses vidéo et audio. Les étiquettes modifiées sont les suivantes : *démarrages de vidéo* en *démarrages de média*, *durée de la vidéo* en *durée du contenu* et *nom de la vidéo* en *nom du contenu*. Dans Reports and Analytics, les rapports vidéo ont tous été mis à jour de sorte à employer le terme « média » plutôt que « vidéo ». Ces changements apportés aux étiquettes n’ont eu aucune incidence sur la collecte de données ou les données historiques. Veuillez prendre note de ces modifications au cas où vous seriez amené à les utiliser dans le Report Builder ou dans toute autre extraction automatisée de données provenant de sources externes qui pourrait être affectée par celles-ci. |




<!-- | title | date | description | -->
