---
title: Attribution du flux média
seo-title: Attribution du flux média
translation-type: tm+mt
source-git-commit: cc067b31066aa5d7e254167e32429c6c56e40c77

---


# Attribution du flux média

Cette fonctionnalité vous permet de lier les actions de l’application aux données de suivi des médias sans avoir besoin de règles de traitement supplémentaires ni de variables personnalisées.

## Dimensions du média en dehors du suivi des médias

Grâce à l’attribution du flux média, les clients peuvent désormais ajouter n’importe quelle dimension multimédia à tous les autres appels d’analyse, tels que les pages vues et les liens personnalisés. Pendant l’implémentation, vous devez ajouter les paramètres de données contextuelles du média aux appels de suivi Analytics. La liste complète des paramètres de données contextuelles utilisés pour les médias est disponible ici : Paramètres [audio et vidéo.](/help/metrics-and-metadata/audio-video-parameters.md)

Vous devez également réactiver la configuration du suivi des médias à partir de la console d’administration pour chaque rapport pour lequel vous souhaitez activer cette fonctionnalité.

>[!NOTE]
>Les mesures des médias _ne sont pas_ disponibles pour être utilisées en dehors du suivi des médias, car la plupart sont calculées par Media Analytics.
>en fonction des événements de pulsation. En outre, il est important que les mesures des médias ne soient pas gonflées par des mises en oeuvre différentes.

## Comment

L’exemple JavaScript ci-dessous génère un appel de suivi de lien personnalisé dont le nom est défini sur "Bannière Héros".

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Dans les rapports Analytics, vous pouvez utiliser l’ `Show` eVar pour ventiler les données et vous pourrez compter les instances de lien de suivi. Le rapport ressemblerait à ceci :

![](/assets/myShow-rpt-1.png)

## Cas d’utilisation

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)

