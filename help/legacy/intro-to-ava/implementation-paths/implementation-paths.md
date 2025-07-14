---
title: Quels chemins d’implémentation des médias en flux continu sont disponibles ?
description: Découvrez les chemins d’implémentation des médias en flux continu Adobe, y compris la collecte de données Adobe Experience Platform.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 92%

---

# Chemins d’implémentation {#implementation-paths}

**CE CONTENU A ÉTÉ DÉPLACÉ VERS LE FICHIER DE CHEMINS D’IMPLÉMENTATION ACTUEL.**

Pour chaque chemin d’implémentation, les clients doivent contacter leur représentant commercial/équipe du compte Adobe pour signer une nouvelle commande, car Media Analytics en flux continu comporte un SKU unique et passe d’un modèle de tarification basé sur les appels de serveur à un modèle basé sur les diffusions vidéo.

## Collecte de données Adobe Experience Platform avec l’extension Adobe Media Analytics

>[!NOTE]
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=fr) suivant pour consulter une référence consolidée des modifications terminologiques.


Les balises dans Adobe Experience Platform Launch représentent la nouvelle génération des fonctionnalités de gestion des balises dʼAdobe. Les balises offrent aux clients un moyen simple de déployer et de gérer toutes les balises dʼanalyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes. Les balises sont proposées aux clients Adobe Experience Cloud en tant que fonctionnalité à valeur ajoutée incluse.

Les balises permettent à tout un chacun de créer et de gérer leurs propres intégrations, appelées extensions. Ces extensions sont disponibles pour les clients Adobe Experience Cloud dans une boutique dʼapplications qui leur permet dʼinstaller, de configurer et de déployer rapidement leurs balises.

Une extension est un package de code (JavaScript, HTML et CSS) qui étend les fonctionnalités des balises. Créez, gérez et mettez à jour vos intégrations à l’aide d’une interface en libre-service ou presque. Vous pouvez considérer les extensions comme des applications que vous utilisez pour réaliser vos tâches. Pour plus d’informations, consultez l’article *Présentation des balises* dans la [documentation d’Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=fr).

L’extension Adobe Media Analytics (MA) ajoute le noyau JavaScript Media SDK (Media 2.x SDK) pour l’audio et la vidéo. Cette extension fournit la fonctionnalité permettant d’ajouter l’instance de suivi `MediaHeartbeat` à un site ou un projet de collecte de données.

La collecte de données Adobe avec l’extension Media Analytics nécessite les éléments suivants :
* Vous devez être un client Adobe Experience Cloud.
* Vous devez déployer la collecte de données ou le code intégré DTM sur vos pages web.
* [Extension Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=fr)
* [Extension Experience Cloud ID](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=fr)


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
* Prise en charge intégrée de Nielsen DTVR (linéaire) avec métadonnées ID3 et de DCR avec métadonnées CMS.


TVSDK est déjà intégré au SDK Media Analytics (Heartbeats), ce qui rend l’implémentation beaucoup plus facile et rapide sur chaque plateforme prise en charge. Pour tirer parti de Primetime, suivez les mêmes directives et conditions préalables que celles qui figurent dans [Côté client](/help/legacy/intro-to-ava/implementation-paths/client-side-path.md), ainsi que les documents suivants pour vos plateformes : [Guide de l’utilisateur Primetime.](https://helpx.adobe.com/fr/support/primetime.html)

Vous devez également contacter votre représentant commercial/responsable de compte pour discuter des mesures à prendre pour acheter TVSDK.
