---
title: Quels chemins d’implémentation des médias en flux continu sont disponibles ?
description: Découvrez les chemins d’implémentation des médias en flux continu Adobe, y compris la collecte de données Adobe Experience Platform.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/U9PBQc7dHNmONZc06t1Xi7EITkveGUkzcst6Sakqqzo
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: eb9732ab-8232-4b21-bc4c-89de86dbe4d7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 676
ht-degree: 87%

---

# Chemins d’implémentation {#implementation-paths}

**CE CONTENU A ÉTÉ DÉPLACÉ VERS LE FICHIER DE CHEMINS D’IMPLÉMENTATION ACTUEL.**

Pour chaque chemin d’implémentation, les clients doivent contacter leur représentant commercial ou l’équipe du compte Adobe pour signer une nouvelle commande, car la collection de médias en flux continu Customer Journey Analytics et Adobe Analytics for Streaming Media disposent d’un SKU unique et passent d’un modèle de tarification basé sur les appels au serveur à un modèle basé sur les diffusions vidéo.

## Collecte de données Adobe Experience Platform avec l’extension Adobe Media Analytics

>[!NOTE]
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=fr) suivant pour consulter une référence consolidée des modifications terminologiques.


Les balises dans Adobe Experience Platform Launch représentent la nouvelle génération des fonctionnalités de gestion des balises dʼAdobe. Les balises offrent aux clients un moyen simple de déployer et de gérer toutes les balises dʼanalyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes. Les balises sont proposées aux clients Adobe Experience Cloud en tant que fonctionnalité à valeur ajoutée incluse.

Les balises permettent à tout un chacun de créer et de gérer leurs propres intégrations, appelées extensions. Ces extensions sont disponibles pour les clients Adobe Experience Cloud dans une boutique dʼapplications qui leur permet dʼinstaller, de configurer et de déployer rapidement leurs balises.

Une extension est un package de code (JavaScript, HTML et CSS) qui étend les fonctionnalités des balises. Créez, gérez et mettez à jour vos intégrations à l’aide d’une interface en libre-service ou presque. Vous pouvez considérer les extensions comme des applications que vous utilisez pour exécuter vos tâches.Pour plus d’informations, consultez l’article *Présentation des balises* dans la documentation de [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=fr)

L’extension Adobe Media Analytics (MA) ajoute le noyau JavaScript Media SDK (Media 2.x SDK) pour l’audio et la vidéo. Cette extension fournit la fonctionnalité permettant d’ajouter l’instance de suivi `MediaHeartbeat` à un site ou un projet de collecte de données.

La collecte de données Adobe avec l’extension Media Analytics nécessite les éléments suivants :
* Vous devez être un client Adobe Experience Cloud.
* Vous devez déployer la collecte de données ou le code intégré DTM sur vos pages web.
* [Extension Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=fr)
* [L’extension Experience Cloud ID](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=fr)


## Côté client

Il s’agit d’intégrations propres à Media Analytics. Vous pouvez choisir le SDK Video Heartbeat et/ou les intégrations de l’API Media Collection. Ce chemin peut être utilisé sur n’importe quel lecteur vidéo, y compris les lecteurs clients et/ou OVP tels que Brightcove, Ooyala, thePlatform, etc.

Si Media Analytics est le chemin que vous choisissez, consultez [Mise en œuvre du SDK Media](/help/legacy/setup/legacy-setup-overview.md) et [API Media Collection](/help/implementation/media-collection-api/mc-api-overview.md)

>[!IMPORTANT]
>Pour utiliser Media Analytics, les clients doivent également utiliser Adobe Analytics.

## Adobe Primetime

Adobe Primetime est une solution Adobe Experience Cloud qui aide les programmeurs et les distributeurs de contenu à monétiser le média sur chaque écran connecté.

Primetime élimine la complexité liée à l’atteinte, la monétisation et l’activation d’audiences mondiales pour tous les appareils en fournissant une plateforme modulaire pour la publication, la publicité, la personnalisation et l’analyse vidéo. En outre, Primetime propose des solutions et offre une réelle valeur ajoutée au niveau des aspects suivants :

* Prise en charge de la mesure précise des types de contenu LINEAR et VOD.
* Prise en charge de la mesure des coupures publicitaires avec (ou sans) insertion de publicités dynamiques.
* Le modèle d’insertion de publicités transparent de TVSDK permet d’analyser directement la lecture de la publicité, ce qui augmente la précision.
* Ensemble d’événements et de métadonnées performant permettant de garantir la précision dans les problèmes de mise en mémoire tampon QoS ou d’interruption de connectivité mobile et les interactions d’utilisateur final (par exemple, recherche, mise en pause et mise en arrière-plan sur appareil mobile).
* Prise en charge intégrée du Nielsen DTVR (linéaire) avec métadonnées ID3 et du DCR avec métadonnées CMS.


TVSDK est déjà intégré au SDK Media Analytics (Heartbeats), ce qui rend l’implémentation beaucoup plus facile et rapide sur chaque plateforme prise en charge. Pour tirer parti de Primetime, suivez les mêmes directives et conditions préalables que celles qui figurent dans [Côté client](/help/legacy/intro-to-ava/implementation-paths/client-side-path.md), ainsi que les documents suivants pour vos plateformes : [Guide de l’utilisateur Primetime.](https://helpx.adobe.com/fr/support/primetime.html)

Vous devez également contacter votre représentant commercial/responsable de compte pour discuter des mesures à prendre pour acheter TVSDK.
