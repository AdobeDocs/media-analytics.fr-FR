---
title: Suivi des publicités sur Android
description: Mettez en oeuvre le suivi des publicités dans les applications Android à l’aide du SDK multimédia.
uuid: 4a4249fb-dc39-4947-a14d-a51d972f32d4
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Suivi des publicités sur Android{#track-ads-on-android}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour l’implémentation à l’aide des SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

## Constantes de suivi des publicités

| Nom de constante | Description |
| --- | --- |
| `MediaHeartbeat.Event.AdBreakStart` | Constante permettant d’effectuer le suivi de l’événement AdBreak Start |
| `MediaHeartbeat.Event.AdBreakComplete` | Constante permettant d’effectuer le suivi de l’événement AdBreak Complete |
| `MediaHeartbeat.Event.AdStart` | Constante permettant d’effectuer le suivi de l’événement Début de la publicité |
| `MediaHeartbeat.Event.AdComplete` | Constante permettant d’effectuer le suivi de l’événement Fin de la publicité |
| `MediaHeartbeat.Event.AdSkip` | Constante permettant d’effectuer le suivi de l’événement Saut de publicité |

## Etapes de mise en oeuvre

1. Identifiez le moment où la limite de coupure publicitaire commence, y compris preroll, et créez un `AdBreakObject` à l’aide des informations de coupure publicitaire.

   `AdBreakObject` référence :

   | Nom de variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom de la coupure publicitaire tel que preroll, mid-roll et post-roll. | Oui |
   | `position` | Position du numéro de la coupure publicitaire dans le contenu, en commençant par 1. | Oui |
   | `startTime` | Valeur du curseur de lecture au début de la coupure publicitaire. | Oui |

   Création d’objet de coupure publicitaire :

   ```java
   MediaObject adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break:

   ```java
   public void onAdBreakStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart,  
                             adBreakInfo,  
                             null); 
   }
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

   ```java
   MediaObject adInfo =  
     MediaHeartbeat.createAdObject(<AD_NAME> 
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. Vous pouvez associer des métadonnées standard et/ou publicitaires à la session de suivi des médias au moyen de variables de données contextuelles.

   * [Mise en œuvre de métadonnées de publicité standard sur Android](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
   * **Métadonnées de publicité personnalisées -** Pour les métadonnées personnalisées, créez un objet de variable pour les variables de données personnalisées et renseignez les données de la publicité actuelle :

      ```java
      // Setting Ad Metadata 
      HashMap<String, String> adMetadata = new HashMap<String, String>(); 
      adMetadata.put("affiliate", "Sample affiliate"); 
      adMetadata.put("campaign", "Sample ad campaign");
      ```

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback.

   Incluez une référence à votre variable de métadonnées personnalisées (ou un objet vide) comme troisième paramètre dans l’appel d’événement :

   ```java
   public void onAdStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                             adInfo,  
                             adMetadata); 
   }
   ```

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event:

   ```java
   public void onAdComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
   }
   ```

1. Si la lecture de la publicité ne s’est pas terminée car l’utilisateur a choisi d’ignorer la publicité, suivez l’événement `AdSkip` :

   ```java
   public void onAdSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdSkip, null, null); 
   }
   ```

1. S’il existe d’autres publicités dans le même `AdBreak`, répétez les étapes 3 à 7.
1. Lorsque la coupure publicitaire est terminée, utilisez l’événement `AdBreakComplete` pour en effectuer le suivi :

   ```java
   public void onAdBreakComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
   }
   ```

Consultez le scénario de suivi [Lecture VOD avec publicités preroll](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) pour en savoir plus.
