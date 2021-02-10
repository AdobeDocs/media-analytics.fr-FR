---
title: Qu’est-ce que l’attribution du flux média ?
description: Apprenez à lier les actions d’application aux données de suivi multimédia sans avoir besoin de règles de traitement supplémentaires ni de variables personnalisées.
translation-type: ht
source-git-commit: 901539a2095b23f9108a934eb61d182b14ccd9e8
workflow-type: ht
source-wordcount: '231'
ht-degree: 100%

---


# Attribution des diffusions multimédia

Cette fonctionnalité vous permet de lier les actions d’application aux données de suivi multimédia sans avoir besoin de règles de traitement supplémentaires ni de variables personnalisées.

## Dimensions du média en dehors du suivi multimédia

Grâce à l’attribution des diffusions multimédia, les clients peuvent désormais ajouter n’importe quelle dimension multimédia à tous les autres appels d’analyse, tels que les pages vues et les liens personnalisés. Pendant l’implémentation, vous devez ajouter les paramètres de données contextuelles du média aux appels de suivi Analytics. La liste complète des paramètres de données contextuelles utilisés pour les médias est disponible ici : [Paramètres audio et vidéo.](/help/metrics-and-metadata/audio-video-parameters.md)

Vous devez également réactiver la configuration du suivi multimédia à partir de la console d’administration pour chaque rapport pour lequel vous souhaitez activer cette fonctionnalité.

>[!NOTE]
>
>Les mesures multimédia _ne sont pas_ disponibles pour être utilisées en dehors du suivi multimédia, car la plupart sont calculées par Media Analytics en fonction des événements de pulsation. En outre, il est important que les mesures multimédia ne soient pas gonflées par des mises en œuvre différentes.

## Comment

L’exemple JavaScript ci-dessous génère un appel de suivi de lien personnalisé dont le nom est défini sur « Hero Banner ».

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Dans les rapports Analytics, vous pouvez utiliser l’eVar `Show` pour ventiler les données et vous pourrez compter les instances de lien de suivi. Le rapport ressemblerait à ceci :

![](/assets/myShow-rpt-1.png)

## Cas d’utilisation

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
