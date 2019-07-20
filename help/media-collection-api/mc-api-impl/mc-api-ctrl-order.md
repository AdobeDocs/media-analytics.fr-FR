---
seo-title: Contrôle de l’ordre des événements
title: Contrôle de l’ordre des événements
uuid: 007 fccc 6-be 72-4 b 79-826 d -588 c 957 ccf 15
translation-type: tm+mt
source-git-commit: 6e13e9a6250949a3a7f059445da772b4db1fdb71

---


# Contrôle de l’ordre des événements{#controlling-the-order-of-events}

Comme l'API de collecte de médias est restful, et que le suivi vidéo est une opération très tributaire du temps, un implémenteur peut être inquiet quant aux appels de suivi de l'API de collection multimédia arrivant à l'arrière-plan. Le serveur principal *tente* de mettre en file d’attente et de réordonner les événements en fonction de l’horodatage fourni et de l’objet `playerTime`. Il y a toutefois une limite à cette fonctionnalité. Actuellement, la réorganisation peut échouer si les délais entre les appels désordonnés dépassent une seconde. Ce « délai acceptable » pourra être optimisé et/ou configurable dans les futures mises à jour.
