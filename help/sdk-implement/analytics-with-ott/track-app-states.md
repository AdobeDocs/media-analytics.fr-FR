---
seo-title: Suivi des états de l’application
title: Suivi des états de l’application
uuid: 2 f 98 fb 43-c 362-4 a 9 b -8732-fa 7 e 963 da 729
translation-type: tm+mt
source-git-commit: 9cdf69e30fa727aeb974213769a7ab61fb05b756

---


# Suivi des états d’application{#track-app-states}

Les états correspondent aux différents écrans ou affichages de votre application. Each time a new state is displayed in your application, you should send a `trackState` call. For example, when a user navigates from the home page to the video details screen, send a `trackState` call. Les états sont généralement consultés au moyen d’un rapport de cheminement afin de découvrir comment les utilisateurs naviguent dans votre application et les états les plus vus.

## Appels trackState

You typically call `trackState` each time the app loads a new screen.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

The state name is reported in the "View State" variable in Adobe Mobile services, and a view is recorded for each `trackState` call. Dans d'autres interfaces Analytics, « Afficher l'état » est signalé comme « Nom de page » ; « Affichages d'état » est signalé comme « Pages vues ».

## Envoi de données contextuelles

Outre le « nom d'état », vous pouvez envoyer des données contextuelles supplémentaires à chaque appel d'état de suivi.

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
>Les valeurs de données contextuelles doivent être associées à des variables personnalisées dans les services Adobe Mobile.

