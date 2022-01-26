---
title: Configuration d’identifiants utilisateur
description: API permettant de définir les ID utilisateur. Elle sert d’identifiant client unique.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: Media Analytics, API
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 100%

---

# Configuration d’identifiants utilisateur {#set-user-ids}

L’identifiant utilisateur est un identifiant visiteur personnalisé unique défini par l’application pour un utilisateur.

Définissez et obtenez l’ID d’utilisateur unique sur le kit SDK ADBMobile comme suit :

* **Définissez la variable :**

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
