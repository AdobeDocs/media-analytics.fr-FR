---
title: Configuration d’identifiants utilisateur
description: API permettant de définir les ID utilisateur, le serveur en tant qu’identifiant client unique.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Configuration d’identifiants utilisateur{#set-user-ids}

L’identifiant utilisateur est un identifiant visiteur personnalisé unique défini par l’application pour un utilisateur.

Définissez et obtenez l’identifiant utilisateur unique sur le kit SDK ADBMobile comme suit :

* **Définissez la variable:**

   * **Roku :**

      ```
      ADBMobile().setUserIdentifer("app-generated-unique-id")
      ```

   * **Chromecast :**

      ```
      ADBMobile().config.setUserIdentifer("app-generated-unique-id");
      ```

* **Obtenir :**

   * **Roku :**

      ```
      vid = ADBMobile().userIdentifer()
      ```

   * **Chromecast :**

      ```
      vid = ADBMobile().config.getUserIdentifer();
      ```
