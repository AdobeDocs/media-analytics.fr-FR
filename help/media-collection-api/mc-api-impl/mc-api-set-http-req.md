---
title: Définition du type de requête HTTP dans votre lecteur
description: null
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Définition du type de requête HTTP {#setting-the-http-request-type}

Le corps de requête pour toutes les requêtes de l’API Media Collection doit être au format JSON. Vous devez donc définir le type de requête de contenu dans votre lecteur. Par exemple, dans JavaScript, vous définiriez l’en-tête de requête `Content-Type` comme suit :

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

