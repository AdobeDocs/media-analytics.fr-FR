---
title: Découvrez comment effectuer le suivi des publicités sur iOS
description: Mettez en œuvre le suivi des publicités dans les applications iOS à l’aide du SDK Media.
uuid: e979e679-cde5-4c30-8f34-867feceac13a
exl-id: a352bca9-bcfc-4418-b2a2-c9b1ad226359
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/4z8fq-mojLd4zzlCJsZQ7R7AOc5W59x0u-yOTpylojc
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 367
ht-degree: 91%

---

# Effectuer le suivi des publicités sur iOS{#track-ads-on-ios}

Les instructions suivantes fournissent des conseils pour la mise en œuvre à l’aide des kits SDK 2.x.

>[!IMPORTANT]
>
>Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/getting-started/download-sdks.md)

## Constantes de suivi des publicités

| Nom de constante | Description   |
|---|---|
| `ADBMediaHeartbeatEventAdBreakStart` | Constante permettant d’effectuer le suivi de l’événement AdBreak Start |
| `ADBMediaHeartbeatEventAdBreakComplete` | Constante permettant d’effectuer le suivi de l’événement AdBreak Complete |
| `ADBMediaHeartbeatEventAdStart` | Constante permettant d’effectuer le suivi de l’événement Début de la publicité |
| `ADBMediaHeartbeatEventAdComplete` | Constante permettant d’effectuer le suivi de l’événement Fin de la publicité |
| `ADBMediaHeartbeatEventAdSkip` | Constante permettant d’effectuer le suivi de l’événement Saut de publicité |

## Procédure de mise en œuvre

1. Identifiez le moment où la limite de coupure publicitaire commence, y compris preroll, et créez un `AdBreakObject` à l’aide des informations de coupure publicitaire.

   Référence `AdBreakObject` :

   | Nom de variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom de la coupure publicitaire tel que pre-roll, mid-roll et post-roll. | Oui |
   | `position` | Position du nombre de la coupure publicitaire dans le contenu, en commençant par 1. | Oui |
   | `startTime` | Valeur du curseur de lecture au début de la coupure publicitaire. | Oui |

   Création d’objet de coupure publicitaire :

   ```
   id adBreakObject = [ADBMediaHeartbeat createAdBreakObjectWithName:[ADBREAK_NAME]
                               position:[POSITION]  
                               startTime:[START_TIME]];
   ```

1. Appelez `trackEvent()` avec `AdBreakStart` dans l’instance `MediaHeartbeat` pour commencer le suivi de la coupure publicitaire :

   ```
   - (void)onAdBreakStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                        mediaObject:adBreakObject  
                        data:nil];
   }
   ```

1. Déterminez le moment où la publicité commence, puis créez une instance `AdObject` à l’aide des informations sur la publicité.

   Référence `AdObject` :

   | Nom de variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom convivial de la publicité. | Oui |
   | `adId` | Identifiant unique de la publicité. | Oui |
   | `position` | Position du nombre de l’annonce publicitaire dans la coupure publicitaire, en commençant par 1. | Oui |
   | `length` | Longueur de la publicité | Oui |

   Création d’objet publicitaire :

   ```
   id adObject = [ADBMediaHeartbeat createAdObjectWithName:[AD_NAME]
                                    adId:[AD_ID]
                                    position:[POSITION]
                                    length:[LENGTH]];
   ```

1. Vous pouvez joindre des métadonnées standard et/ou de publicité à la session de suivi multimédia par le biais de variables de données contextuelles.

   * [Mise en œuvre de métadonnées de publicité standard sur iOS](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
   * **Métadonnées de publicité personnalisées -** Pour les métadonnées personnalisées, créez un objet de variable pour les variables de données personnalisées et renseignez les données de la publicité actuelle :

     ```
     NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init];
     [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"];
     [adDictionary setObject:@"Sample campaign" forKey:@"campaign"];
     [adDictionary setObject:@"Sample creative" forKey:@"creative"];
     ```

1. Appelez `trackEvent()` avec l’événement `AdStart` dans l’instance `MediaHeartbeat` pour commencer le suivi de la lecture de publicité.

   Incluez une référence à votre variable de métadonnées personnalisées (ou un objet vide) comme troisième paramètre dans l’appel d’événement :

   ```
   - (void)onAdStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                        mediaObject:adObject  
                        data:adDictionary];
   }
   ```

1. Lorsque la lecture de la publicité atteint la fin de la publicité, appelez `trackEvent()` avec l’événement `AdComplete`.

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

Consultez le scénario de suivi [Lecture VOD avec publicités preroll](/help/use-cases/tracking-scenarios/vod-preroll-ads.md) pour en savoir plus.
