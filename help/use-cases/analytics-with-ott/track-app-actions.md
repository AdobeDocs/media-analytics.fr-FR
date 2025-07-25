---
title: Suivi des actions de l’application
description: Les actions de l’application sont des événements qui se produisent dans l’application que vous souhaitez mesurer.
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
exl-id: 88b7d540-67b7-4ec1-8273-02e34853bf60
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 100%

---

# Suivi des actions de l’application{#track-app-actions}

Les actions sont des événements qui se produisent votre application que vous souhaitez mesurer.

Chaque action est associée à une ou à plusieurs mesures qui sont incrémentées chaque fois que l’événement se produit. Par exemple, vous pourriez envoyer un appel `trackAction` à chaque nouvel abonnement, à chaque évaluation du contenu ou à chaque niveau atteint.

Le suivi des actions n’est pas automatique. Par conséquent, appelez `trackAction` lorsqu’un événement dont vous souhaitez effectuer le suivi se produit, puis mappez l’action avec un événement personnalisé.

1. Lorsqu’un événement dont vous souhaitez effectuer le suivi se produit, appelez `trackAction`.

   * **Roku :**

     ```js
     ADBMobile().trackAction("myapp.ActionName", {})
     ```

   * **Chromecast :**

     ```js
     ADBMobile.analytics.trackAction("myapp.ActionName", {});
     ```

1. Mappez l’action avec un événement personnalisé.

   * **Roku :**

     ```js
     dictionary = {} 
     dictionary["myapp.social.SocialSource"] = "Twitter"  
     ADBMobile().trackAction("myapp.SocialShare", dictionary)
     ```

   * **Chromecast :**

     ```js
     var dictionary = {}; 
     dictionary["myapp.social.SocialSource"] = "Twitter"; 
     ADBMobile.analytics.trackAction("myapp.SocialShare", dictionary);
     ```

Vous pouvez également envoyer des données contextuelles supplémentaires à chaque appel de suivi d’action.
