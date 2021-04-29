---
title: Contrôle de l’ordre des événements
description: Contrôle de l’ordre des événements
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
translation-type: tm+mt
source-git-commit: 27694ec83de89980404df7a7cc77fa42b3d1a751
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 4%

---

# Contrôle de l’ordre des événements {#controlling-the-order-of-events}

Le suivi vidéo en flux continu est une opération très dépendante du temps. Les appels de suivi de l’API de collecte de médias arrivent parfois en arrière-plan hors service. Dans ce cas, l’arrière-plan tente de mettre en file d’attente et de réorganiser les événements en fonction de l’horodatage fourni dans l’objet `playerTime`.  Cela se produit avec certaines limites. Actuellement, la réorganisation peut échouer si les retards entre les appels en rupture de commande sont de plus d’une seconde. Dans les futures mises à jour, le &quot;délai acceptable&quot; peut être optimisé et configurable.

## Exemple de événement hors service

Des événements hors service se produisent lorsque des événements traversent le réseau, ce qui entraîne parfois des retards.

Par exemple, vous pouvez envoyer un événement `adBreakStart` suivi d’un événement `adStart`. Il s’agit d’un cas d’utilisation courant, car il est nécessaire pour qu’une publicité se début au sein d’une coupure publicitaire.

Si la publicité est prête et qu’aucun tampon n’est nécessaire, les deux événements se produisent presque instantanément et le `playerTime.ts` pour les deux événements sont très proches les uns des autres, mais ils ne devraient jamais être égaux.

> &quot;playerTime.ts&quot; des événements ne devrait jamais être égal à un événement, puisque l&#39;algorithme de tri ne saurait pas quel événement s&#39;est produit en premier. Il doit y avoir au moins 1 milliseconde de différence d&#39;horodatage pour chaque 2 événements consécutifs.

Parce que les deux événements se produisent très près l&#39;un de l&#39;autre dans le temps quand ils déclenchent des appels réseau, il est possible qu&#39;ils arrivent en panne. Dans cet exemple, le événement `adStart` arrive avant le événement `adBreakStart`.


Il y a une fenêtre de événements temporisée : 5 secondes ou un maximum de 10 événements. Les événements sont mis en mémoire tampon avant de les envoyer au pipeline de traitement. Lorsque les conditions sont remplies : 5 secondes ont passé ou plus de 10 événements sont reçus, les événements sont réorganisés en fonction de `playerTime.ts` puis envoyés dans la nouvelle commande, au pipeline de traitement.

>[!IMPORTANT]
>
>Il existe un événement d&#39;exception qui est envoyé immédiatement au pipeline de traitement, c&#39;est-à-dire le événement `sessionStart`.
