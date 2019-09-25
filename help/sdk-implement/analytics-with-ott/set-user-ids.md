---
seo-title: Configuration d’identifiants utilisateur
title: Configuration d’identifiants utilisateur
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Configuration d’identifiants utilisateur{#set-user-ids}

L’identifiant utilisateur est un identifiant visiteur personnalisé unique défini par l’application pour un utilisateur.

Définissez et obtenez l’identifiant utilisateur unique sur le kit SDK ADBMobile comme suit :

* **Définir :**

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
