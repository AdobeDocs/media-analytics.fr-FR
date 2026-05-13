---
title: Découvrez comment effectuer le suivi des publicités à lʼaide de JavaScript 3.x
description: Mettez en œuvre le suivi des publicités dans les applications de navigateur (JS) à l’aide du SDK Media.
exl-id: 6b34b2c0-5e50-471a-b52c-b9c760fa3169
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/j8xAr1QwslwoGu5IKvW14wFjyCSMMIIerA1t-JECNcQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 406
ht-degree: 88%

---

# Effectuer le suivi des publicités à l’aide de JavaScript 3.x{#track-ads-on-javascript}

Les instructions suivantes fournissent des conseils pour la mise en œuvre à l’aide des kits SDK 3.x.

>[!IMPORTANT]
>
>Si vous mettez en œuvre une version précédente du kit SDK, vous pouvez télécharger les Guides du développeur dans la rubrique [Téléchargement des SDK.](/help/getting-started/download-sdks.md)

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
   | `name` | string | Chaîne non vide désignant le nom de la coupure publicitaire (pre-roll, mid-roll et post-roll). |
   | `position` | number | Position du nombre au début de la coupure publicitaire commençant par 1. |
   | `startTime` | number | Valeur du curseur de lecture au début de la coupure publicitaire. |

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
   | `name` | string | Chaîne non vide désignant le nom de l’annonce publicitaire. |
   | `adId` | string | Chaîne non vide désignant l’identifiant de l’annonce publicitaire. |
   | `position` | number | Position du numéro de l’annonce publicitaire dans la coupure publicitaire, en commençant par 1. |
   | `length` | number | Numéro positif désignant la longueur de l’annonce publicitaire. |

   Création d’objet publicitaire :

   ```js
   var adObject =
     ADB.Media.createAdObject.createAdObject(<AD_NAME>,
                                   <AD_ID>,
                                   <POSITION>,
                                   <LENGTH>);
   ```

1. (Facultatif) Joignez des métadonnées standard et/ou publicitaires à la session de suivi multimédia par le biais de variables de données contextuelles.

   * [Mise en œuvre de métadonnées de publicité standard sur JavaScript](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
   * **Métadonnées de publicité personnalisées -** Pour les métadonnées personnalisées, créez un objet de variable pour les variables de données personnalisées et renseignez les données de la publicité actuelle :

     ```js
     /* Set context data */
     // Standard metadata keys provided by adobe.
     adMetadata[ADB.Media.AdMetadataKeys]  ="Sample Advertiser";
     adMetadata[ADB.Media.AdMetadataKeys] = "Sample Campaign";
     
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

Consultez le scénario de suivi [Lecture VOD avec publicités preroll](/help/use-cases/tracking-scenarios/vod-preroll-ads.md) pour en savoir plus.

## Suivi granulaire des publicités

L’intervalle de ping des annonces par défaut est `10 seconds`.

Vous pouvez configurer le suivi granulaire des publicités pour activer le suivi des publicités `1 second`.

>[!IMPORTANT]
>
>Ces informations doivent être fournies lors du démarrage d&#39;une session de tracking.



**Syntaxe**

```javascript
ADB.Media.MediaObjectKey = {
   GranularAdTracking: "media.granularadtracking"
   }
```

**Exemple**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

// Enable granular ad tracking
mediaObject[ADB.Media.MediaObjectKey.GranularAdTracking] = true;

tracker.trackSessionStart(mediaObject);
```
