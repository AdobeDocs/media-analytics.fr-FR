---
seo-title: Gestion des interruptions de l’application lors de la lecture
title: Gestion des interruptions de l’application lors de la lecture
uuid: 1 ccb 4507-bda 6-462 d-bf 67-e 22978 a 4 db 3 d
translation-type: tm+mt
source-git-commit: 8c9592ee7ad97de2cf4aefb226ed1390bc5b53a8

---


# Gestion des interruptions de l’application lors de la lecture{#handling-application-interrupts-during-playback}

La lecture dans une application multimédia peut être interrompue de différentes manières : un utilisateur appuie explicitement sur Pause ou lorsqu'un utilisateur place l'application dans l'arrière-plan. Quelles que soient les causes d'une interruption de lecture multimédia, les instructions de suivi sont les mêmes :

1. Call **`trackPause`** when the application is interrupted (goes to background, media pauses, etc.).
1. Call **`trackPlay`** when the application returns to the foreground and/or the media resumes playing.

>[!NOTE]
>
>The Media Analytics team has seen instances where customers called `trackSessionStart` when their app returned from the background. Ainsi, la lecture jusqu'à ce point n'est pas comptabilisée jusqu'à la durée totale de lecture, avec ainsi perdre des marqueurs de progression, des segments, etc. Instead, call `trackPlay` when the app returns and/or the media resumes playing.

## FAQ about handling application interrupts: {#section_osf_xqs_h2b}

* _Pendant combien de temps une application doit-elle être placée en arrière-plan avant que la session ne se ferme ?_

   Si l’application permet la lecture en arrière-plan, elle peut continuer le suivi en appelant nos API. Nous enverrons alors tous nos pings de suivi habituels. Peu d'applications vidéo autorisent la lecture en arrière-plan, à l'exception de YouTube rouge. Toutefois, toutes les applications audio autorisent cette opération. Si l'application n'autorise pas la lecture en arrière-plan, il est conseillé de rester dans l'état Pause pendant une minute, puis de terminer la session de suivi. L'application ne peut pas continuer à envoyer des pures de mise en pause, car dans la plupart des cas, elle ne peut pas déterminer si l'utilisateur va revenir pour poursuivre l'affichage du média ou déterminer quand il sera tué. Elle ne peut pas non plus continuer à envoyer des pings lorsque l’application se trouve en arrière-plan.

* _Comment gérer le redémarrage du suivi après que l’application a été placée en arrière-plan pendant longtemps ?_

   L’application doit appeler `trackSessionEnd` pour mettre fin à la session de suivi. À compter de la version 2.1, le kit SDK envoie un ping de fin pour informer le serveur principal de la fermeture de la session de suivi.

* _Comment redémarrer la même session ?_

   Pour obtenir des instructions détaillées sur le redémarrage d’une session de suivi, consultez la page [Reprise manuelle d’une session précédemment fermée.](../../sdk-implement/cookbook/resuming-inactive.md) Le kit SDK envoie un ping de reprise pour informer le serveur principal que l’utilisateur reprend manuellement la session.

