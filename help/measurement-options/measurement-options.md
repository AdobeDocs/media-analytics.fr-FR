---
title: Options de mesure
description: null
uuid: null
translation-type: tm+mt
source-git-commit: 47b4c7fe09da0d38c8faae1c3b4293ce48552bdc

---


# Options de mesure

Vous pouvez activer le suivi audio et vidéo à l’aide d’Adobe Launch avec l’extension Adobe Media Analytics, le SDK Media ou l’API Media Collection.

## Adobe Launch avec l’extension Adobe Media Analytics

Adobe Launch est la nouvelle génération de solutions de gestion des balises d’Adobe. Le lancement offre une méthode simple de déploiement et de gestion de toutes les balises d’analyse, de marketing et de publicité nécessaires pour alimenter les expériences client pertinentes. Pour créer et gérer vos propres intégrations avec Launch, vous utilisez des extensions. Une extension est un package JavaScript, HTML et CSS qui étend les fonctionnalités de l’interface utilisateur de lancement et du client. Pour plus d’informations, consultez le Guide de l’utilisateur du lancement de la plateforme [d’expérience.](https://docs.adobe.com/content/help/fr-FR/launch/using/overview.html)

L’extension Adobe Media Analytics (MA) ajoute le noyau JavaScript Media SDK (Media 2.x SDK) pour l’audio et la vidéo. Cette extension permet d’ajouter l’instance `MediaHeartbeat` de suivi à un site ou à un projet Launch.

Adobe Launch avec l’extension Media Analytics nécessite les éléments suivants :
* Vous devez être un client Adobe Experience Cloud.
* Vous devez déployer le code d’intégration Launch ou DTM sur vos pages Web.
* [Extension Analytics](https://docs.adobe.com/content/help/fr-FR/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
* [L’extension Experience Cloud ID](https://docs.adobe.com/content/help/fr-FR/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)

## SDK Media

Le SDK multimédia s’intègre aux lecteurs multimédias les plus utilisés.

## API de collecte de médias (API RESTful)

S’intègre à des lecteurs sans prise en charge du SDK ou lorsque l’intégration du SDK n’est pas nécessaire.<br>A compter de la version v2.2.0, les SDK de la bibliothèque Video Heartbeat (VHL) sont renommés SDK Media Analytics pour prendre en charge le suivi audio et vidéo. Le SDK Media 2.2.0 est entièrement rétrocompatible avec la série de SDK VHL 2.x. Le changement de nom est simplement un changement de convention d’affectation de nom et ne représente pas de changements fonctionnels.
