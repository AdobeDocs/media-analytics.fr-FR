---
seo-title: Mesures audio et vidéo dans Adobe Analytics
title: Mesures audio et vidéo dans Adobe Analytics
uuid: b 3 cbe 240-b 94 d -42 b 8-a 99 c -0280334 aaa 14
translation-type: tm+mt
source-git-commit: 1915261ec21679f510350663a472096abe7fdf63

---


# Mesures audio et vidéo dans Adobe Analytics{#measuring-audio-and-video-in-adobe-analytics}

![Bannière](./assets/media_analytics_banner.png)

>[!IMPORTANT]
>
>The documentation provided here is specific to clients utilizing version 1.5 or higher of Adobe's *Media SDK* for heartbeat measurement, or Adobe's newer *Media Collection API* for heartbeat measurement. Elle n'inclut pas les instructions concernant l'implémentation vidéo Milestone héritée. Nous encourageons tous les clients à adopter l’une des dernières solutions de suivi multimédia ou les deux, afin de capitaliser sur les améliorations et la mesure développée. Vous pouvez afficher les [avantages de la transition vers les dernières solutions](media-overview.md#section_cnj_5st_p1b) ci-dessous. Bien que nous continuions à prendre en charge la méthode Milestone pour le suivi des vidéos, il n'y aura pas de mise à jour, de correctifs ni d'amélioration des fonctionnalités planifiées. Contactez votre responsable de compte Adobe si vous avez des questions supplémentaires.

## Aperçu {#section_8BFE4F8DA64B4A5F826A4940B11AA466}

Adobe Analytics for Media (également appelé Media Analytics) est un complément à l’offre Analytics de base qui fournit aux clients une mesure multimédia performante pour le contenu, le son et les publicités. Media Analytics offre de nombreux avantages aux clients, qui bénéficient d’un suivi en temps réel, d’analyses détaillées, d’informations exploitables et d’opportunités de monétisation.

Le suivi multimédia est activé via l’une des méthodes suivantes :

* **SDK Media :** Peut être intégré à la plupart des lecteurs multimédia couramment utilisés.
* **API Media Collection :** (API RESTful) Peut être intégrée aux lecteurs qui ne prennent pas en charge le SDK (ou aux lecteurs auxquels les clients ne souhaitent pas intégrer le SDK).

   L’API Media Collection offre également une fonctionnalité supplémentaire qui n’est pas encore disponible dans le SDK :

   * **Suivi du contenu téléchargé :** Permet la prise en charge du suivi du contenu multimédia (vidéo et audio) téléchargé et lu à partir d’un appareil, indépendamment de la connectivité. Cette fonctionnalité a été créée sur l’API Media Collection et suit la même spécification de suivi de lecture. (Le SDK n’est pour l’instant pas pris en charge.)

Adobe Analytics for Media permet aux clients de suivre le parcours complet des clients sur leur site, ce qui inclut la consommation multimédia, et ces mesures sont aisément intégrées dans les rapports Analytics et d’autres produits Experience Cloud. La mesure multimédia vous permet de diviser et de regrouper vos données en plusieurs dimensions et segments, en capturant toutes les métadonnées dont vous avez besoin pour effectuer une analyse détaillée complète et attribuer des critères de succès à des médias consommés entièrement, à la durée moyenne de consommation et aux publicités terminées.

Les solutions multimédia n’incluent pas seulement les principales mesures de diffusion liées à la qualité de service (QoS), par exemple les images perdues, la durée de mise en mémoire tampon et le débit moyen. Elles peuvent également être combinées avec les données de votre site Web ou de votre application pour visualiser le parcours du client et ses intérêts, afin de formuler de meilleures recommandations et de personnaliser les expériences par le biais d’Adobe Experience Cloud.

## Avantages {#section_7712BA90EAE64C118218D1C581EF68B7}

Voici quelques-uns des nombreux avantages offerts par les solutions de mesure multimédia Adobe :

* **Analyses rapides** : Prenez des décisions en temps réel exploitables à l’aide de mesures de performance clés (par exemple, durée) sur plusieurs canaux. Les principaux événements de contenu sont mesurés en intervalles de **10 secondes** pour capturer toutes les activités au fur et à mesure. Les événements de suivi publicitaires se produisent à des intervalles de **1 seconde**.
* **Stimuler l’engagement** : Stimulez l’engagement des utilisateurs en réduisant le nombre d’événements de mise en mémoire tampon et en sachant où et quand les publicités doivent être lues dans le contenu pour offrir une expérience fluide et moins intrusive qui fait revenir les utilisateurs et apporte des visites renouvelées.
* **Image holistique :** combinez plusieurs points de données à l'ensemble de vos distributeurs de contenu pour obtenir une vue complète de l'activité multimédia, et mesurez l'engagement et les vues/écoute sur tous les canaux possibles par le biais [de la fonction Analyses](federated-analytics.md) fédérées.
* **Meilleure granularité** : Évaluez le comportement de visionnage au niveau le plus granulaire, y compris l’heure des visiteurs individuels dans la journée, les observateurs/auditeurs simultanés par minute et la durée moyenne de consommation du contenu.
* **Mesure précise** : Effectuez une mesure à travers les multiples appareils utilisés pour la consommation de médias, notamment les appareils OTT, les smartphones, les tablettes, les postes de travail et autres, pour surveiller les schémas et les habitudes d’engagement des utilisateurs.
* **Segmentation** : Appliquez des classifications à vos lecteurs, appareils, genres, chapitres et programmes pour voir comment chacun a un impact sur vos vues/écoutes générales et l’implication du client dans le contenu, le son, les publicités et ces éléments combinés.

## Avantages Heartbeat et avantages Milestone {#section_cnj_5st_p1b}

Adobe Analytics pour les médias peut être mesuré par deux moyens : la méthode Milestone héritée (vidéo uniquement) et la méthode Heartbeats actuelle (audio et vidéo, présentée à la fois dans Media SDK et dans l'API de collecte de médias). La méthode Heartbeats est la méthode privilégiée de mesure et nous encourageons tous les clients à passer à cette version si ce n’est pas déjà fait, pour tirer parti des avantages décrits ci-dessous.

La méthode Milestone héritée est basée sur des appels de serveur individuels au serveur Analytics, pour les démarrages de vidéo, les quartiles, la durée et les fins de vidéo. La méthode Heartbeats offre une solution de suivi multimédia plus performante qui mesure le contenu principal par intervalles de 10 secondes pour fournir des mesures avancées et normalisées. En outre, Adobe a retiré un enseignement de notre méthode Milestone pour offrir un processus de mise en œuvre plus fluide et simplifié via le kit SDK Media ou l’API Media Collection utilisés par Heartbeats.

Voici quelques-uns des nombreux avantages de la méthode Heartbeats :

* **Processus de mise en œuvre simplifié** : Mappez plus facilement les variables via l’API de votre lecteur et validez les mises en œuvre via l’outil Adobe Debug pour vous assurer du suivi précis de toutes les variables nécessaires.
* **Intégration automatique d’Adobe Experience Cloud** : Tirez parti de l’intégration automatique avec Adobe Experience Cloud via l’Experience Cloud ID, segmentez les audiences de votre média, ciblez-les et faites des recommandations multimédia en fonction des préférences des utilisateurs.
* **Données partagées par le biais de Federated Analytics** : Capitalisez sur nos fonctionnalités de partage multimédia leaders du secteur, pour évaluer les données de manière holistique à travers tous vos partenaires de distribution multimédia (opérateurs, programmeurs et distributeurs).
* **Partenariats avec des partenaires d’évaluation certifiés** : Adobe s’associe au partenaire d’évaluation de l’audience Nielsen pour fournir une mesure tierce de recensement neutre afin d’autoriser des évaluations certifiées de confiance.
* **Solution normalisée sur toutes les plates-formes** : Autorisez des variables homogènes et normalisées sur tous vos médias et plates-formes afin de garantir une comparaison plus efficace entre les campagnes, les appareils et les fournisseurs.

### Graphique comparatif

|  | Video Analytics - Milestone | Media Analytics - Heartbeats |
|---|---|---|
| **Événements multimédia** | Événements standard de haut niveau | Événements détaillés et personnalisés toutes les 10 s pour le contenu principal, toutes les 1 s pour les publicités |
| **Mesures et dimensions** | Variations entre les fournisseurs, les mesures non normalisées et les dimensions | Mesures, dimensions et évaluations claires et normalisées à travers les fournisseurs |
| **Intégrations aux produits Adobe** | Sessions individuelles avec mappages et intégrations | Experience Cloud ID assemblé lié à l’instance Adobe Experience Cloud complète pour une analyse croisée plus facile |
| **Tarifs** | Suivi et facturation par rapport à chaque appel de serveur | Suivi transparent par diffusion multimédia (unique) |
| **Mise en œuvre et support** | Intégrations plus longues avec prise en charge limitée des versions existantes et pas de mises à niveau | Configuration simplifiée avec mises à jour et améliorations continues |
| **Partage de partenaire** | S.O. | Federated Analytics et mesures certifiées |
| **Suivi avancé** | S.O. | Suivi de la reprise après erreur et observateurs simultanés |

## Appareils pris en charge {#section_lkm_l5t_p1b}

Adobe Analytics for Media a évolué avec le secteur pour fournir des outils de collecte de données performants afin de garantir que chaque diffusion multimédia est collectée et signalée sur tous les appareils appropriés. Notre kit SDK Media est développé pour tous les appareils les plus utilisés, notamment :

* Smartphones et tablettes iOS et Android
* Appareils OTT pour ROKU, Apple TV, FireTV et Android TV
* Navigateur JavaScript pour ordinateur de bureau et ordinateur portable

Les kits SDK sont régulièrement mis à jour lorsque de nouvelles versions d’appareils sont publiées et vous pouvez utiliser ces kits SDK pour intégrer la plupart des lecteurs multimédia les plus courants, y compris Brightcove et Ooyala.

Pour les appareils ou les plates-formes qui ne prennent actuellement pas en charge le kit SDK (ou même s’ils le font), vous pouvez mettre en œuvre l’API Media Collection, par le biais de laquelle vous effectuez des appels d’API RESTful directement de l’appareil/la plate-forme au serveur principal Media Analytics.

Le tableau ci-dessous fournit la liste des appareils actuellement pris en charge via la mise en œuvre de notre kit SDK Media et de notre API Media Collection. Pour télécharger la dernière version du SDK, consultez [Téléchargement des SDK.](sdk-implement/download-sdks.md) Si un appareil par rapport auquel vous cherchez une mesure n’est pas répertorié dans la liste, contactez l’assistance clientèle ou votre consultant de solution pour connaître l’état de cet appareil.

|      | SDK Media | API Media Collection |
|---|:---:|:---:|
| **Navigateur JavaScript** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Appareils iOS** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Appareils Android** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Unified Windows Platform (UWP)** |  | ![](assets/icon-blue-check.png) |
| **BlackBerry** |  | ![](assets/icon-blue-check.png) |
| **Apple TV (nouveau/existant)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (JS)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (application native)** |  | ![](assets/icon-blue-check.png) |
| **OSX** |  | ![](assets/icon-blue-check.png) |
| **FireTV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Chromecast** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Xbox One/360** |  | ![](assets/icon-blue-check.png) |
| **Sony PS3/PS4** |  | ![](assets/icon-blue-check.png) |
| **(Autres/nouveaux appareils connectés)** |  | ![](assets/icon-blue-check.png) |

For Media SDK, also see [Minimum Platform Version Support](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

## Transport Layer Security {#transport-layer-security}

**Avis TLS :** Adobe dispose de normes de conformité de sécurité qui exigent la fin de vie des anciens protocoles de sécurité. Pour respecter les normes de protocole de sécurité en évolution, Adobe évolue vers TLS 1.2 pour que la version la plus récente et la plus sécurisée soit utilisée. Depuis le 20 février 2019, Adobe ne prendra en charge que TLS 1.1 ou version ultérieure. Avec cette modification, Adobe ne collectera plus les données à partir de la fin : les utilisateurs disposant d'anciens appareils ou de navigateurs Web qui déploient TLS 1.0. La migration vers TLS 1.2 améliore la sécurité. Il est important que vous passiez en revue les détails et que vous planifiiez les changements pour une transition en douceur.

>[!NOTE]
>
>TLS est actuellement le protocole de sécurité le plus déployé utilisé dans les navigateurs Web et les autres applications qui exigent que les données soient échangées en toute sécurité sur un réseau.
