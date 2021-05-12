---
title: Contrôle de l’ordre des événements
description: Contrôle de l’ordre des événements
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
source-git-commit: 27694ec83de89980404df7a7cc77fa42b3d1a751
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 100%

---

# Contrôle de l’ordre des événements {#controlling-the-order-of-events}

Le suivi vidéo en flux continu est une opération qui dépend énormément du temps. Les appels de suivi de l’API de collecte de médias arrivent parfois au serveur principal dans le désordre. Dans un tel cas, le serveur principal tente de mettre en file d’attente et de réorganiser les événements en fonction de l’horodatage fourni et de l’objet `playerTime`.  Cela se produit avec certaines limites. Actuellement, la réorganisation peut échouer si les délais entre les appels dans le désordre dépassent une seconde. Dans les futures mises à jour, le « délai acceptable » peut être optimisé et configurable.

## Exemple d’événement dans le désordre

Des événements dans le désordre se produisent lorsque des événements traversent le réseau, ce qui entraîne parfois des retards.

Par exemple, vous pouvez envoyer un événement `adBreakStart` suivi d’un événement `adStart`. Il s’agit d’un cas d’utilisation courant, car cela est nécessaire pour qu’une publicité démarre au sein d’une coupure publicitaire.

Si la publicité est prête et qu’aucune mémoire tampon n’est nécessaire, les deux événements se produisent presque instantanément et les variables `playerTime.ts` des deux événements sont très proches. Toutefois, elles ne doivent jamais être égales.

> Les variables « playerTime.ts » des événements ne doivent jamais être égales pour un événement, car l’algorithme de tri ne saurait alors pas déterminer quel événement s’est produit en premier. Il doit y avoir au moins 1 milliseconde de différence d’horodatage chaque fois que l’on compte 2 événements consécutifs.

Les deux événements se produisant à un moment très proche lors du déclenchement des appels au réseau, il est possible qu’ils arrivent dans le désordre. Dans cet exemple, l’événement `adStart` arrive avant l’événement `adBreakStart`.


Il y a une fenêtre d’événements temporelle : 5 secondes ou un maximum de 10 événements. Les événements sont mis en mémoire tampon avant d’être envoyés au pipeline de traitement. Lorsque les conditions sont remplies, c’est-à-dire lorsque 5 secondes se sont écoulées ou lorsque plus de 10 événements ont été reçus, les événements sont réorganisés en fonction de `playerTime.ts` avant d’être envoyés dans la nouvelle commande, au pipeline de traitement.

>[!IMPORTANT]
>
>Il existe un événement d’exception qui est immédiatement envoyé au pipeline de traitement. Il s’agit de l’événement `sessionStart`.
