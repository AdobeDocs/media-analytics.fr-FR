---
title: Contrôle de l’ordre des événements
description: Découvrez comment contrôler l’ordre des événements et comment, dans certains cas, les événements sont réorganisés en fonction de la date et l’heure fournies dans l’objet playerTime.
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/LSKiNN-obuHzVYKbAai52SQ2MvI6-gzgb-G-x0DH2dE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 331
ht-degree: 73%

---

# Contrôle de l’ordre des événements{#controlling-the-order-of-events}

Le suivi vidéo en flux continu est une opération qui dépend énormément du temps. Les appels de suivi de l’API de collecte de médias arrivent parfois au serveur principal dans le désordre. Dans un tel cas, le serveur principal tente de mettre en file d’attente et de réorganiser les événements en fonction de l’horodatage fourni et de l’objet `playerTime`.  Cela se produit avec certaines limites. Actuellement, la réorganisation peut échouer si les délais entre les appels dans le désordre dépassent une seconde. Dans les futures mises à jour, le « délai acceptable » peut être optimisé et configurable.

## Exemple d’événement dans le désordre

Des événements dans le désordre se produisent lorsque des événements traversent le réseau, ce qui entraîne parfois des retards.

Par exemple, vous pouvez envoyer un événement `adBreakStart` suivi d’un événement `adStart`. Il s’agit d’un cas d’utilisation courant, car cela est nécessaire pour qu’une publicité démarre au sein d’une coupure publicitaire.

Si la publicité est prête et qu’aucune mémoire tampon n’est nécessaire, les deux événements se produisent presque instantanément et les `playerTime.ts` des deux événements sont très proches. Toutefois, ils ne doivent jamais être égaux, car l’algorithme de tri ne saurait pas savoir quel événement s’est produit en premier. Conservez toujours une différence d’horodatage d’au moins 1 milliseconde pour les événements consécutifs.

Les deux événements se produisant à un moment très proche lors du déclenchement des appels au réseau, il est possible qu’ils arrivent dans le désordre. Dans cet exemple, l’événement `adStart` arrive avant l’événement `adBreakStart`.

Il y a une fenêtre d’événements temporelle : 5 secondes ou un maximum de 10 événements. Les événements sont mis en mémoire tampon avant d’être envoyés au pipeline de traitement. Lorsque les conditions sont remplies (5 secondes se sont écoulées ou plus de 10 événements sont reçus), les événements sont réorganisés en fonction de la `playerTime.ts`, puis envoyés dans la nouvelle commande au pipeline de traitement.

>[!IMPORTANT]
>
>Il existe un événement d’exception qui est immédiatement envoyé au pipeline de traitement. Il s’agit de l’événement `sessionStart`.
