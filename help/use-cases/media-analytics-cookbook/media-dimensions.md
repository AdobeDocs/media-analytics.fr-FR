---
title: Qu’est-ce que l’attribution du flux média ?
description: Apprenez à lier les actions d’application aux données de suivi multimédia sans avoir besoin de règles de traitement supplémentaires ni de variables personnalisées.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 41%

---

# Attribution des diffusions multimédia {#media-stream-attribution}

Grâce à l’attribution des diffusions multimédia, vous pouvez lier les actions de l’application aux données de suivi multimédia sans avoir besoin de règles de traitement supplémentaires et de variables personnalisées.

## Dimensions du média en dehors du suivi multimédia

Vous pouvez ajouter des dimensions multimédia aux appels d’analyse tels que les pages vues et les liens personnalisés. Pendant l’implémentation, vous devez ajouter les paramètres de données contextuelles du média aux appels de suivi Analytics. Pour afficher la liste complète des paramètres de données contextuelles disponibles utilisés pour le média, voir [Paramètres audio et vidéo.](/help/implementation/variables/audio-video-parameters.md)

Pour activer cette fonction pour un rapport spécifique, réactivez la configuration du suivi multimédia à partir de la console d’administration.

>[!NOTE]
>
>Les mesures multimédia sont les suivantes : _not_ disponibles en dehors du suivi multimédia, car la plupart d’entre elles sont calculées par Streaming Media Analytics en fonction des événements de pulsation. En outre, il est important que les mesures multimédia ne soient pas gonflées par des mises en œuvre différentes.

## Utilisation de l’attribution de diffusion multimédia

L’exemple JavaScript ci-dessous génère un appel de suivi de lien personnalisé dont le nom est défini sur &quot;Hero Banner&quot;.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Dans les rapports Analytics, vous pouvez utiliser l’eVar `Show` pour ventiler les données et vous pourrez compter les instances de lien de suivi. Le rapport ressemblerait à ceci :

![](/assets/myShow-rpt-1.png)

## Cas d’utilisation

Les exemples suivants présentent des cas d’utilisation pour les éléments suivants :

* Emplacement des catégories
* Hero Placement
* Engagement
* Abonnements

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)