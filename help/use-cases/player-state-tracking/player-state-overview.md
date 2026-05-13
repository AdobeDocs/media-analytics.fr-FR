---
title: À propos du suivi de l’état du lecteur
description: Découvrez la fonctionnalité de suivi de l’état du lecteur, dont les exigences et les directives relatives à l’implémentation et au compte rendu des performances des états du lecteur.
exl-id: c678e182-74e4-4f46-8596-7be57e645c66
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/R4ByVgEI65JyN-LFdMX1CCBs4zVyppVgebN9OJxJNMM
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 409
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
