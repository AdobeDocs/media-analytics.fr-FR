---
title: Conditions d’expiration
description: null
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Conditions d’expiration {#timeout-conditions}

**Conditions de délai d’expiration de l’API Media Collection**

L’API Media Collection, étant sans état, n’utilise pas le même mécanisme que le SDK Media pour émettre un nouvel ID de session en cas de conditions d’expiration. Lorsqu’une condition d’expiration se produit, le serveur principal ferme la session, et tous les appels suivants effectués avec cet ID de session sont abandonnés. La logique qui gère une expiration de session doit être traitée par le client. En d’autres termes, le lecteur doit surveiller les conditions d’expiration et obtenir un nouvel ID de session en cas d’expiration.

* **10 minutes : aucun événement d’API**

   Si le serveur principal ne reçoit aucun événement d’API, il ferme la session.
* **30 minutes : aucun changement de curseur de lecture**

   Si le curseur de lecture ne se déplace pas pendant 30 minutes (par exemple, l’utilisateur appuie sur Pause et s’en va), le serveur principal ferme la session.

>[!NOTE]
>
>Vous pouvez également forcer la fin d’une session en envoyant une requête `events` avec le type d’événement `sessionEnd`.

