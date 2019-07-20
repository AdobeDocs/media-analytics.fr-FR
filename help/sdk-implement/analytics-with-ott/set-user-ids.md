---
seo-title: Configuration d’identifiants utilisateur
title: Configuration d’identifiants utilisateur
uuid: fdd 54 fec -79 cd -4 bf 8-b 17 e -4 d 61 d 84 f 6310
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
