---
title: Chemins de mise en œuvre
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Chemins de mise en œuvre {#implementation-paths}

Video Analytics (Heartbeats) est la solution vidéo normalisée d’Adobe. Elle a remplacé le modèle Milestone plus ancien d’Adobe.

Pour chacun de ces chemins de mise en œuvre, les clients doivent contacter leur représentant commercial/responsable de compte pour signer une nouvelle commande de ventes car Media Analytics comporte un SKU unique et passe d’un modèle de tarification basé sur les appels de serveur à un modèle basé sur les diffusions vidéo :

* **Côté client -** Il s’agit d’intégrations propres à Media Analytics. Vous pouvez choisir le SDK Video Heartbeat et/ou les intégrations de l’API Media Collection. Ce chemin peut être utilisé sur n’importe quel lecteur vidéo, y compris les lecteurs clients et/ou OVP tels que Brightcove, Ooyala, thePlatform, etc.

   Si Media Analytics est le chemin que vous choisissez, consultez [Mise en œuvre du SDK Media](/help/sdk-implement/setup/setup-overview.md) et [API Media Collection](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Pour utiliser Media Analytics, les clients doivent également utiliser Adobe Analytics.

* **Adobe Experience Platform Launch -** Adobe Experience Platform Launch, le produit associé à la Dynamic Tag Management, comprend une extension de lancement Media Analytics qui facilite la mise en œuvre du suivi vidéo dans vos lecteurs.

   Vous pouvez en savoir plus sur Experience Platform Launch ici : [Extension Adobe Media Analytics for Audio and Video](https://docs.adobe.com/content/help/fr-FR/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
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
