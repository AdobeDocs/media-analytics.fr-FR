---
title: Suivi des publicités à l’aide de JavaScript 3.x
description: Mettez en œuvre le suivi des publicités dans les applications de navigateur (JS) à l’aide du SDK Media.
translation-type: tm+mt
source-git-commit: f5b3961e0525c26b682490a4376d244c2703ae24
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 80%

---


# Suivi des publicités à l’aide de JavaScript 3.x{#track-ads-on-javascript}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre à l’aide des kits SDK 3.x. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

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

   Référence `AdBreakObject` :

   | Nom de variable | Type | Description |
   | --- | --- | --- |
   | `name` | string | Chaîne non vide indiquant le nom de l’abréviation (preroll, mid-roll et post-roll). |
   | `position` | nombre | Position du nombre au début de la coupure publicitaire commençant par 1. |
   | `startTime` | nombre | Valeur du curseur de lecture au début de la coupure publicitaire. |

   Création d’objet de coupure publicitaire :

   ```js
   var adBreakObject =
     ADB.Media.createAdBreakObject(<ADBREAK_NAME>,
                                      <POSITION>,
                                      <START_TIME>);
   ```

1. Appelez `trackEvent()` avec `AdBreakStart` dans l’instance `MediaHeartbeat` pour commencer le suivi de la coupure publicitaire :

   ```js
   tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);
   ```

1. Déterminez le moment où la publicité commence, puis créez une instance `AdObject` à l’aide des informations sur la publicité.

   Référence `AdObject` :

   | Nom de variable | Type | Description |
   | --- | --- | --- |
   | `name` | string | Chaîne non vide indiquant le nom de la publicité. |
   | `adId` | string | Chaîne non vide indiquant l&#39;identifiant de publicité. |
   | `position` | nombre | Position du numéro de la publicité dans l&#39;adbreak, commençant par 1. |
   | `length` | nombre | Numéro positif indiquant la longueur de la publicité. |

   Création d’objet publicitaire :

   ```js
   var adObject =
     ADB.Media.createAdObject.createAdObject(<AD_NAME>,
                                   <AD_ID>,
                                   <POSITION>,
                                   <LENGTH>);
   ```

1. Vous pouvez joindre des métadonnées standard et/ou de publicité à la session de suivi multimédia par le biais de variables de données contextuelles.

   * [Mise en œuvre de métadonnées de publicité standard sur JavaScript](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-js.md)
   * **Métadonnées de publicité personnalisées -** Pour les métadonnées personnalisées, créez un objet de variable pour les variables de données personnalisées et renseignez les données de la publicité actuelle :

      ```js
      /* Set context data */
      // Standard metadata keys provided by adobe.
      adMetadata[ADB.Media.AdMetadataKeys.ADVERTISER]  ="Sample Advertiser";
      adMetadata[ADB.Media.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
      
      // Custom metadata keys
      adMetadata["affiliate"] = "Sample affiliate";
      adMetadata["campaign"] = "Sample ad campaign";
      adMetadata["creative"] = "Sample creative";
      ```

1. Appelez `trackEvent()` avec l’événement `AdStart` dans l’instance `MediaHeartbeat` pour commencer le suivi de la lecture de publicité.

   Incluez une référence à votre variable de métadonnées personnalisées (ou un objet vide) comme troisième paramètre dans l’appel d’événement :

   ```js
   _onAdStart = function() {
       tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
   };
   ```

1. Lorsque la lecture de la publicité atteint la fin de la publicité, appelez `trackEvent()` avec l’événement `AdComplete` :

   ```js
   _onAdComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdComplete);
   };
   ```

1. Si la lecture de la publicité ne s’est pas terminée car l’utilisateur a choisi d’ignorer la publicité, suivez l’événement `AdSkip` :

   ```js
   _onAdSkip = function() {
       tracker.trackEvent(ADB.Media.Event.AdSkip);
   };
   ```

1. S’il existe d’autres publicités dans le même `AdBreak`, répétez les étapes 3 à 7.
1. Lorsque la coupure publicitaire est terminée, utilisez l’événement `AdBreakComplete` pour en effectuer le suivi :

   ```js
   _onAdBreakComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
   };
   ```

Consultez le scénario de suivi [Lecture VOD avec publicités preroll](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) pour en savoir plus.
