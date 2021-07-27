---
title: Quels chemins d’implémentation des médias en flux continu sont disponibles ?
description: Découvrez les chemins d’implémentation des médias en flux continu Adobe, y compris Adobe Launch.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: ht
source-wordcount: '501'
ht-degree: 100%

---

# Chemins de mise en œuvre {#implementation-paths}

Pour chaque chemin de mise en œuvre, les clients doivent contacter leur représentant commercial/responsable de compte pour signer une nouvelle commande car Media Analytics comporte un SKU unique et passe d’un modèle de tarification basé sur les appels de serveur à un modèle basé sur les diffusions vidéo.

* **Adobe Launch avec l’extension Adobe Media Analytics**

   Adobe Launch représente la nouvelle génération de solution de gestion des balises d’Adobe. Launch offre un moyen simple de déployer et de gérer toutes les balises d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes. Pour créer et gérer vos propres intégrations avec Launch, vous utilisez des extensions. Une extension est un module JavaScript, HTML et CSS qui étend l’interface utilisateur de Launch et les fonctionnalités du client. Pour plus d’informations, consultez le [Guide de l’utilisateur d’Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/overview.html?lang=fr)

   L’extension Adobe Media Analytics (MA) ajoute le noyau JavaScript Media SDK (Media 2.x SDK) pour l’audio et la vidéo. Cette extension permet d’ajouter l’instance `MediaHeartbeat` de suivi à un site ou à un projet Launch.

   Adobe Launch avec l’extension Media Analytics nécessite les éléments suivants :
   * Vous devez être un client Adobe Experience Cloud.
   * Vous devez déployer le code Launch ou DTM incorporé sur vos pages web.
   * [Extension Analytics](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html?lang=fr)
   * [L’extension Experience Cloud ID](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html?lang=fr)


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
