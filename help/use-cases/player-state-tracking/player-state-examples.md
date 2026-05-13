---
title: Exemples de suivi de l’état du lecteur
description: Cette rubrique comprend des exemples de la fonctionnalité de suivi de l’état du lecteur.
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eJ9Pb4tWQy0lRhkNXmexUyflt3qT0105FM--jAsGldQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 120
ht-degree: 100%

---

# Exemples de suivi de l’état du lecteur


## Exemple de pause longue

Lorsqu’une session vidéo présente une durée de pause supérieure à 30 minutes, l’API requiert une nouvelle session. Dans ce cas, le client doit générer un nouvel ID de session. Pour les deux sessions vidéo, le client doit conserver tous les états dans lesquels se trouve un lecteur et envoyer toutes les informations en tant qu’événement `stateStart` immédiatement après l’appel `sessionStart`.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

Une fois que la `sessionEnd` est envoyée, une nouvelle session vidéo doit être lancée. Les premiers événements d’API sont les suivants :

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

L’exemple de pause longue montre que le lecteur stocke également ses états afin de pouvoir les envoyer à la nouvelle session vidéo.
