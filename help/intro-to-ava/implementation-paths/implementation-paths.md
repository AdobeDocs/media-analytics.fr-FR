---
title: Chemins de mise en œuvre
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: tm+mt
source-git-commit: 0bc3928b8e3076feb8e9a16e005cd0415f723408
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 64%

---


# Chemins de mise en œuvre {#implementation-paths}

Pour chaque chemin d’implémentation, les clients doivent contacter leur représentant commercial/gestionnaire de compte pour signer une nouvelle commande client, car Media Analytics dispose d’un SKU unique et évolue d’un modèle de tarification basé sur les appels serveur vers un modèle basé sur les flux vidéo.

* **Adobe Launch avec l’extension Adobe Media Analytics**

   Adobe Launch est la nouvelle génération de solutions de gestion des balises d’Adobe. Le lancement offre une méthode simple de déploiement et de gestion de toutes les balises d’analyse, de marketing et de publicité nécessaires pour alimenter les expériences client pertinentes. Pour créer et gérer vos propres intégrations avec Launch, vous utilisez des extensions. Une extension est un package JavaScript, HTML et CSS qui étend les fonctionnalités de l’interface utilisateur de lancement et du client. Pour plus d’informations, consultez le Guide de l’utilisateur du lancement de la plateforme [d’expérience.](https://docs.adobe.com/content/help/fr-FR/launch/using/overview.html)

   L’extension Adobe Media Analytics (MA) ajoute le noyau JavaScript Media SDK (Media 2.x SDK) pour l’audio et la vidéo. Cette extension permet d’ajouter l’instance `MediaHeartbeat` de suivi à un site ou à un projet Launch.

   Adobe Launch avec l’extension Media Analytics nécessite les éléments suivants :
   * Vous devez être un client Adobe Experience Cloud.
   * Vous devez déployer le code d’intégration Launch ou DTM sur vos pages Web.
   * [Extension Analytics](https://docs.adobe.com/content/help/fr-FR/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
   * [L’extension Experience Cloud ID](https://docs.adobe.com/content/help/fr-FR/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)


* **Côté client -** Il s’agit d’intégrations propres à Media Analytics. Vous pouvez choisir le SDK Video Heartbeat et/ou les intégrations de l’API Media Collection. Ce chemin peut être utilisé sur n’importe quel lecteur vidéo, y compris les lecteurs clients et/ou OVP tels que Brightcove, Ooyala, thePlatform, etc.

   Si Media Analytics est le chemin que vous choisissez, consultez [Mise en œuvre du SDK Media](/help/sdk-implement/setup/setup-overview.md) et [API Media Collection](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Pour utiliser Media Analytics, les clients doivent également utiliser Adobe Analytics.

* **Adobe Primetime -** Adobe Primetime est une solution Adobe Experience Cloud qui aide les programmeurs et les distributeurs de contenu à monétiser le média sur chaque écran connecté.

   Primetime élimine la complexité liée à l’atteinte, la monétisation et l’activation d’audiences mondiales pour tous les appareils en fournissant une plateforme modulaire pour la publication, la publicité, la personnalisation et l’analyse vidéo. En outre, Primetime propose des solutions et offre une réelle valeur ajoutée au niveau des aspects suivants :

   * Prise en charge de la mesure précise des types de contenu LINEAR et VOD.
   * Prise en charge de la mesure des coupures publicitaires avec (ou sans) insertion de publicités dynamiques.
   * Le modèle d’insertion de publicités transparent de TVSDK permet d’analyser directement la lecture de la publicité, ce qui augmente la précision.
   * Ensemble d’événements et de métadonnées performant permettant de garantir la précision dans les problèmes de mise en mémoire tampon QoS ou d’interruption de connectivité mobile et les interactions d’utilisateur final (par exemple, recherche, mise en pause et mise en arrière-plan sur appareil mobile).
<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK est déjà intégré au SDK Media Analytics (Heartbeats), ce qui rend la mise en œuvre beaucoup plus facile et rapide sur chaque plateforme prise en charge. <!--Primetime also supports the partnership with Nielsen.--> Pour tirer parti de Primetime, suivez les mêmes directives et conditions préalables que celles qui figurent dans [Côté client](/help/intro-to-ava/implementation-paths/client-side-path.md), ainsi que les documents suivants pour vos plateformes : [Guide de l’utilisateur Primetime.](https://helpx.adobe.com/fr/support/primetime.html)

Vous devez également contacter votre représentant commercial/responsable de compte pour discuter des mesures à prendre pour acheter TVSDK.
