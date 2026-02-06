---
title: Gestion des interruptions de l’application lors de la lecture
description: Découvrez comment gérer les interruptions du suivi pendant la lecture du média.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 63%

---

# Gestion des interruptions de l’application lors de la lecture{#handling-application-interrupts-during-playback}

La lecture dans une application multimédia peut être interrompue de différentes manières. Par exemple, un utilisateur peut appuyer explicitement sur pause ou l’utilisateur peut mettre l’application en arrière-plan. Quelle que soit la cause de l’interruption de la lecture multimédia, les instructions de suivi sont les mêmes.

1. Appelez **`trackPause`** lorsque l’application est interrompue (mise en arrière-plan, pause du média, etc.).
1. Appelez **`trackPlay`** lorsque l’application revient au premier plan et/ou que la lecture du média reprend.

>[!NOTE]
>
>L’appel de `trackSessionStart` lorsque l’application revient de l’arrière-plan peut entraîner le non-comptage de la lecture jusqu’à ce point par rapport au temps de lecture total, ainsi que la perte des marques de progression antérieures, des segments, etc. À la place, appelez `trackPlay` lorsque l’application revient au premier plan et/ou que la lecture du média reprend.

## FAQ sur la gestion des interruptions de l’application : {#faq-about-handling-application-interrupts}

* _Pendant combien de temps une application doit-elle être mise en arrière-plan avant la fermeture de la session ?_

  Si l’application autorise la lecture en arrière-plan, elle peut continuer à effectuer le suivi en appelant nos API et nous enverrons tous nos pings de suivi réguliers. Peu d’applications vidéo autorisent la lecture en arrière-plan, à l’exception de YouTube Red. Toutefois, toutes les applications audio le permettent. Si l’application ne permet pas la lecture en arrière-plan, il est recommandé de rester en état de pause pendant 1 minute, puis de mettre fin à la session de suivi. L’application ne peut pas continuer à envoyer des pings de pause, car dans la plupart des cas, elle n’est pas en mesure de déterminer si l’utilisateur va reprendre le visionnage du contenu média ou s’il va le fermer. Il est également déconseillé de continuer à envoyer des pings en arrière-plan.

* _Quelle est la bonne façon de gérer le redémarrage du suivi après que l’application a été en arrière-plan pendant longtemps ?_

  L’application doit appeler `trackSessionEnd` pour mettre fin à la session de suivi. À partir de la version 2.1, le SDK envoie un ping « de fin » pour informer le serveur principal de la fermeture de la session de suivi.

* _Que diriez-vous de redémarrer la même session ?_

  Pour plus d’informations sur la reprise d’une session de suivi, voir la section [Reprise des sessions inactives](resuming-inactive.md). Le SDK envoie un ping de reprise pour informer le serveur principal que l’utilisateur(utilisatrice) reprend manuellement la session.
