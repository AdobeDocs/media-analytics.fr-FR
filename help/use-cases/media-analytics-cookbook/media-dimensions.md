---
title: Qu’est-ce que l’attribution du flux média ?
description: Apprenez à lier les actions d’application aux données de suivi multimédia sans avoir besoin de règles de traitement supplémentaires ni de variables personnalisées.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 88%

---

# Attribution des diffusions multimédia {#media-stream-attribution}

L’attribution des diffusions multimédia vous permet de lier les actions d’application aux données de suivi multimédia sans avoir besoin de règles de traitement supplémentaires ni de variables personnalisées.

## Dimensions multimédia en dehors du suivi multimédia

Vous pouvez ajouter des dimensions multimédia aux appels d’analyse tels que les pages vues et les liens personnalisés. Pendant l’implémentation, vous devez ajouter les paramètres de données contextuelles du média aux appels de suivi Analytics. Pour afficher la liste complète des paramètres de données contextuelles disponibles utilisés pour le média, voir [Paramètres audio et vidéo](/help/implementation/variables/audio-video-parameters.md).

Pour activer cette fonction pour un rapport spécifique, réactivez la configuration du suivi multimédia à partir de l’Admin Console.

>[!NOTE]
>
>Les mesures multimédia ne sont _pas_ disponibles en dehors du suivi multimédia, car la plupart d’entre elles sont calculées par les services de médias en flux continu en fonction des événements Heartbeat. En outre, il est important que les mesures multimédia ne soient pas gonflées par des implémentations différentes.

## Utiliser l’attribution des diffusions multimédia

L’exemple JavaScript ci-dessous génère un appel de suivi de lien personnalisé dont le nom est défini sur « Bannière principale ».

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Dans les rapports Analytics, vous pouvez utiliser l’eVar `Show` pour ventiler les données et vous pourrez compter les instances de lien de suivi. Le rapport ressemblerait à ceci :

![](/assets/myShow-rpt-1.png)

## Cas d’utilisation

Les exemples suivants présentent des cas d’utilisation pour les éléments suivants :

* Emplacement des catégories
* Emplacement du héros
* Engagement
* Abonnements

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
