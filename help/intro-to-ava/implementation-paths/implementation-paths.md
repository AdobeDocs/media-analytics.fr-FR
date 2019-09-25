---
seo-title: Chemins de mise en œuvre
title: Chemins de mise en œuvre
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Chemins de mise en œuvre {#implementation-paths}

Media Analytics (Heartbeats) est la solution vidéo standard d’Adobe. Elle a remplacé le modèle Milestone plus ancien d’Adobe.

Pour chacun de ces chemins d’implémentation, les clients doivent contacter leur représentant commercial/gestionnaire de compte pour signer une nouvelle commande client, car Media Analytics dispose d’un SKU unique et évolue d’un modèle de tarification basé sur les appels serveur vers un modèle basé sur les flux vidéo :

* **Côté client -** Il s’agit d’intégrations Media Analytics uniquement. Vous pouvez choisir les intégrations du SDK Video Heartbeat et/ou de l’API Media Collection. Ce chemin peut être utilisé dans tout lecteur vidéo, y compris les lecteurs client et/ou OVP tels que Brightcove, Ooyala, thePlatform, etc.

   If Media Analytics is your intended path, see the [Media SDK Implementation](/help/sdk-implement/setup/setup-overview.md) and the [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Pour utiliser Media Analytics, les clients doivent également utiliser Adobe Analytics.

* **Lancement de la plateforme Adobe Experience Platform -** Lancement de la plateforme Adobe Experience Platform, le produit suivant de la gestion dynamique des balises, comporte une extension de lancement Media Analytics qui facilite la mise en oeuvre du suivi vidéo dans vos lecteurs.

   Vous pouvez en savoir plus sur le lancement de la plateforme d’expérience ici : Extension [Adobe Media Analytics pour l’audio et la vidéo](https://docs.adobelaunch.com/extension-reference/web/adobe-media-analytics-for-audio-and-video-extension)
* **Adobe Primetime -** Adobe Primetime est une solution Adobe Experience Cloud qui aide les programmeurs et les distributeurs de contenu à monétiser les médias sur chaque écran connecté.

   Primetime élimine la complexité liée à l’atteinte, la monétisation et l’activation d’audiences mondiales à travers les appareils en fournissant une plate-forme modulaire pour la publication, la publicité, la personnalisation et l’analyse vidéo. En outre, Primetime offre des solutions et une valeur au niveau des aspects suivants :

   * Prise en charge de la mesure précise des types de contenu LINEAR et VOD.
   * Prise en charge de la mesure des coupures publicitaires avec (ou sans) insertion de publicités dynamiques.
   * Le modèle d’insertion de publicités transparent de TVSDK permet d’analyser directement la lecture de la publicité, ce qui augmente la précision.
   * Ensemble d’événements et de métadonnées performant permettant de garantir la précision dans les problèmes de mise en mémoire tampon QoS ou d’interruption de connectivité mobile et les interactions d’utilisateur final (par exemple, recherche, mise en pause et mise en arrière-plan sur appareil mobile).
   * Prise en charge intégrée de Nielsen DTVR (linéaire) avec métadonnées ID3 et de DCR avec métadonnées CMS.
   TVSDK est déjà intégré au SDK Media Analytics (Heartbeats), ce qui facilite et accélère la mise en oeuvre sur toutes les plates-formes prises en charge. Primetime prend également en charge le partenariat avec Nielsen. Pour exploiter Primetime, suivez les mêmes conseils et conditions requises.  [Côté client](/help/intro-to-ava/implementation-paths/client-side-path.md) avec les documents suivants pour votre ou vos plates-formes : Guide de l’utilisateur [Primetime.](https://helpx.adobe.com/primetime/user-guide.html)

   Vous devez également contacter votre représentant commercial/responsable de compte pour discuter des mesures à prendre pour acheter TVSDK.
