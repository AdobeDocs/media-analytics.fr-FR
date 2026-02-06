---
title: Configuration d’identifiants utilisateur
description: API permettant de définir les ID utilisateur. Elle sert d’identifiant client unique.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: "Streaming Media, API"
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 45%

---

# Configuration d’identifiants utilisateur {#set-user-ids}

L’identifiant utilisateur est un identifiant visiteur personnalisé unique défini par l’application pour un utilisateur.

Définissez et obtenez l’ID d’utilisateur unique sur ADBMobile SDK comme suit :

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
