---
title: Conditions d’expiration
description: Découvrez les conditions d’expiration de l’API Media Collection.
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 60%

---

# Conditions de temporisation{#timeout-conditions}

**Conditions de délai d’expiration de l’API Media Collection**

L’API Media Collection, étant sans état, n’utilise pas le même mécanisme que le SDK Media pour émettre un nouvel ID de session en cas de conditions de temporisation. Lorsqu’une condition de temporisation se produit, le serveur principal ferme la session et tous les appels suivants effectués avec cet ID de session sont ignorés. La logique qui gère une temporisation de session doit être gérée dans le client. En d’autres termes, le lecteur doit surveiller les conditions de temporisation et obtenir un nouvel ID de session si une temporisation se produit.

* **10 minutes : aucun événement d’API**

  Si le serveur principal ne reçoit aucun événement d’API, il ferme la session.
* **30 minutes : aucun changement de curseur de lecture**

  Si le curseur de lecture ne se déplace pas pendant 30 minutes (par exemple, l’utilisateur appuie sur Pause et s’en va), le serveur principal ferme la session.

>[!NOTE]
>
>Vous pouvez également forcer la fin d’une session en envoyant une requête `events` avec le type d’événement `sessionEnd`.
