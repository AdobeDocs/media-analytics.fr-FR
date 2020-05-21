---
title: A propos du suivi de l'état du lecteur
description: Cette rubrique décrit la fonction de suivi de l’état du lecteur, y compris les exigences et les directives relatives à la mise en oeuvre et à l’rapports des états du lecteur.
translation-type: tm+mt
source-git-commit: 1cf11a6b8971f5be490998bbd855a27bfe366e48
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---


# A propos du suivi de l&#39;état du lecteur

Pour optimiser l’expérience de vos produits et optimiser la valeur de votre entreprise, il est important de comprendre le comportement des clients lors de l’affichage des vidéos. Cela inclut le temps passé dans différents états du lecteur.  Et pour optimiser votre compréhension, vous avez besoin de la flexibilité nécessaire pour créer et mesurer de nouveaux états et événements de lecteur selon vos besoins.

Le suivi de l’état du lecteur permet de capturer l’interaction de la visionneuse au cours de la lecture à l’aide d’un ensemble standard de variables de solution pour le plein écran, le sous-titrage, le silence, l’image dans l’image et la mise au point.  Le suivi de l’état du lecteur offre également la possibilité de créer des états de lecteur personnalisés.  Les variables de suivi d’état du lecteur sont également disponibles pour le rapports dans Analyse Workspace.

Pour capturer les modifications apportées à l’état du lecteur, le suivi de l’état du lecteur met à jour les métadonnées des mesures vidéo. Par exemple, pour déterminer l’engagement vidéo &quot;réel&quot;, le suivi de l’état du lecteur mesure le temps passé avec le son activé par rapport aux vues vidéo passives ou non fiancées lorsque le son est désactivé ou le temps passé en mode normal par rapport au mode plein écran.

Le suivi de l’état du lecteur offre les avantages suivants :

* Fournit des variables standard qui mesurent les états communs, telles que le sous-titrage en plein écran ou sous-titrage
* Fournit des variables personnalisables pour mesurer des états personnalisés au cours d’une session de lecture.
* Mesure le temps passé dans un état de lecteur personnalisé
* Mesure plusieurs états pouvant être simultanés

![Suivi des états du lecteur](assets/player_state_tracking.png)

## Conditions

Le suivi de l’état du lecteur nécessite les éléments suivants pour Media Analytics Extension pour une utilisation avec Adobe Experience Platform (AEP SDK) :
* Web : Adobe Media Analytics (SDK 3.x) pour l’audio et la vidéo v1.0+
* Mobile : Adobe Media Analytics pour l’audio et la vidéo v2.0+

Si vous décidez de ne pas utiliser le SDK AEP, vous pouvez utiliser les éléments suivants avec le suivi de l’état du lecteur :
* SDK Media JS 3.0+
* Version de l’API de collecte de médias ?

## Instructions

Avant de mettre en oeuvre le suivi des états du lecteur, tenez compte des recommandations suivantes.

* L’état du lecteur est calculé sur l’ensemble des états de lecture (sans fractionnement).
* Vous pouvez mesurer plusieurs états du lecteur en même temps.
* Le nombre maximal d’états du lecteur pouvant être suivis au cours d’une lecture est de 10. 
* Les mesures d’état du lecteur sont envoyées à Analytics pour rapports sur l’appel de fermeture du média UNIQUEMENT
* Les états du lecteur sont capturés pour chaque session de lecture individuelle ; l’état du lecteur n’est pas calculé sur plusieurs lectures. 
