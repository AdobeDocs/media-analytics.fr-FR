---
title: Contrôle de l’ordre des événements
description: null
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Contrôle de l’ordre des événements{#controlling-the-order-of-events}

Puisque l’API de collecte de médias est RESTful et que le suivi vidéo est une opération très dépendante du temps, un implémenteur peut se préoccuper des appels de suivi de l’API de collecte de médias qui arrivent en arrière-plan hors service. Le serveur principal *tente* de mettre en file d’attente et de réordonner les événements en fonction de l’horodatage fourni et de l’objet `playerTime`. Il y a toutefois une limite à cette fonctionnalité. Actuellement, la réorganisation peut échouer si les délais entre les appels désordonnés dépassent une seconde. Ce « délai acceptable » pourra être optimisé et/ou configurable dans les futures mises à jour.
