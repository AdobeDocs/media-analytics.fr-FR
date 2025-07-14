---
title: Configuration d’identifiants utilisateur
description: API permettant de définir les ID utilisateur. Elle sert d’identifiant client unique.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: "Streaming Media, API"
role: User, Admin, Data Engineer
source-git-commit: 70900e305c3ed7a2be4069c6f296d56f1f6e0966
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
