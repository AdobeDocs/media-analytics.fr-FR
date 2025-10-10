---
title: Découvrez comment effectuer le suivi des publicités sur Roku
description: Mettez en œuvre le suivi des publicités dans les applications Roku à l’aide du SDK Media.
uuid: b1567265-7043-4efa-a313-aaaa91c4bb01
exl-id: aaed828d-1aba-486e-83e3-2ffd092305e2
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Effectuer le suivi des publicités sur Roku{#track-ads-on-roku}

Les instructions suivantes fournissent des conseils pour la mise en œuvre à l’aide des kits SDK 2.x.

>[!IMPORTANT]
>
>Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/getting-started/download-sdks.md)

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

   | Nom de variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom de la coupure publicitaire tel que pre-roll, mid-roll et post-roll. | Oui |
   | `position` | Position du nombre au début de la coupure publicitaire commençant par 1. | Oui |
   | `startTime` | Valeur du curseur de lecture au début de la coupure publicitaire. | Oui |

   ```
   ‘ Create an adbreak info object
   adBreakInfo = adb_media_init_adbreakinfo()
   adBreakInfo.name = <ADBREAK_NAME>
   adBreakInfo.startTime = <START_TIME>
   adBreakInfo.position = <POSITION>
   ```

1. Appelez `trackEvent()` avec `AdBreakStart` dans l’instance `MediaHeartbeat` pour commencer le suivi de la coupure publicitaire :

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_START, adBreakInfo, contextData)
   ```

1. Déterminez le moment où la ressource de publicité commence, puis créez une instance `AdObject` à l’aide des informations sur la publicité.

   ```
   adInfo =  
     adb_media_init_adinfo(ad.title,  
                           ad.id,  
                           ad.position,  
                           ad.duration)
   ```

1. Vous pouvez joindre des métadonnées standard et/ou de publicité à la session de suivi multimédia par le biais de variables de données contextuelles.

   * [Mise en œuvre de métadonnées de publicité standard sur Roku ](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   * **Métadonnées de publicité personnalisées -** Pour les métadonnées personnalisées, créez un objet de variable pour les variables de données personnalisées et renseignez les données de la ressource de publicité actuelle :

     ```
     contextData = {}
     contextData["adinfo1"] = "adinfo2"
     contextData["adinfo2"] = "adinfo2"
     ```

1. Appelez `trackEvent()` avec l’événement `AdStart` dans l’instance `MediaHeartbeat` pour commencer le suivi de la lecture de publicité :

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_START, adInfo, contextData)
   ```

1. Lorsque la lecture de la ressource de publicité atteint la fin de la publicité, appelez `trackEvent()` avec l’événement `AdComplete`.

   ```
   standardAdMetadata = {}
   contextData = {}
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_COMPLETE, adInfo, contextData)
   ```

1. Si la lecture de la publicité ne s’est pas terminée car l’utilisateur a choisi d’ignorer la publicité, suivez l’événement `AdSkip` :

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_SKIP, adInfo, contextData
   ```

1. S’il existe d’autres publicités dans le même `AdBreak`, répétez les étapes 3 à 7.
1. Lorsque la coupure publicitaire est terminée, utilisez l’événement `AdBreakComplete` pour en effectuer le suivi :

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_COMPLETE, adBreakInfo, contextData)
   ```

Consultez le scénario de suivi [Lecture VOD avec publicités preroll](/help/use-cases/tracking-scenarios/vod-preroll-ads.md) pour en savoir plus.
