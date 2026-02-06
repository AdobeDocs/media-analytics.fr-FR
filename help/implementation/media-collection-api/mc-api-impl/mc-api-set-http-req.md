---
title: Définition du type de requête HTTP dans votre lecteur
description: Le corps de la requête pour toutes les requêtes de l’API Media Collection doit être au format JSON. Découvrez comment définir le type de requête de contenu dans votre lecteur.
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 81%

---

# Définition du type de requête HTTP {#setting-the-http-request-type}

Le corps de requête pour toutes les requêtes de l’API Media Collection doit être au format JSON. Vous devez donc définir le type de requête de contenu dans votre lecteur. Par exemple, dans JavaScript, vous définiriez l’en-tête de requête `Content-Type` comme suit :

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```
