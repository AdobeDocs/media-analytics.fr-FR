---
seo-title: Suivi des publicités sur JavaScript
title: Suivi des publicités sur JavaScript
uuid: 4 d 81 d 29 c-c 55 d -4 d 48-b 505-3260922712 ff
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Suivi des publicités sur JavaScript{#track-ads-on-javascript}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre à l'aide des SDK 2. x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

## Constantes de suivi des publicités

| Nom de constante | Description   |
|---|---|
| `AdBreakStart` | Constante permettant d’effectuer le suivi de l’événement AdBreak Start |
| `AdBreakComplete` | Constante permettant d’effectuer le suivi de l’événement AdBreak Complete |
| `AdStart` | Constante permettant d’effectuer le suivi de l’événement Début de la publicité |
| `AdComplete` | Constante permettant d’effectuer le suivi de l’événement Fin de la publicité |
| `AdSkip` | Constante permettant d’effectuer le suivi de l’événement Saut de publicité |

## Procédure de mise en œuvre

1. Identifiez le moment où la limite de coupure publicitaire commence, y compris preroll, et créez un `AdBreakObject` à l’aide des informations de coupure publicitaire.

   `AdBreakObject` référence :

   | Nom de variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom de la coupure publicitaire tel que preroll, mid-roll et post-roll. | Oui |
   | `position` | Position du nombre au début de la coupure publicitaire commençant par 1. | Oui |
   | `startTime` | Valeur du curseur de lecture au début de la coupure publicitaire. | Oui |

   Création d’objet de coupure publicitaire :

   ```js
   var adBreakObject =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break:

   ```js
   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);
   ```

1. Déterminez le moment où la publicité commence, puis créez une instance `AdObject` à l’aide des informations sur la publicité.

   `AdObject` référence :

   | Nom de variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom convivial de la publicité. | Oui |
   | `adId` | Identifiant unique de la publicité. | Oui |
   | `position` | Position du numéro de la publicité dans la coupure publicitaire, en commençant par 1. | Oui |
   | `length` | Longueur de la publicité | Oui |

   Création d’objet publicitaire :

   ```js
   var adObject =  
     MediaHeartbeat.createAdObject(<AD_NAME>,  
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. Vous pouvez éventuellement joindre des métadonnées standard et/ou publicitaires à la session de suivi multimédia par le biais de variables de données contextuelles.

   * [Mise en œuvre de métadonnées de publicité standard sur JavaScript](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-js.md)
   * **Métadonnées de publicité personnalisées -** Pour les métadonnées personnalisées, créez un objet de variable pour les variables de données personnalisées et renseignez les données de la publicité actuelle :

      ```js
      /* Set custom context data */ 
      var adCustomMetadata = { 
          affiliate: "Sample affiliate", 
          campaign: "Sample ad campaign", 
          creative: "Sample creative" 
      };
      ```

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback.

   Incluez une référence à votre variable de métadonnées personnalisées (ou un objet vide) comme troisième paramètre dans l’appel d’événement :

   ```js
   _onAdStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                                       adObject,  
                                       adCustomMetadata); 
   };
   ```

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event:

   ```js
   _onAdComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
   };
   ```

1. Si la lecture de la publicité ne s’est pas terminée car l’utilisateur a choisi d’ignorer la publicité, suivez l’événement `AdSkip` :

   ```js
   _onAdSkip = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip); 
   };
   ```

1. S’il existe d’autres publicités dans le même `AdBreak`, répétez les étapes 3 à 7.
1. Lorsque la coupure publicitaire est terminée, utilisez l’événement `AdBreakComplete` pour en effectuer le suivi :

   ```js
   _onAdBreakComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
   };
   ```

Consultez le scénario de suivi [Lecture VOD avec publicités preroll](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) pour en savoir plus.
