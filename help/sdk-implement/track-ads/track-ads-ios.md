---
title: Suivi des publicités sur iOS
description: Mettez en oeuvre le suivi des publicités dans les applications iOS à l’aide du SDK multimédia.
uuid: e979e679-cde5-4c30-8f34-867feceac13a
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Suivi des publicités sur iOS{#track-ads-on-ios}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour l’implémentation à l’aide des SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

## Constantes de suivi des publicités

| Nom de constante | Description   |
|---|---|
| `ADBMediaHeartbeatEventAdBreakStart` | Constante permettant d’effectuer le suivi de l’événement AdBreak Start |
| `ADBMediaHeartbeatEventAdBreakComplete` | Constante permettant d’effectuer le suivi de l’événement AdBreak Complete |
| `ADBMediaHeartbeatEventAdStart` | Constante permettant d’effectuer le suivi de l’événement Début de la publicité |
| `ADBMediaHeartbeatEventAdComplete` | Constante permettant d’effectuer le suivi de l’événement Fin de la publicité |
| `ADBMediaHeartbeatEventAdSkip` | Constante permettant d’effectuer le suivi de l’événement Saut de publicité |

## Etapes de mise en oeuvre

1. Identifiez le moment où la limite de coupure publicitaire commence, y compris preroll, et créez un `AdBreakObject` à l’aide des informations de coupure publicitaire.

   `AdBreakObject` référence :

   | Nom de variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom de la coupure publicitaire tel que preroll, mid-roll et post-roll. | Oui |
   | `position` | Position du numéro de la coupure publicitaire dans le contenu, en commençant par 1. | Oui |
   | `startTime` | Valeur du curseur de lecture au début de la coupure publicitaire. | Oui |

   Création d’objet de coupure publicitaire :

   ```
   id adBreakObject = [ADBMediaHeartbeat createAdBreakObjectWithName:[ADBREAK_NAME] 
                               position:[POSITION]  
                               startTime:[START_TIME]];
   ```

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break:

   ```
   - (void)onAdBreakStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                        mediaObject:adBreakObject  
                        data:nil]; 
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

   ```
   id adObject = [ADBMediaHeartbeat createAdObjectWithName:[AD_NAME] 
                                    adId:[AD_ID] 
                                    position:[POSITION] 
                                    length:[LENGTH]];
   ```

1. Vous pouvez associer des métadonnées standard et/ou publicitaires à la session de suivi des médias au moyen de variables de données contextuelles.

   * [Mise en œuvre de métadonnées de publicité standard sur iOS](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
   * **Métadonnées de publicité personnalisées -** Pour les métadonnées personnalisées, créez un objet de variable pour les variables de données personnalisées et renseignez les données de la publicité actuelle :

      ```
      NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init]; 
      [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"]; 
      [adDictionary setObject:@"Sample campaign" forKey:@"campaign"]; 
      [adDictionary setObject:@"Sample creative" forKey:@"creative"];
      ```

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback.

   Incluez une référence à votre variable de métadonnées personnalisées (ou un objet vide) comme troisième paramètre dans l’appel d’événement :

   ```
   - (void)onAdStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                        mediaObject:adObject  
                        data:adDictionary]; 
   }
   ```

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event.

   ```
   - (void)onAdComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Si la lecture de la publicité ne s’est pas terminée car l’utilisateur a choisi d’ignorer la publicité, effectuez le suivi de l’événement `AdSkip`.

   ```
   - (void)onAdSkip:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdSkip  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. S’il existe d’autres publicités dans le même `AdBreak`, répétez les étapes 3 à 7.
1. Lorsque la coupure publicitaire est terminée, utilisez l’événement `AdBreakComplete` pour en effectuer le suivi :

   ```
   - (void)onAdBreakComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

Consultez le scénario de suivi [Lecture VOD avec publicités preroll](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) pour en savoir plus.
