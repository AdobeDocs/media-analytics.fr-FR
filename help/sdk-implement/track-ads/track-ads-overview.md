---
seo-title: Aperçu
title: Aperçu
uuid: 1607798 b-c 6 ef -4 d 60-8 e 40-e 958 c 345 b 09 c
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Aperçu{#overview}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre à l'aide des SDK 2. x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

La lecture de publicité inclut le suivi des coupures publicitaires, des démarrages de publicité, des fins de publicité et des publicités ignorées. Utilisez l'API du lecteur multimédia pour identifier les événements clés du lecteur et renseigner les variables publicitaires obligatoires et facultatives. See the comprehensive list of metadata here: [Ad parameters.](/help/metrics-and-metadata/ad-parameters.md)

## Player events {#player-events}


### Démarrage de la coupure publicitaire

>[!NOTE]
>Inclusion de preroll

* Créez une instance d’objet `adBreak` pour la coupure publicitaire. Par exemple : `adBreakObject`.

* Call `trackEvent` for the ad break start with your `adBreakObject`.

### À chaque démarrage de ressource de publicité

* Créez une instance d’objet publicitaire pour la ressource de publicité. Par exemple : `adObject`.
* Populate the ad metadata, `adCustomMetadata`.
* Appelez `trackEvent` pour le démarrage de publicité.

### À chaque fin de publicité

* Appelez `trackEvent` pour la fin de publicité.

### Lorsqu’une publicité est ignorée

* Appelez `trackEvent` pour le saut de publicité.

### À la fin de la coupure publicitaire

* Appelez `trackEvent` pour la fin de la coupure publicitaire.

## Implement ad tracking {#section_83E0F9406A7743E3B57405D4CDA66F68}

### Constantes de suivi des publicités

| Nom de constante | Description   |
|---|---|
| `AdBreakStart` | Constante permettant d’effectuer le suivi de l’événement AdBreak Start |
| `AdBreakComplete` | Constante permettant d’effectuer le suivi de l’événement AdBreak Complete |
| `AdStart` | Constante permettant d’effectuer le suivi de l’événement Début de la publicité |
| `AdComplete` | Constante permettant d’effectuer le suivi de l’événement Fin de la publicité |
| `AdSkip` | Constante permettant d’effectuer le suivi de l’événement Saut de publicité |

### Procédure de mise en œuvre

1. Identifiez le moment où la limite de coupure publicitaire commence, y compris preroll, et créez un `AdBreakObject` à l’aide des informations de coupure publicitaire.

   `AdBreakObject` référence :

   | Nom de variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom de la coupure publicitaire tel que preroll, mid-roll et post-roll. | Oui |
   | `position` | Position du numéro de la coupure publicitaire dans le contenu, en commençant par 1. | Oui |
   | `startTime` | Valeur du curseur de lecture au début de la coupure publicitaire. | Oui |

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break.

1. Déterminez le moment où la publicité commence, puis créez une instance `AdObject` à l’aide des informations sur la publicité.

   `AdObject` référence :

   | Nom de variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom convivial de la publicité. | Oui |
   | `adId` | Identifiant unique de la publicité. | Oui |
   | `position` | Position du numéro de la publicité dans la coupure publicitaire, en commençant par 1. | Oui |
   | `length` | Longueur de la publicité | Oui |

1. Vous pouvez joindre des métadonnées standard et/ou de publicité à la session de suivi par le biais de variables de données contextuelles.

   * **Métadonnées de publicité standard -** Pour les métadonnées de publicité standard, créez un dictionnaire de paires clé-valeur de métadonnées de publicité standard à l’aide des clés pour votre plate-forme.
   * **Métadonnées de publicité personnalisées -** Pour les métadonnées personnalisées, créez un objet de variable pour les variables de données personnalisées et renseignez les données de la publicité actuelle.

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback.

   Incluez une référence à votre variable de métadonnées personnalisées (ou un objet vide) comme troisième paramètre dans l’appel d’événement.

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event.

1. Si la lecture de la publicité ne s’est pas terminée car l’utilisateur a choisi d’ignorer la publicité, effectuez le suivi de l’événement `AdSkip`.
1. S’il existe d’autres publicités dans le même `AdBreak`, répétez les étapes 3 à 7.
1. When the ad break is complete, use the `AdBreakComplete` event to track it.

>[!IMPORTANT]
>
>Make sure you do NOT increment the content player playhead (`l:event:playhead`) during ad playback (`s:asset:type=ad`). Si vous le faites, les mesures Durée de la visite du contenu seront compromises.

L'exemple de code suivant utilise le SDK JavaScript 2. x pour un lecteur de médias HTML 5.

```js
/* Call on ad break start */ 
 
if (e.type == "ad break start") { 
    var adBreakObject = MediaHeartbeat.createAdBreakObject("mid-roll", 2, 500); 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject); 
}; 
 
/* Call on ad start */ 
if (e.type == "ad start") { 
    var adObject = MediaHeartbeat.createAdObject("PepsiOne", "123456ab", 1, 30); 
    /* Set custom context data */ 
    var adCustomMetadata = { 
        affiliate:"Sample affiliate", 
        campaign:"Sample ad campaign", 
        creative:"Sample creative" 
    } 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata); 
}; 
 
/* Call on ad complete */ 
if (e.type == "ad complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
}; 
 
/* Call on ad skip */ 
if (e.type == "ad skip") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip); 
}; 
     
/* Call on ad break complete */ 
if (e.type == "ad break complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
}; 
```

## Validation {#section_5F1783F5FE2644F1B94B0101F73D57EB}

### Démarrage de publicité

Au démarrage d’une lecture de publicité spécifique, ces appels clés sont envoyés dans l’ordre suivant :

1. Démarrage de l’analyse de la publicité vidéo
1. Démarrage de la publicité Heartbeat
1. Démarrage de l’analyse Heartbeat

Les appels 1 et 2 contiennent des variables de métadonnées supplémentaires pour les formats personnalisés et standard.

### Lecture de la publicité

Lors de la lecture de la publicité, les appels de lecture de publicité Heartbeat sont envoyés au serveur Heartbeat toutes les secondes.

### Publicité terminée

Au point 100 % sur une publicité, un appel de fin de publicité Heartbeat est envoyé.

### Ignorer la publicité

Lorsqu’une publicité est ignorée, aucun événement n’est envoyé. Les appels de suivi n’incluent donc pas les informations de publicité.

>[!TIP]
>
>Aucun appel unique n'est envoyé au début de la coupure publicitaire et au saut de publicité terminé.

