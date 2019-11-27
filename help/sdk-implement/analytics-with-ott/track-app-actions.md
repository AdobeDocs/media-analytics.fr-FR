---
title: Suivi des actions de l’application
description: Les actions de l’application sont des événements qui se produisent dans l’application que vous souhaitez mesurer.
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Suivi des actions d’application {#track-app-actions}

Les actions sont les événements qui se produisent dans votre application et que vous souhaitez mesurer.

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

