---
title: Liens d’accès au téléchargement des SDK Media Analytics
description: Liens vers les téléchargements du SDK pour les plateformes disponibles, dont Android, iOS, JavaScript, Chromecast et Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 26%

---

# Obtention des SDK Media, des extensions à l’aide de balises et des SDK OTT {#download-sdks}

Les informations de cette page comprennent des liens pour télécharger les SDK multimédia actuels et obtenir les extensions multimédia.

Les informations de cette page comprennent des liens pour télécharger les SDK Media actuels et obtenir les extensions Media qui utilisent des balises.

Les balises dans Adobe Experience Platform représentent la nouvelle génération de fonctionnalités de gestion de SDK mobile et de balises de site web d’Adobe. Les balises offrent un moyen simple de déployer et gérer les solutions d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes. Pour plus d’informations sur les balises, voir [Présentation des balises](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=fr)


>[!NOTE]
>
>Pour plus d’informations sur le téléchargement des SDK hérités, voir [Ancien SDK de téléchargement](/help/legacy/legacy-download-sdks.md).<br>
>Pour obtenir des informations importantes sur la fin de la prise en charge, voir [FAQ sur la fin de la prise en charge](/help/additional-resources/end-of-support-faqs.md).

## SDK Media et bibliothèques mobiles {#media-sdks-libraries}

### Implémentation web {#download-web-sdk}

| Plateforme prise en charge | Version  |  API   |  Documentation  |  Exemple  |
|:---:|---|---|---|---|
| ![Icône JavaScript](assets/javascript-icon.png) | Web - [SDK Media pour JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [Référence de l’API JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [Configuration du SDK Media v3.x pour JavaScript](/help/implementation/media-sdk/setup/web-implementation.md) | [Exemple de SDK Media pour JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![Icône JavaScript](assets/javascript-icon.png) | Web - Extension Media |  | [Extension Adobe Medium Analytics (SDK 3.x) for Audio and Video — à l’aide de balises (collecte de données)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=en) | [Exemple d’extension Adobe Medium Analytics (SDK 3.x) for Audio and Video](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |

### Implémentation mobile {#get-mobile-extension}

| Plateforme prise en charge | Version  |  Documentation   |  Exemples  |
|:---:|---|---|---|
| ![Icône Android](assets/android-icon.png) | Android - Extension Media | [Documentation du SDK Mobile](https://developer.adobe.com/client-sdks/documentation/) | [Adobe Analytics - Exemple Media Analytics for Audio and Video](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Icône Apple iOS](assets/ios-icon.png)<br>icône d’ajout de tvOS | iOS/tvOS - Extension Media | [Documentation du SDK Mobile](https://developer.adobe.com/client-sdks/documentation/) | [Adobe Analytics - Exemple Media Analytics for Audio and Video](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |

### Mise en oeuvre par-dessus le plan {#download-ott-libraries}

| Plateforme prise en charge | Version  |  API   |  Documentation  |
|:---:|---|---|---|
| ![Icône Chromecast](assets/chromecast-icon.png) | [Kit SDK pour Chromecast v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Référence à l’API Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [Configuration du SDK Mobile v3.x pour Chromecast](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![Icône Roku](assets/roku-icon.png) | [SDK pour Roku v2.2.6](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) | [Référence de l’API Roku](/help/implementation/media-sdk/setup/set-up-roku.md) | [Configuration du SDK Mobile v2.x pour Roku](/help/implementation/media-sdk/setup/set-up-roku.md) |

## Extensions Adobe {#adobe-extensions}

### Extension de médias en flux continu {#streaming-media-extension}

Le **Extension Adobe Medium Analytics for Audio and Video** nécessite le SKU du module complémentaire Adobe Analytics for Media. Pour en savoir plus, contactez votre représentant commercial Adobe, votre gestionnaire de compte ou votre gestionnaire de succès client.

Pour plus d’informations sur l’installation, la configuration et l’implémentation de la variable **Extension Adobe Medium Analytics for Audio and Video**, voir [Présentation de l’extension Adobe Medium Analytics for Audio and Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=en) et [Configuration de l’extension Media Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics#configure-the-media-analytics-extension).

### Extension Analytics {#analytics-extension}

[Extension Analytics v1.6 ou version ultérieure](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en): cette extension vous permet de charger la bibliothèque JavaScript du SDK Web de Adobe Experience Platform pour envoyer des données aux solutions Adobe. Le **Extension Analytics** v1.6 ou version ultérieure est requis.

Pour plus d’informations sur la configuration de cette extension, voir [Configuration de l’extension Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en).

### L’extension Experience Cloud ID {#cloud-id-extension}

[Extension d’ID Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en): cette extension met en oeuvre le service d’identification des Experience Cloud qui identifie les visiteurs dans toutes les solutions Experience Cloud. Le service d’ID Experience Cloud est une extension de personnalisation de Adobe Experience Platform.

Utilisez cette extension pour intégrer le service Experience Cloud Identity à votre propriété. Grâce au service Experience Cloud Identity, vous pouvez créer et stocker des identifiants uniques et persistants pour les visiteurs de votre site.

Pour plus d’informations sur la configuration de cette extension, voir [Configuration de l’extension d’ID d’Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en)
