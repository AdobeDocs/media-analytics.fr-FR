---
title: Gestion des interruptions de l’application lors de la lecture
description: Comment gérer les interruptions du suivi pendant la lecture du média.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Gestion des interruptions de l’application lors de la lecture{#handling-application-interrupts-during-playback}

La lecture dans une application multimédia peut être interrompue de différentes manières : un utilisateur appuie explicitement sur pause ou lorsqu’un utilisateur place l’application en arrière-plan. Quelles que soient les causes d’une interruption de la lecture multimédia, les instructions de suivi sont les mêmes :

1. Call **`trackPause`** when the application is interrupted (goes to background, media pauses, etc.).
1. Call **`trackPlay`** when the application returns to the foreground and/or the media resumes playing.

>[!NOTE]
>
>The Media Analytics team has seen instances where customers called `trackSessionStart` when their app returned from the background. La lecture s’effectue ainsi jusqu’à ce moment-là sans compter le temps total de lecture, ainsi que la perte des marqueurs de progression, des segments, etc. précédents. Instead, call `trackPlay` when the app returns and/or the media resumes playing.

## FAQ about handling application interrupts: {#faq-about-handling-application-interrupts}

* _Pendant combien de temps une application doit-elle être placée en arrière-plan avant que la session ne se ferme ?_

   Si l’application permet la lecture en arrière-plan, elle peut continuer le suivi en appelant nos API. Nous enverrons alors tous nos pings de suivi habituels. Peu d’applications vidéo autorisent la lecture en arrière-plan, à l’exception de YouTube Red. Toutefois, toutes les applications audio le permettent. Si l’application n’autorise pas la lecture en arrière-plan, il est conseillé de rester dans l’état Pause pendant une minute, puis de terminer la session de suivi. L’application ne peut pas continuer à envoyer des pings de mise en pause, car, dans la plupart des cas, elle ne peut pas déterminer si l’utilisateur va revenir pour continuer à regarder le média ou déterminer quand il va être tué. Elle ne peut pas non plus continuer à envoyer des pings lorsque l’application se trouve en arrière-plan.

* _Comment gérer le redémarrage du suivi après que l’application a été placée en arrière-plan pendant longtemps ?_

   L’application doit appeler `trackSessionEnd` pour mettre fin à la session de suivi. À compter de la version 2.1, le kit SDK envoie un ping de fin pour informer le serveur principal de la fermeture de la session de suivi.

* _Comment redémarrer la même session ?_

   Pour obtenir des instructions détaillées sur le redémarrage d’une session de suivi, consultez la page [Reprise manuelle d’une session précédemment fermée.](/help/sdk-implement/cookbook/resuming-inactive.md) Le kit SDK envoie un ping de reprise pour informer le serveur principal que l’utilisateur reprend manuellement la session.

