---
seo-title: Conditions d’expiration
title: Conditions d’expiration
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Conditions d’expiration{#timeout-conditions}

**Conditions de délai d’expiration de l’API de collecte de médias**

L’API Media Collection, étant sans état, ne dispose pas du même mécanisme que le SDK Media pour émettre un nouvel ID de session lorsque des conditions de délai d’expiration se produisent. Lorsqu’une condition d’expiration se produit, le serveur principal ferme la session, et tous les appels suivants effectués avec cet ID de session sont abandonnés. La logique qui gère une expiration de session doit être traitée par le client. En d’autres termes, le lecteur doit surveiller les conditions d’expiration et obtenir un nouvel ID de session en cas d’expiration.

* **10 minutes : Aucun événement d’API**

   Si le serveur principal ne reçoit aucun événement API, il ferme la session.
* **30 minutes : Aucun changement de tête de lecture**

   Si le curseur de lecture ne bouge pas pendant 30 minutes (par exemple, si l’utilisateur appuie sur Pause et s’éloigne), l’arrière-plan ferme la session.

>[!NOTE]
>
>You can also force a session end by sending an `events` request with the `sessionEnd` event type.

