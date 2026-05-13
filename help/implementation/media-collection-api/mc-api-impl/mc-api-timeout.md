---
title: Conditions d’expiration
description: Découvrez les conditions d’expiration de l’API Media Collection.
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/13vwFrp3NF-e-odFn3eXIuhHusl14ovkwhTpPYbJC0U
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 165
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
