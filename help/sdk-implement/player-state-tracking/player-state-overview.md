---
title: À propos du suivi de l’état du lecteur
description: Cette rubrique décrit la fonctionnalité de suivi de l’état du lecteur, y compris les exigences et les directives relatives à la mise en œuvre et à la création de rapports portant sur les états du lecteur.
exl-id: c678e182-74e4-4f46-8596-7be57e645c66
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '404'
ht-degree: 100%

---

# À propos du suivi de l’état du lecteur

Pour optimiser votre expérience produit et augmenter la valeur pour votre entreprise, il est important de comprendre le comportement des clients lorsqu’ils regardent des vidéos. Cela inclut le temps passé dans les différents états du lecteur.  Il est également important de disposer de la flexibilité nécessaire pour créer et mesurer de nouveaux états et événements du lecteur selon vos besoins.

Le suivi de l’état du lecteur permet de capturer l’interaction avec la visionneuse tout au long de la lecture à l’aide d’un ensemble standard de variables de solutions pour le plein écran, le sous-titrage codé, le mode muet, le mode « Image dans l’Image » et le mode « En point de mires ».  Le suivi de l’état du lecteur offre également la possibilité de créer des états du lecteur personnalisés. Vous pouvez utiliser les variables du suivi de l’état du lecteur pour la création de rapports dans Analysis Workspace.

Pour capturer les modifications apportées à l’état du lecteur, le suivi de l’état du lecteur met à jour les métadonnées des mesures vidéo. Par exemple, afin de déterminer l’engagement vidéo « réel », le suivi de l’état du lecteur mesure le temps passé avec le son activé par rapport aux vidéos visionnées de manière passive ou sans implication de la part de l’utilisateur lorsque le son est coupé, ou le temps passé en mode normal par rapport au plein écran.

Le suivi de l’état du lecteur offre les avantages suivants :

* Fournit des variables standard qui mesurent les états communs, tels que le passage en plein écran ou l’affichage des sous-titres codés.
* Fournit des variables personnalisables pour mesurer des états personnalisés au cours de la session de lecture.
* Mesure le temps passé dans un état du lecteur personnalisé.
* Mesure plusieurs états pouvant être simultanés.

![Suivi de l’état du lecteur](assets/player_state_tracking.png)

## Conditions

Le suivi de l’état du lecteur requiert l’un des éléments suivants pour la collecte de données :
* SDK Media pour JS 3.0+
* SDK Chromecast 3.0 pour les solutions Adobe Experience Cloud
* Extension Media Analytics (à utiliser avec le SDK Adobe Experience Platform (AEP))
   * Web : Adobe Media Analytics (SDK 3.x) for Audio and Video v1.0+
   * Mobile : Adobe Media Analytics for Audio and Video v2.0+
* API Media Collection

## Instructions

Avant de mettre en œuvre le suivi de l’état du lecteur, tenez compte des instructions suivantes.

* L’état du lecteur est calculé sur l’ensemble des états de lecture (sans fractionnement).
* Vous pouvez mesurer plusieurs états du lecteur simultanément.
* Le nombre maximal d’états du lecteur pouvant être suivis au cours d’une lecture est de 10.
* Les mesures d’état du lecteur sont envoyées à Analytics pour la création de rapports uniquement sur l’appel de fermeture du média.
* La connaissance de l’état de l’application n’est pas conservée après l’arrêt d’un état. Après la fin d’un état, celui-ci doit être redémarré pour continuer le suivi. Pour chaque nouvel état de lecture, l’état du lecteur doit être redémarré.
* Les états du lecteur sont capturés pour chaque session de lecture individuelle ; l’état du lecteur n’est pas calculé sur plusieurs lectures.
