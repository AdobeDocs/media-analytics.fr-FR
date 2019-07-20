---
seo-title: Définition du type de requête HTTP dans votre lecteur
title: Définition du type de requête HTTP dans votre lecteur
uuid: b 8 fa 7233-e 654-4 acf-a 9 d 7-14158 cded 13 e
translation-type: tm+mt
source-git-commit: 7f0a6a8d6def094bd669e5924ea76107a4ab3cc1

---


# Setting the HTTP request type {#setting-the-http-request-type}

Le corps de requête pour toutes les requêtes de l’API Media Collection doit être au format JSON. Vous devez donc définir le type de requête de contenu dans votre lecteur. Par exemple, dans JavaScript, vous définiriez l’en-tête de requête `Content-Type` comme suit :

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

