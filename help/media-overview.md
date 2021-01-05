---
title: Mesurer des médias en flux continu dans Adobe Analytics
description: Adobe Analytics for Media (également appelé Media Analytics) fournit aux clients une mesure multimédia performante pour le contenu, le son et les publicités.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: ht
source-git-commit: 82b38f7870b6f890aaa812de30fa2d02d4f3ba8a
workflow-type: ht
source-wordcount: '903'
ht-degree: 100%

---


# Mesurer des médias en flux continu dans Adobe Analytics {#measuring-audio-and-video-in-adobe-analytics}

![Bannière](./assets/media_analytics_banner.png)

## À propos d’Adobe Analytics for Streaming Media

Adobe Analytics for Streaming Media est un module complémentaire d’Adobe Analytics qui fournit de puissants outils de mesure pour l’audio, la vidéo et les publicités. Adobe Analytics fait partie d’Adobe Experience Platform.

Adobe Analytics for Streaming Media vous permet de suivre l’ensemble du parcours client sur votre site. Les mesures s’intègrent facilement aux rapports Adobe Analytics et aux autres produits Adobe Experience Cloud. La mesure des médias vous permet de catégoriser vos données en plusieurs dimensions et segments, en capturant toutes les métadonnées nécessaires à une analyse complète et détaillée. Vous pouvez ensuite analyser les données et attribuer des critères de succès au média entièrement consommé, au temps passé moyen et aux publicités terminées.

Vous pouvez déterminer les mesures de diffusion vidéo essentielles liées à la qualité de service, telles que les images perdues, le temps consacré à la mise en mémoire tampon et le débit moyen. De plus, les mesures peuvent être combinées avec les données de votre site Web ou de votre application pour visualiser le chemin et les intérêts des clients, afin de fournir des recommandations optimisées et de personnaliser les expériences client à l’aide d’Adobe Experience Cloud.

## Fonctionnalités {#features}

Les avantages d’Adobe Analytics for Streaming Media incluent la surveillance en temps réel, les analyses détaillées, des informations exploitables et des opportunités de monétisation.
* **Analyse en temps réel** : prenez des décisions en temps réel et exploitables en utilisant des mesures de performances clés telles que la durée, ex2 et ex3, sur plusieurs canaux. Les principaux événements vidéo de contenu sont mesurés en intervalles de 10 secondes pour capturer toutes les activités au fur et à mesure. Les événements de suivi publicitaires se produisent à des intervalles de 1 seconde.
* **Stimuler l’engagement** : stimulez l’engagement des utilisateurs en réduisant le nombre d’événements de mise en mémoire tampon et en sachant où et quand les publicités doivent s’afficher dans le contenu vidéo pour offrir une expérience de visionnage fluide et moins intrusive qui apporte des visites renouvelées.
* **Image holistique** : combinez plusieurs points de données sur tous vos distributeurs de contenu pour obtenir une vue complète de l’ensemble de vos activités multimédia. Mesurez l’engagement et les vues/écoutes sur tous les canaux possibles via la fonctionnalité Federated Analytics.
* **Meilleure granularité** : évaluez le comportement de visionnage au niveau le plus granulaire, y compris l’heure des visiteurs individuels dans la journée, les observateurs simultanés par minute et la durée moyenne d’affichage du contenu.
* **Mesure précise** : effectuez une mesure pour les différents appareils utilisés pour la consommation de vidéos, notamment les appareils OTT, les smartphones, les tablettes, les postes de travail et autres, pour surveiller les schémas et les habitudes d’engagement des utilisateurs.
* **Segmentation** : appliquez des classifications à vos lecteurs, appareils, genres, chapitres et programmes pour voir comment chacun a un impact sur vos vues générales et l’implication du client dans le contenu, le son, les publicités et ces éléments combinés.

## Mesure des pulsations {#heartbeat}

