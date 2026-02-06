---
title: Suivi des états de l’application
description: Les états correspondent aux différents écrans ou affichages dans votre application. Découvrez comment effectuer le suivi de l’état de l’application dans votre application à l’aide de l’appel trackState.
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
exl-id: bb1e0eee-7c59-40b4-9359-a7441b9686b8
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 100%

---

# Suivi des états de l’application{#track-app-states}

Les états correspondent aux différents écrans ou affichages de votre application. Chaque fois qu’un nouvel état est affiché dans votre application, vous devez envoyer un appel `trackState`. Par exemple, lorsqu’un utilisateur navigue de la page d’accueil vers l’écran des détails de la vidéo, envoyez un appel `trackState`. Les états sont généralement consultés au moyen d’un rapport de cheminement afin de découvrir comment les utilisateurs naviguent dans votre application et les états les plus vus.

## Appels trackState

Vous appelez généralement `trackState` chaque fois que l’application charge un nouvel écran.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

Le nom de l’état est signalé dans la variable « View State » dans Adobe Mobile Services, et un affichage est enregistré pour chaque appel `trackState`. Dans d’autres interfaces Analytics, la variable « View State » est signalée en tant que « Page Name » et « State Views » est signalée en tant que « Page Views ».

## Envoi de données contextuelles

Outre « State Name », vous pouvez envoyer des données contextuelles supplémentaires avec chaque appel d’action de suivi.

### Roku

```js
dictionary = { } 
dictionary["myapp.login.LoginStatus"] = "logged in"  
ADBMobile().trackState("Home Screen", dictionary)
```

### Chromecast

```js
var dictionary = { }; 
dictionary["myapp.login.LoginStatus"] = "logged in"; 
ADBMobile.analytics.trackState("Home Screen", dictionary); 
```

>[!NOTE]
>
>Les valeurs des données contextuelles doivent être mises en correspondance avec des variables personnalisées dans Adobe Mobile Services.
