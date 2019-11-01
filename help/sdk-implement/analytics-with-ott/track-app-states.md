---
title: Suivi des états de l’application
description: 'Les états d’application sont les différents écrans ou affichages de votre application, qui, lorsqu’ils sont affichés, doivent déclencher un appel trackState. '
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Suivi des états d’application{#track-app-states}

Les états correspondent aux différents écrans ou affichages de votre application. Chaque fois qu’un nouvel état est affiché dans votre application, vous devez envoyer un `trackState` appel. Par exemple, lorsqu’un utilisateur navigue de la page d’accueil vers l’écran des détails de la vidéo, envoyez un `trackState` appel. Les états sont généralement consultés au moyen d’un rapport de cheminement afin de découvrir comment les utilisateurs naviguent dans votre application et les états les plus vus.

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

The state name is reported in the "View State" variable in Adobe Mobile services, and a view is recorded for each `trackState` call. Dans d’autres interfaces Analytics, l’état d’affichage est signalé comme "Nom de page" ; "Vues d’état" est signalé comme "Pages vues".

## Envoyer des données contextuelles

Outre "Nom d’état", vous pouvez envoyer des données contextuelles supplémentaires avec chaque appel d’état de suivi.

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
>Les valeurs de données contextuelles doivent être mises en correspondance avec des variables personnalisées dans Adobe Mobile Services.

