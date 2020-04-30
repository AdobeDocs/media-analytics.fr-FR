---
title: Mesures audio et vidéo dans Adobe Analytics
description: 'Adobe Analytics for Media (également appelé Media Analytics) fournit aux clients une mesure multimédia performante pour le contenu, le son et les publicités. '
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: ht
source-git-commit: 689b7d4ce632d3ddba6704bb8040eec52bfc326f

---


# Mesures audio et vidéo dans Adobe Analytics {#measuring-audio-and-video-in-adobe-analytics}

![Bannière](./assets/media_analytics_banner.png)

>[!IMPORTANT]
>
>La documentation fournie ici est spécifique aux clients utilisant la version 1.5 ou ultérieure de *SDK Media* d’Adobe pour la mesure des pulsations, ou la nouvelle *API Media Collection* d’Adobe pour la mesure des pulsations. Elle n’inclut pas d’instructions concernant la mise en œuvre de la vidéo Milestone héritée. Nous encourageons tous les clients à adopter l’une des dernières solutions de suivi vidéo ou les deux, afin de capitaliser sur les améliorations et la mesure développée. Vous pouvez afficher les [avantages de la transition vers les dernières solutions](media-overview.md#heartbeat-versus-milestone-benefits) ci-dessous. Bien que nous continuerons à prendre en charge la méthode Milestone de suivi des vidéos, nous ne prévoyons pas de mises à jour, de correctifs ou d’améliorations de fonctionnalités. Contactez votre responsable de compte Adobe si vous avez des questions supplémentaires.

## Aperçu {#overview}

Adobe Analytics for Media (également appelé Media Analytics) est un module complémentaire à l’offre Analytics de base qui fournit aux clients une mesure multimédia performante pour le contenu, le son et les annonces publicitaires. Media Analytics offre de nombreux avantages aux clients, qui bénéficient d’un suivi en temps réel, d’analyses détaillées, d’informations exploitables et d’opportunités de monétisation.

Le suivi des médias est activé via l’une des méthodes suivantes :

* L’intégration du **SDK Media** avec les lecteurs vidéo les plus utilisés
* L’intégration de l’**API Media Collection** (API RESTful) dans les lecteurs pour lesquels il n’existe aucun support SDK (ou pour lesquels vous ne souhaitez pas utiliser le SDK)

Adobe Analytics for Media permet aux clients de suivre le parcours complet des clients sur leur site, ce qui inclut la consommation vidéo, et ces mesures sont aisément intégrées dans les rapports Analytics et d’autres produits Experience Cloud. La mesure multimédia vous permet de découper et de regrouper vos données en plusieurs dimensions et segments, en capturant toutes les métadonnées dont vous avez besoin pour effectuer une analyse détaillée complète et attribuer des critères de réussite à des vidéos regardées entièrement, à la durée moyenne de consultation et aux publicités terminées.

Les solutions vidéo mesurent les mesures de diffusion vidéo essentielles liées à la qualité de service, telles que les images perdues, le temps consacré à la mise en mémoire tampon et le débit moyen. Elles peuvent également être combinées à votre site web ou à des données d’application pour visualiser le flux du client et ses centres d’intérêt afin de mieux formuler des recommandations et de personnaliser l’expérience du client dans Adobe Experience Cloud.

## Avantages {#benefits}

Voici quelques-uns des avantages offerts par les solutions de mesure multimédia Adobe :

* **Analyses rapides** : prenez des décisions en temps réel exploitables à l’aide de mesures de performance vidéo clés (par exemple, durée) sur plusieurs canaux. Les principaux événements vidéo de contenu sont mesurés en intervalles de **10 secondes** pour capturer toutes les activités au fur et à mesure. Les événements de suivi publicitaires se produisent à des intervalles de **1 seconde**.
* **Stimuler l’engagement** : stimulez l’engagement des utilisateurs en réduisant le nombre d’événements de mise en mémoire tampon et en sachant où et quand les publicités doivent s’afficher dans le contenu vidéo pour offrir une expérience de visionnage fluide et moins intrusive qui fait revenir les utilisateurs et apporte des visites renouvelées.
* **Image holistique :** Combinez plusieurs points de données sur tous vos distributeurs de contenu pour obtenir une vue complète de l’ensemble de vos activités multimédia et mesurez l’engagement et les vues/écoutes sur tous les canaux possibles via la fonctionnalité [Federated Analytics](/help/federated-analytics.md).
* **Meilleure granularité** : évaluez le comportement de visionnage au niveau le plus granulaire, y compris l’heure des visiteurs individuels dans la journée, les observateurs simultanés par minute et la durée moyenne d’affichage du contenu.
* **Mesure précise** : effectuez une mesure pour les différents appareils utilisés pour la consommation de vidéos, notamment les appareils OTT, les smartphones, les tablettes, les postes de travail et autres, pour surveiller les schémas et les habitudes d’engagement des utilisateurs.
* **Segmentation** : appliquez des classifications à vos lecteurs, appareils, genres, chapitres et programmes pour voir comment chacun a un impact sur vos vues générales et l’implication du client dans le contenu, le son, les publicités et ces éléments combinés.

## Avantages Heartbeat et avantages Milestone {#heartbeat-versus-milestone-benefits}

Adobe Analytics for Media peut être mesuré par deux moyens : la méthode Milestone héritée (vidéo uniquement) et la méthode Heartbeats actuelle (audio et vidéo, dans le SDK Media et l’API Media Collection). La méthode Heartbeats est la méthode privilégiée de mesure et nous encourageons tous les clients à passer à cette version si ce n’est pas déjà fait, pour tirer parti des avantages décrits ci-dessous.

La méthode Milestone héritée est basée sur des appels de serveur individuels au serveur Analytics, pour les démarrages de vidéo, les quartiles, la durée et les fins de vidéo. La méthode Heartbeats offre une solution de suivi vidéo plus robuste qui mesure la vidéo de contenu principal en intervalles de 10 secondes pour fournir des mesures vidéo avancées et normalisées. En outre, Adobe a retiré un enseignement de notre méthode Milestone pour offrir un processus de mise en œuvre plus fluide et simplifié via le SDK VA ou l’API Media Collection utilisé par les pulsations.

Voici quelques-uns des nombreux avantages de la méthode Heartbeats :

* **Processus de mise en œuvre simplifié** : mappez plus facilement les variables via l’API de votre lecteur et validez les mises en œuvre via l’outil Adobe Debug Tool pour vous assurer du suivi précis de toutes les variables nécessaires.
* **Intégration automatique d’Adobe Experience Cloud** : tirez parti de l’intégration automatique avec Adobe Experience Cloud via Experience Cloud ID, segmentez les audiences de votre vidéo, ciblez-les et faites des recommandations vidéo en fonction des préférences des utilisateurs.
* **Données vidéo partagées par le biais de Federated Analytics** : capitalisez sur nos fonctionnalités de partage vidéo leaders du secteur, pour évaluer les données de manière holistique pour l’ensemble de vos partenaires de distribution vidéo (opérateurs, programmeurs et distributeurs).
* **Solution normalisée sur toutes les plateformes :** autorisez des variables homogènes et normalisées sur tous vos médias et plateformes afin de garantir une comparaison plus efficace entre les campagnes, les appareils et les fournisseurs.
* **Suivi du contenu téléchargé :** Suivez le contenu multimédia (vidéo et audio) téléchargé et lu à partir sur un appareil, indépendamment de sa connectivité.

### Graphique comparatif

|  | Video Analytics - Milestone | Media Analytics - Heartbeats |
|---|---|---|
| **Événements de médias** | Événements standard de haut niveau | Événements détaillés et personnalisés toutes les 10 s pour le contenu principal, toutes les 1 s pour les publicités |
| **Mesures et dimensions** | Variations entre les fournisseurs, les mesures non normalisées et les dimensions | Mesures, dimensions et évaluations claires et normalisées pour tous les fournisseurs |
| **Intégrations aux produits Adobe** | Sessions individuelles avec quelques mappages et intégrations | Experience Cloud ID assemblé lié à l’instance Adobe Experience Cloud complète pour une analyse croisée plus facile |
| **Tarifs** | Suivi et facturation par rapport à chaque appel serveur | Suivi transparent par diffusion média (unique) |
| **Mise en œuvre et support** | Intégrations plus longues avec prise en charge limitée des versions existantes et pas de mises à niveau | Configuration simplifiée avec mises à jour et améliorations continues |
| **Partage de partenaires** | S.O. | Federated Analytics et mesures certifiées |
| **Suivi avancé** | S.O. | Suivi de la reprise après erreur et observateurs simultanés |

## Appareils pris en charge {#devices-supported}

Adobe Analytics for Media a évolué avec le secteur pour fournir des outils de collecte de données performants afin de garantir que chaque diffusion vidéo est collectée et signalée sur tous les appareils appropriés. Notre SDK Media est développé pour tous les appareils les plus utilisés, notamment :

* Smartphones et tablettes iOS et Android
* Appareils OTT pour ROKU, Apple TV, FireTV et Android TV
* Navigateur JavaScript pour ordinateur de bureau et ordinateur portable

Les kits SDK sont régulièrement mis à jour lorsque de nouvelles versions d’appareil sont commercialisées. Vous pouvez utiliser ces kits SDK pour intégrer la plupart des lecteurs vidéo les plus courants, y compris Brightcove et Ooyala.

Pour les appareils ou les plateformes qui ne prennent actuellement pas en charge le SDK (ou même s’ils le font), vous pouvez mettre en œuvre l’API Media Collection, par le biais de laquelle vous effectuez des appels d’API RESTful directement de l’appareil/la plateforme au serveur principal Media Analytics.

Le tableau ci-dessous fournit la liste des appareils actuellement pris en charge via la mise en œuvre de notre SDK Media et de notre API Media Collection. Pour télécharger la dernière version du SDK, consultez [Téléchargement des SDK.](sdk-implement/download-sdks.md) Si un appareil par rapport auquel vous cherchez une mesure n’est pas répertorié dans la liste, contactez l’assistance clientèle ou votre consultant de solution pour connaître l’état de cet appareil.

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

Pour le SDK Media, voir également [Prise en charge de version minimum de plateforme](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

## Sécurité du calque de transport {#transport-layer-security}

**Remarque TLS -** Adobe applique des normes de conformité de sécurité qui exigent la fin de vie des anciens protocoles de sécurité. Pour continuer à répondre aux normes de protocole de sécurité en constante évolution, Adobe se dirige vers l’utilisation de TLS 1.2, afin d’avoir la version la plus récente et la plus sécurisée en usage. A partir du 20 février 2019, Adobe ne prendra en charge que TLS 1.1 ou version ultérieure. Avec cette modification, Adobe ne collectera plus de données provenant d’utilisateurs finaux disposant d’anciens appareils ou navigateurs web qui déploient TLS 1.0. La migration vers TLS 1.2 améliore la sécurité. Il est important que vous passiez en revue les détails et que vous planifiiez les changements pour une transition en douceur.

>[!NOTE]
>
>TLS est actuellement le protocole de sécurité le plus répandu, utilisé pour les navigateurs web et autres applications exigeant que les données soient échangées en toute sécurité sur un réseau.

