---
title: Gestion des interruptions de l’application lors de la lecture
description: Découvrez comment gérer les interruptions du suivi pendant la lecture du média.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/BlL-c1rf5d3juDKHybex9vrPvQsBIiNXVO2ug9LKl0g
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: 473
ht-degree: 41%

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

  Pour plus d’informations sur la reprise d’une session de suivi, voir [Reprise des sessions inactives](resuming-inactive.md).Le SDK envoie un ping de reprise pour informer le serveur principal que l’utilisateur(utilisatrice) reprend manuellement la session.

* _Que se passe-t-il si `trackSessionEnd` est appelé deux fois pour la même session ?_

  Appeler `trackSessionEnd` plusieurs fois pour la même session est sans risque. Le serveur principal ferme la session sur le premier événement et supprime silencieusement tous les événements suivants pour cet ID de session, y compris un second `trackSessionEnd`. Cela signifie que les conditions de concurrence (par exemple, le délai d’inactivité de 30 minutes qui se déclenche au moment où la visionneuse ferme le lecteur) ne produisent pas de données en double.

* _Que se passe-t-il si `trackSessionStart` est appelé alors qu’une session est déjà active ?_

  Le SDK ignore le deuxième appel `trackSessionStart` si la session n’a pas encore été fermée. Si vous devez démarrer une nouvelle session, appelez d’abord `trackSessionEnd` pour fermer explicitement la session en cours, puis appelez `trackSessionStart` pour la nouvelle session.
