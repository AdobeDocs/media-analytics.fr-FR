---
seo-title: Chemins de mise en œuvre
title: Chemins de mise en œuvre
uuid: 8400 c 938-e 77 e -4 c 88-b 23 b -5 f 5977 a 5316 c
translation-type: tm+mt
source-git-commit: ca7e63d9af1f84c7d5d620c72df5f62555f68c03

---


# Chemins de mise en œuvre {#implementation-paths}

Media Analytics (Heartbeats) est la solution vidéo normalisée d'Adobe. Elle a remplacé le modèle Milestone plus ancien d’Adobe.

Pour chacun de ces chemins d'implémentation, les clients doivent contacter leur représentant commercial/gestionnaire de compte pour signer un nouvel ordre de vente, car Media Analytics dispose d'un SKU unique et d'un modèle de tarification basé sur les appels du serveur à un modèle basé sur les flux vidéo :

* **Côté client :** il s'agit uniquement d'intégrations Media Analytics. Vous pouvez choisir les intégrations du SDK Video Heartbeat et/ou de l’API Media Collection. Ce chemin peut être utilisé dans tout lecteur vidéo, y compris les lecteurs client et/ou OVP tels que Brightcove, Ooyala, thePlatform, etc.

   If Media Analytics is your intended path, see the [Media SDK Implementation](../../sdk-implement/setup/setup-overview.md) and the [Media Collection API.](../../media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Pour utiliser Media Analytics, les clients doivent également utiliser Adobe Analytics.

* **Lancement de la plate-forme Adobe Experience Platform -** Adobe Experience Platform Launch, le produit suivi de la gestion dynamique des balises, comporte une extension de lancement Media Analytics qui facilite la mise en œuvre du suivi vidéo dans vos lecteurs.

   You can learn more about Experience Platform Launch here: [Adobe Media Analytics for Audio and Video Extension](https://docs.adobelaunch.com/extension-reference/web/adobe-media-analytics-for-audio-and-video-extension)
* **Adobe Primetime -** Adobe Primetime est une solution Adobe Experience Cloud qui aide les programmeurs et les distributeurs à monétiser les médias sur chaque écran connecté.

   Primetime élimine la complexité liée à l’atteinte, la monétisation et l’activation d’audiences mondiales à travers les appareils en fournissant une plate-forme modulaire pour la publication, la publicité, la personnalisation et l’analyse vidéo. En outre, Primetime offre des solutions et une valeur au niveau des aspects suivants :

   * Prise en charge de la mesure précise des types de contenu LINEAR et VOD.
   * Prise en charge de la mesure des coupures publicitaires avec (ou sans) insertion de publicités dynamiques.
   * Le modèle d’insertion de publicités transparent de TVSDK permet d’analyser directement la lecture de la publicité, ce qui augmente la précision.
   * Ensemble d’événements et de métadonnées performant permettant de garantir la précision dans les problèmes de mise en mémoire tampon QoS ou d’interruption de connectivité mobile et les interactions d’utilisateur final (par exemple, recherche, mise en pause et mise en arrière-plan sur appareil mobile).
   * Prise en charge intégrée de Nielsen DTVR (linéaire) avec métadonnées ID3 et de DCR avec métadonnées CMS.
   TVSDK est déjà intégré au SDK Media Analtyics (Heartbeats), ce qui facilite et accélère l'implémentation sur toutes les plates-formes prises en charge. Primetime prend également en charge le partenariat avec Nielsen. Pour exploiter Primetime, suivez les mêmes conseils et conditions requises.  [Côté client](../../intro-to-ava/implementation-paths/client-side-path.md) avec les documents suivants pour votre ou vos plates-formes : [Guide de l'utilisateur Primetime.](https://helpx.adobe.com/primetime/user-guide.html)

   Vous devez également contacter votre représentant commercial/responsable de compte pour discuter des mesures à prendre pour acheter TVSDK.