Adobe Analytics utilise des « pulsations » pour collecter des mesures vidéo. Pendant la lecture vidéo, les pulsations sont envoyées au serveur de suivi de pulsation pour mesurer la durée de lecture. Les appels de pulsation sont envoyés toutes les dix secondes. Les pulsations génèrent des mesures d’engagement vidéo granulaires et des rapports d’abandons vidéo plus précis. Adobe Analytics for Streaming Media mesure les pulsations à l’aide d’Adobe Launch avec l’extension Media Analytics, le SDK Media et l’API Media Collection. Les composants `AppMeasurement` et `VisitorID` sont utilisés pour recevoir des données vidéo.

L’utilisation de pulsations Adobe Analytics pour les médias en flux continu présente les avantages suivants :

| Fonctionnalité | Description |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Événements de médias | Des événements détaillés et personnalisés sont envoyés toutes les 10 secondes pour le contenu principal et toutes les secondes pour les publicités. |
| Mesures et dimensions | Contrôlez des mesures, dimensions et benchmarks standardisés pour plusieurs fournisseurs<br>Grâce à une solution standardisée sur toutes les plates-formes, vous pouvez utiliser des variables uniformes et standardisées sur l’ensemble de vos supports et plates-formes pour permettre une comparaison plus efficace entre les campagnes, les périphériques et les fournisseurs. |
| Intégrations | L’Experience Cloud ID est lié à Adobe Experience Cloud pour une analyse croisée plus facile<br>Avec l’intégration automatique d’Adobe Experience Cloud, vous pouvez segmenter vos audiences multimédia, les cibler et faire des recommandations multimédia en fonction de leurs préférences. |
| Tarifs | Suivi transparent par diffusion média (unique) |
| Mise en œuvre et support | Configuration rationalisée avec mises à jour et améliorations constants<br>Grâce à un processus d’implémentation simplifié, vous pouvez rapidement mettre des variables en correspondance à l’aide de votre API de lecteur et valider les implémentations à l’aide de l’outil de débogage Adobe pour vous assurer que toutes les variables nécessaires sont suivies avec précision. |
| Partage de partenaires | Federated Analytics et Certified Metrics (Mesures certifiées)<br>Avec les données vidéo partagées par le biais de Federated Analytics, vous pouvez capitaliser sur nos fonctionnalités de partage vidéo leaders du secteur, pour évaluer les données de manière holistique pour l’ensemble de vos partenaires de distribution vidéo (opérateurs, programmeurs et distributeurs). |
| Suivi avancé | Suivi du contenu téléchargé, suivi de la récupération des erreurs et observateurs simultanés<br>Vous pouvez effectuer le suivi du contenu multimédia en flux continu téléchargé et lu sur un appareil, quelle que soit sa connectivité. |



## Sécurité {#security}

Chez Adobe, nous prenons la sécurité de vos ressources numériques très au sérieux. De l’intégration rigoureuse de la sécurité dans notre processus et nos outils de développement logiciel interne à nos équipes interfonctionnelles d’intervention en cas d’incident, nous nous efforçons d’être proactifs et flexibles. De plus, notre collaboration avec des partenaires, des chercheurs et d’autres organisations du secteur nous aide à comprendre les dernières menaces et les bonnes pratiques en matière de sécurité, et à renforcer continuellement la sécurité dans les produits et les services que nous offrons.


### Sécurité du calque de transport {#transport-layer-security}

**Remarque TLS -** Adobe applique des normes de conformité de sécurité qui exigent la fin de vie des anciens protocoles de sécurité. Pour continuer à répondre aux normes de protocole de sécurité en constante évolution, Adobe se dirige vers l’utilisation de TLS 1.2, afin d’avoir la version la plus récente et la plus sécurisée en usage. A partir du 20 février 2019, Adobe ne prendra en charge que TLS 1.1 ou version ultérieure. Avec cette modification, Adobe ne collectera plus de données provenant d’utilisateurs finaux disposant d’anciens appareils ou navigateurs web qui déploient TLS 1.0. La migration vers TLS 1.2 améliore la sécurité. Il est important que vous passiez en revue les détails et que vous planifiiez les changements pour une transition en douceur.

>[!NOTE]
>
>TLS est actuellement le protocole de sécurité le plus répandu, utilisé pour les navigateurs web et autres applications exigeant que les données soient échangées en toute sécurité sur un réseau.
