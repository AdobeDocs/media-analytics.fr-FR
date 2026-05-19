---
title: Présentation du suivi des publicités
description: Présentation de l’implémentation du suivi des publicités avec le SDK Media.
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PguxKIzAL95WbMl5c0yJq9rYSqZgOGbbAYtxOI4eVOs
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: 641
ht-degree: 60%

---

# Aperçu{#overview}

Les instructions suivantes fournissent des conseils pour la mise en œuvre à l’aide des kits SDK 2.x.

>[!IMPORTANT]
>
>Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger les Guides du développeur 1.x dans la rubrique [Téléchargement des SDK.](/help/getting-started/download-sdks.md)

La lecture de publicité inclut le suivi des coupures publicitaires, des démarrages de publicité, des fins de publicité et des publicités ignorées. Utilisez l’API du lecteur multimédia pour identifier les événements de lecteur clés et spécifier les variables de publicité obligatoires et facultatives.

## Événements du lecteur {#player-events}

### Au démarrage de la coupure publicitaire

>[!NOTE]
>Y compris preroll

* Créez une instance d’objet `adBreak` pour la coupure publicitaire. Par exemple : `adBreakObject`.

* Appelez `trackEvent` pour le démarrage de la coupure publicitaire avec `adBreakObject`.

### À chaque démarrage de ressource de publicité

* Créez une instance d’objet publicitaire pour la ressource de publicité. Par exemple : `adObject`.
* Renseignez les métadonnées de publicité, `adCustomMetadata`.
* Appelez `trackEvent` pour le démarrage de publicité.

### À chaque fin de publicité

* Appelez `trackEvent` pour la fin de publicité.

### Lorsqu’une publicité est ignorée

* Appelez `trackEvent` pour le saut de publicité.

### À la fin de la coupure publicitaire

* Appelez `trackEvent` pour la fin de la coupure publicitaire.

## Mise en œuvre du suivi des publicités {#implement-ad-tracking}

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

   Référence `AdBreakObject` :

   | Nom de variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom de la coupure publicitaire tel que pre-roll, mid-roll et post-roll. | Oui |
   | `position` | Position du nombre de la coupure publicitaire dans le contenu, en commençant par 1. | Oui |
   | `startTime` | Valeur du curseur de lecture au début de la coupure publicitaire. | Oui |

1. Appelez `trackEvent()` avec `AdBreakStart` dans l’instance `MediaHeartbeat` pour commencer le suivi de coupure publicitaire.

1. Déterminez le moment où la publicité commence, puis créez une instance `AdObject` à l’aide des informations sur la publicité.

   Référence `AdObject` :

   | Nom de variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom convivial de la publicité. | Oui |
   | `adId` | Identifiant unique de la publicité. | Oui |
   | `position` | Position du nombre de l’annonce publicitaire dans la coupure publicitaire, en commençant par 1. | Oui |
   | `length` | Longueur de la publicité | Oui |

1. Vous pouvez éventuellement joindre des métadonnées standard et/ou publicitaires à la session de suivi via des variables de données contextuelles.

   * **Métadonnées de publicité standard -** Pour les métadonnées de publicité standard, créez un dictionnaire de paires de valeurs de clé de métadonnées de publicité standard à l’aide des clés de votre plateforme.
   * **Métadonnées de publicité personnalisées -** pour les métadonnées personnalisées, créez un objet de variable pour les variables de données personnalisées et renseignez les données de la publicité actuelle.

1. Appelez `trackEvent()` avec l’événement `AdStart` dans l’instance `MediaHeartbeat` pour commencer le suivi de la lecture de publicité.

   Incluez une référence à votre variable de métadonnées personnalisées (ou un objet vide) comme troisième paramètre dans l’appel d’événement. Pendant la lecture de la publicité, gardez le curseur de lecture du contenu (`l:event:playhead`) fixe à l’emplacement où la coupure publicitaire a commencé ; sa progression pendant la lecture de la publicité est exagérée [Temps passé sur le contenu](/help/reporting/metrics/content-time-spent.md).

1. Lorsque la lecture de la publicité atteint la fin de la publicité, appelez `trackEvent()` avec l’événement `AdComplete`.

1. Si la lecture de la publicité ne s’est pas terminée car l’utilisateur a choisi d’ignorer la publicité, effectuez le suivi de l’événement `AdSkip`.
1. S’il existe d’autres publicités dans le même `AdBreak`, répétez les étapes 3 à 7.
1. Lorsque la coupure publicitaire est terminée, utilisez l’événement `AdBreakComplete` pour en effectuer le suivi.

>[!IMPORTANT]
>
>**Annonces preroll : ne pas appeler `trackPlay` avant `AdBreakStart` et `AdStart`.** Le premier ping de `play` sur les incréments de contenu principaux [Le contenu démarre](/help/reporting/metrics/content-starts.md). Si `trackPlay` est appelé avant le déclenchement des événements de publicité preroll et que la visionneuse abandonne pendant la publicité, les démarrages de contenu sont incrémentés même si aucun contenu principal n’a jamais été lu. Pour les scénarios de preroll, retardez le `trackPlay` jusqu’à ce que les `AdBreakStart` et `AdStart` aient été envoyés.

>[!NOTE]
>
>La valeur du curseur de lecture signalée pendant la lecture de la publicité représente la position de la visionneuse dans le **contenu principal**, et non dans la publicité. Pour une publicité preroll précédant une vidéo de 10 minutes, le curseur de lecture est `0` tout au long de la publicité. Pour une publicité mid-roll qui démarre à 5 minutes, le curseur de lecture reste à `300` (secondes) pendant la durée de la publicité.

L’exemple de code suivant utilise le kit SDK JavaScript 2.x pour un lecteur multimédia HTML5.

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

>[!MORELIKETHIS]
>
>* [Début de la coupure publicitaire](/help/implementation/events/ads/ad-break-start.md)
>* [Début de la publicité](/help/implementation/events/ads/ad-start.md)
>* [Publicité terminée](/help/implementation/events/ads/ad-complete.md)
>* [Saut d’annonce publicitaire](/help/implementation/events/ads/ad-skip.md)
>* [Coupure publicitaire terminée](/help/implementation/events/ads/ad-break-complete.md)
