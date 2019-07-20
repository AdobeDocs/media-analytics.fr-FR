---
seo-title: Conditions d’expiration
title: Conditions d’expiration
uuid: 2 a 4 ea 13 e-a 561-4 adf-b 567-f 980301 b 32 c 8
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Conditions d’expiration{#timeout-conditions}

**Conditions de dépassement de délai de l'API de collection multimédia**

L'API de collecte de médias, étant état sans état, n'a pas le même mécanisme que le SDK Media pour l'émission d'un nouvel ID de session lorsque des conditions d'expiration se produisent. Lorsqu’une condition d’expiration se produit, le serveur principal ferme la session, et tous les appels suivants effectués avec cet ID de session sont abandonnés. La logique qui gère une expiration de session doit être traitée par le client. En d’autres termes, le lecteur doit surveiller les conditions d’expiration et obtenir un nouvel ID de session en cas d’expiration.

* **10 minutes : Aucun événement d'API**

   Si l'arrière-plan ne reçoit pas d'événements d'API, la session est fermée.
* **30 minutes : Aucun changement de tête de lecture**

   Si le curseur de lecture ne se déplace pas pendant 30 minutes (par exemple, l'utilisateur accède à Pause et à la fin de la session), la session arrière ferme la session.

>[!NOTE]
>
>You can also force a session end by sending an `events` request with the `sessionEnd` event type.

