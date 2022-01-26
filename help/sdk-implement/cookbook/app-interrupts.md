---
title: Gestion des interruptions de l’application lors de la lecture
description: Découvrez comment gérer les interruptions du suivi pendant la lecture du média.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 100%

---

# Gestion des interruptions de l’application lors de la lecture{#handling-application-interrupts-during-playback}

Dans une application multimédia, la lecture peut être interrompue de différentes façons : par exemple lorsqu’un utilisateur appuie sur le bouton de pause ou place l’application en arrière-plan. Quelle que soit la cause de l’interruption de la lecture multimédia, les instructions de suivi sont les mêmes :

1. Appelez **`trackPause`** lorsque l’application est interrompue (mise en arrière-plan, pause du média, etc.).
1. Appelez **`trackPlay`** lorsque l’application revient au premier plan et/ou que la lecture du média reprend.

>[!NOTE]
>
>L’équipe médias Analytics a déjà vu des clients qui appelaient `trackSessionStart` lorsque leur application revenait au premier plan. En procédant ainsi, la durée totale de lecture reprendra à zéro et vous perdrez les marqueurs de progression, segments, etc. À la place, appelez `trackPlay` lorsque l’application revient au premier plan et/ou que la lecture du média reprend.

## FAQ sur la gestion des interruptions de l’application : {#faq-about-handling-application-interrupts}

* _Pendant combien de temps une application doit-elle être placée en arrière-plan avant que la session ne se ferme ?_

   Si l’application permet la lecture en arrière-plan, elle peut continuer le suivi en appelant nos API. Nous enverrons alors tous nos pings de suivi habituels. Peu d’applications vidéo autorisent la lecture en arrière-plan, à l’exception de YouTube Red. Toutefois, toutes les applications audio le permettent. Si l’application ne permet pas la lecture en arrière-plan, il est recommandé de rester en état de pause pendant 1 minute, puis de mettre fin à la session de suivi. L’application ne peut pas continuer à envoyer des pings de pause, car dans la plupart des cas, elle n’est pas en mesure de déterminer si l’utilisateur va reprendre le visionnage du contenu média ou s’il va le fermer. Elle ne peut pas non plus continuer à envoyer des pings lorsque l’application se trouve en arrière-plan.

* _Comment gérer le redémarrage du suivi après que l’application a été placée en arrière-plan pendant longtemps ?_

   L’application doit appeler `trackSessionEnd` pour mettre fin à la session de suivi. À compter de la version 2.1, le kit SDK envoie un ping de fin pour informer le serveur principal de la fermeture de la session de suivi.

* _Comment redémarrer la même session ?_

   Pour obtenir des instructions détaillées sur le redémarrage d’une session de suivi, consultez la page [Reprise manuelle d’une session précédemment fermée](/help/sdk-implement/cookbook/resuming-inactive.md). Le kit SDK envoie un ping de reprise pour informer le serveur principal que l’utilisateur reprend manuellement la session.
