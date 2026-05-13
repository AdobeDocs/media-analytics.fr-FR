---
title: Suivi des états de l’application
description: Les états correspondent aux différents écrans ou affichages dans votre application. Découvrez comment effectuer le suivi de l’état de l’application dans votre application à l’aide de l’appel trackState.
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
exl-id: bb1e0eee-7c59-40b4-9359-a7441b9686b8
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/fVNQ4CIqXbSYyi32rBlB2B9S6YTsBwxJhD3XaeDcDIE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 188
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
