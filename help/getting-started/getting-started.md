---
title: Prise en main
description: Prise en main d’Adobe Analytics for Streaming Media.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 660aa29a-2a3d-4a4f-acd6-471551d1047b
source-git-commit: 8b939da2374acb5d573a553c848ba880345e64b5
workflow-type: ht
source-wordcount: '439'
ht-degree: 100%

---

# Prise en main {#getting-started}

Adobe Analytics for Streaming Media offre deux méthodes principales d’implémentation, les SDK Media et les API Media Collection.

![méthodes](assets/getting-started2.png)

Grâce à la logique intégrée des **SDK Media**, vous pouvez comparer avec précision plusieurs plateformes multimédias, notamment des sites Web, des téléphones mobiles, des télévisions connectées, des tablettes, des appareils OTT, des décodeurs et des consoles de jeux. Vous pouvez même comparer le contenu téléchargé. Vous obtenez des informations approfondies sur l’engagement de l’utilisateur, vous pouvez ainsi comprendre la durée, le moment et le lieu de l’engagement des observateurs. Les SDK Media utilisent les **API Media Collection** pour effectuer le suivi. Les API Media Collection sont personnalisables si votre application nécessite des fonctionnalités de suivi personnalisées. Pour les appareils non pris en charge par les SDK Media, vous pouvez utiliser les API Media Collection.

La solution Adobe Analytics for Streaming Media est fournie pour les plateformes multimédias suivantes :

* Web
* Mobile
* OTT
* Tout appareil connecté pouvant être utilisé pour les médias en flux continu ou une intégration serveur à serveur

Pour obtenir de plus amples informations, consultez [Périphériques et plateformes pris en charge](#_Supported_devices_and).

>[!IMPORTANT]
>
>Pour implémenter Adobe Analytics for Streaming Media, contactez votre représentant commercial ou votre responsable de compte Adobe pour vous assurer que Streaming Media fait partie de votre portefolio de produits.

## SDK Media pour les médias en flux continu {#media-sdks}

Les SDK Media pour les médias en flux continu sont disponibles pour les plateformes JavaScript, Android, iOS, tvOS, Chromecast et Roku.

Pour obtenir de plus amples informations sur le téléchargement et l’installation des SDK Media, consultez [Obtention des SDK Media, des extensions à l’aide de balises et des SDK OTT](/help/getting-started/download-sdks.md).


## API Media Collection {#media-collection-apis}

Les **API Media Collection** vous permettent de personnaliser votre implémentation de Media Analytics. Utilisez les API Media Collection pour appeler directement les serveurs d’Adobe afin d’effectuer pratiquement toutes les actions réalisables à l’aide des SDK et plus encore. Personnalisez votre collecte de données afin de créer des rapports qui explorent vos données de médias en flux continu, y obtiennent des insights ou répondent à des questions importantes à leur sujet.

Pour obtenir de plus amples informations sur l’utilisation des API Media Collection, consultez [Documentation relative à l’API Streaming Media](/help/implementation/media-collection-api/mc-api-overview.md).

## Extensions Adobe {#adobe-extensions}

* L’[**extension Adobe Media Analytics for Audio and Video**](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=fr) (extension Media Analytics) est requise pour les implémentations iOS et tvOS. Cette extension permet d’ajouter l’instance de suivi à un site ou un projet de balise. L’extension MA nécessite également les extensions Analytics et Experience Cloud ID.

* [Extension Analytics v1.6 ou version ultérieure](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=fr) : cette extension vous permet de charger la bibliothèque JavaScript du SDK Web Adobe Experience Platform pour envoyer des données aux solutions Adobe.

* [Extension Experience Cloud ID](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=fr) : cette extension implémente le service Experience Cloud ID qui identifie les visiteurs à travers l’ensemble des solutions Experience Cloud. Le service Experience Cloud ID est une extension de personnalisation d’Adobe Experience Platform.
