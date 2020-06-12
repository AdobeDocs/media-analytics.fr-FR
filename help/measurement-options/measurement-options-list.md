---
title: Options de mesure
description: null
uuid: null
translation-type: ht
source-git-commit: 967a126723ebbbe02097bd07edc2ed967cd35f4c
workflow-type: ht
source-wordcount: '293'
ht-degree: 100%

---


# Options de mesure {#measurement-options}

Vous pouvez activer le suivi audio et vidéo à l’aide d’Adobe Launch avec l’extension Adobe Media Analytics, le SDK Media ou l’API Media Collection.

## Adobe Launch avec l’extension Adobe Media Analytics

Adobe Launch représente la nouvelle génération de solution de gestion des balises d’Adobe. Launch offre un moyen simple de déployer et de gérer toutes les balises d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes. Pour créer et gérer vos propres intégrations avec Launch, vous utilisez des extensions. Une extension est un module JavaScript, HTML et CSS qui étend l’interface utilisateur de Launch et les fonctionnalités du client. Pour plus d’informations, consultez le [Guide de l’utilisateur d’Experience Platform Launch](https://docs.adobe.com/content/help/fr-FR/launch/using/overview.html)

L’extension Adobe Media Analytics (MA) ajoute le noyau JavaScript Media SDK (Media 2.x SDK) pour l’audio et la vidéo. Cette extension permet d’ajouter l’instance `MediaHeartbeat` de suivi à un site ou à un projet Launch.

Adobe Launch avec l’extension Media Analytics nécessite les éléments suivants :
* Vous devez être un client Adobe Experience Cloud.
* Vous devez déployer le code Launch ou DTM incorporé sur vos pages web.
* [Extension Analytics](https://docs.adobe.com/content/help/fr-FR/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
* [L’extension Experience Cloud ID](https://docs.adobe.com/content/help/fr-FR/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)

## SDK Media

L’intégration du SDK Media avec les lecteurs vidéo les plus courants.

## API Media Collection (API RESTful)

S’intègre à des lecteurs sans prise en charge de SDK ou lorsque l’intégration du SDK n’est pas nécessaire.<br>À compter de la version v2.2.0, les SDK de la bibliothèque Video Heartbeat (VHL) sont renommés SDK Media Analytics pour prendre en charge le suivi audio et vidéo. Le SDK Media 2.2.0 est entièrement rétrocompatible avec la série des SDK VHL 2.x. Le changement de nom est simplement un changement de convention d’appellation et n’emporte aucun changement fonctionnel.
