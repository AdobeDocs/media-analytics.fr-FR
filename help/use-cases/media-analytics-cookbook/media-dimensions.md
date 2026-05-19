---
title: Qu’est-ce que l’attribution du flux média ?
description: Apprenez à lier les actions d’application aux données de suivi multimédia sans avoir besoin de règles de traitement supplémentaires ni de variables personnalisées.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/G0RufpSDBB65tr4XJRvPU2keKgKxv1uDviyhqzxEVD4
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e4f5f438-eabb-4c54-9133-b817e3d125f5
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 215
ht-degree: 87%

---

# Attribution des diffusions multimédia {#media-stream-attribution}

L’attribution des diffusions multimédia vous permet de lier les actions d’application aux données de suivi multimédia sans avoir besoin de règles de traitement supplémentaires ni de variables personnalisées.

## Dimensions multimédia en dehors du suivi multimédia

Vous pouvez ajouter des dimensions multimédia aux appels d’analyse tels que les pages vues et les liens personnalisés. Pendant l’implémentation, vous devez ajouter les paramètres de données contextuelles du média aux appels de suivi Analytics.

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
