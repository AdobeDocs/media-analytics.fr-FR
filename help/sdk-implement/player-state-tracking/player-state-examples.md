---
title: Exemples de suivi de l'état du lecteur
description: Cette rubrique comprend des exemples de la fonction de suivi de l’état du lecteur.
translation-type: tm+mt
source-git-commit: 1c2992d2a5992b07fa24823501d542c1878aa296
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# Exemples de suivi de l&#39;état du lecteur


## Exemple de longue pause

Lorsqu’une session vidéo présente une durée de pause supérieure à 30 minutes, l’API requiert une nouvelle session. Dans ce cas, le client doit générer un nouvel ID de session. Pour les deux sessions vidéo, le client doit conserver tous les états dans lesquels se trouve un lecteur et envoyer toutes les informations en tant que `stateStart` événement juste après l’ `sessionStart` appel.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd
`

Une fois que la `sessionEnd` vidéo est envoyée, une nouvelle session vidéo doit être lancée et les premiers événements d’API sont les suivants :

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

L’exemple de longue pause montre que le lecteur stocke également ses états afin de pouvoir les envoyer à la nouvelle session vidéo.
