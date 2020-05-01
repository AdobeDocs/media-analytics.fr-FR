---
title: Mesures audio et vidéo dans Adobe Analytics
description: Adobe Analytics for Media (également appelé Media Analytics) fournit aux clients une mesure multimédia performante pour le contenu, le son et les publicités.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: bddcbcd844145788518c60399bee9e4744e42d3a

---


# Mesures audio et vidéo dans Adobe Analytics {#measuring-audio-and-video-in-adobe-analytics}

![Bannière](./assets/media_analytics_banner.png)

## A propos d’Adobe Analytics pour l’audio et la vidéo

Adobe Analytics pour l’audio et la vidéo est un module complémentaire d’Adobe Analytics qui fournit de puissants outils de mesure pour l’audio, la vidéo et les publicités. Adobe Analytics fait partie de la plate-forme Adobe Experience Platform.

Adobe Analytics pour les fichiers audio et vidéo vous permet de suivre l’ensemble du parcours des clients sur votre site. Les mesures s’intègrent facilement aux rapports Adobe Analytics et aux autres produits Adobe Experience Cloud. La mesure des médias vous permet de catégoriser vos données en plusieurs dimensions et segments, en capturant toutes les métadonnées nécessaires à une analyse complète et détaillée. Vous pouvez ensuite analyser les données et attribuer des critères de réussite au média entièrement consommé, à la durée moyenne de consultation et aux publicités terminées.

Vous pouvez mesurer des mesures de diffusion vitales liées à la qualité de service (perte d’images, durée de mise en mémoire tampon et débit moyen, par exemple). De plus, les mesures peuvent être combinées avec les données de votre site Web ou de votre application pour visualiser le chemin et les intérêts des clients, afin de fournir des recommandations optimisées et de personnaliser les expériences client à l’aide d’Adobe Experience Cloud.

## Fonctionnalités {#features}

Les avantages d’Adobe Analytics pour l’audio et la vidéo incluent la surveillance en temps réel, une analyse détaillée, des informations exploitables et des opportunités de monétisation.
* **analyse** en temps réel : prenez des décisions en temps réel et exploitables en utilisant des mesures de performances clés telles que la durée, ex2 et ex3, sur plusieurs canaux. Les principaux événements vidéo de contenu sont mesurés en intervalles de 10 secondes pour capturer toutes les activités au fur et à mesure. Les événements de suivi publicitaires se produisent à des intervalles de 1 seconde.
* **Favoriser l&#39;engagement**: permet aux utilisateurs d&#39;interagir pleinement avec moins de événements de mise en mémoire tampon et de comprendre où et quand les publicités doivent être lues dans le contenu afin de fournir une expérience fluide et moins intrusive permettant d&#39;effectuer des visites répétées.
* **Image** holistique : combinez plusieurs points de données sur l&#39;ensemble de vos distributeurs de contenu pour obtenir une vue complète de toute votre activité multimédia. Mesurez l’engagement et les vues/écoutes dans tous les canaux possibles grâce à la fonction Analyses fédérées.
* **Granularité** accrue : évaluez le comportement d&#39;affichage au niveau le plus granulaire, y compris l&#39;heure du visiteur individuel, les visiteurs/auditeurs simultanés par minute et la durée moyenne de consommation du contenu.
* **Mesure** précise : mesurez les différents périphériques utilisés pour la consommation de médias, notamment OTT, smartphone, tablette, bureau, etc., afin de surveiller les schémas et habitudes d&#39;engagement des utilisateurs.
* **Segmentation**: appliquez des classifications à vos lecteurs, périphériques, genres, chapitres et montre comment chacun a un impact sur vos vues/écoutes globales et l&#39;engagement des clients avec le contenu, l&#39;audio, les publicités et la combinaison.

## Mesure Pulsation {#heartbeat}

Adobe Analytics utilise des &quot;pulsations&quot; pour collecter des mesures vidéo. Pendant la lecture vidéo, les pulsations sont envoyées au serveur de suivi de pulsation pour mesurer la durée de lecture. Les appels de pulsation sont envoyés toutes les dix secondes. Les pulsations génèrent des mesures d’engagement vidéo granulaires et des rapports d’abandons vidéo plus précis. Adobe Analytics pour l’audio et la vidéo mesurent les pulsations à l’aide d’Adobe Launch avec l’extension Media Analytics, le SDK Media et l’API Media Collection. Les `AppMeasurement` et `VisitorID` composants sont utilisés pour recevoir des données vidéo.

L’utilisation des pulsations Adobe Analytics pour l’audio et la vidéo présente les avantages suivants :

| Fonctionnalité | Description |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Événements de médias | Des Événements détaillés et personnalisés sont envoyés toutes les 10 secondes pour le contenu principal et toutes les 1 seconde pour les publicités. |
| Mesures et dimensions | Effacer les mesures, les dimensions et les repères standardisés entre<br>les fournisseursGrâce à une solution standardisée sur toutes les plates-formes, vous pouvez utiliser des variables uniformes et standardisées sur l&#39;ensemble de vos supports et plates-formes pour permettre une comparaison plus efficace entre les campagnes, les périphériques et les fournisseurs. |
| Intégrations | Experience Cloud ID est lié à Adobe Experience Cloud pour une<br>analyse croisée plus facileAvec l’intégration automatique d’Adobe Experience Cloud, vous pouvez segmenter vos audiences multimédia, les cible et faire des recommandations multimédia en fonction des préférences de l’utilisateur. |
| Tarifs | Suivi transparent par diffusion média (unique) |
| Mise en œuvre et support | Configuration rationalisée avec mises à jour et<br>améliorations en coursGrâce à un processus d’implémentation simplifié, vous pouvez rapidement mapper des variables à l’aide de votre API de lecteur et valider les implémentations à l’aide de l’outil de débogage Adobe pour vous assurer que toutes les variables nécessaires sont suivies avec précision. |
| Partage de partenaires | Federated Analytics and Certified Metrics<br>With shared data through Federated Analytics, you can capitalize on our industry-first media sharing capabilities, to evaluate data holistically across all of your media distribution partners—operators, programmers, and distributors. |
| Suivi avancé | Suivi du contenu téléchargé, suivi de la récupération des erreurs et<br>visionneuses simultanéesVous pouvez effectuer le suivi du contenu audio et vidéo téléchargé et lu sur un périphérique, quelle que soit sa connectivité. |



## Sécurité {#security}

Chez Adobe, nous prenons la sécurité de vos ressources numériques au sérieux. De l&#39;intégration rigoureuse de la sécurité dans notre processus et nos outils de développement logiciel interne à nos équipes interfonctionnelles d&#39;intervention en cas d&#39;incident, nous nous efforçons d&#39;être proactifs et flexibles. De plus, notre collaboration avec des partenaires, des chercheurs et d&#39;autres organisations du secteur nous aide à comprendre les dernières menaces et les meilleures pratiques en matière de sécurité, et à renforcer continuellement la sécurité dans les produits et les services que nous offres.


### Sécurité du calque de transport {#transport-layer-security}

**Remarque TLS -** Adobe applique des normes de conformité de sécurité qui exigent la fin de vie des anciens protocoles de sécurité. Pour continuer à répondre aux normes de protocole de sécurité en constante évolution, Adobe se dirige vers l’utilisation de TLS 1.2, afin d’avoir la version la plus récente et la plus sécurisée en usage. A partir du 20 février 2019, Adobe ne prendra en charge que TLS 1.1 ou version ultérieure. Avec cette modification, Adobe ne collectera plus de données provenant d’utilisateurs finaux disposant d’anciens appareils ou navigateurs web qui déploient TLS 1.0. La migration vers TLS 1.2 améliore la sécurité. Il est important que vous passiez en revue les détails et que vous planifiiez les changements pour une transition en douceur.

>[!NOTE]
>
>TLS est actuellement le protocole de sécurité le plus répandu, utilisé pour les navigateurs web et autres applications exigeant que les données soient échangées en toute sécurité sur un réseau.
