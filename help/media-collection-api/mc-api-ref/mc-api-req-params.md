---
title: Paramètres de requête
description: null
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
translation-type: tm+mt
source-git-commit: b1b94b4cde74908ea528fb69d78250dc1da1db80
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 99%

---


# Paramètres de requête {#request-parameters}

## Données d’analyse

| Clé de requête  | Obligatoire | Définir sur... |  Description  |
| --- | :---: | :---: | --- |
| `analytics.trackingServer` | Y | `sessionStart` | URL de votre serveur Adobe Analytics |
| `analytics.reportSuite` | Y | `sessionStart` | ID identifiant vos données de rapport d’analyse |
| `analytics.enableSSL` | N | `sessionStart` | True ou false pour activer SSL |
| `analytics.visitorId` | N | `sessionStart` | L’identifiant visiteur Adobe est un ID personnalisé que vous pouvez utiliser dans plusieurs applications Adobe. La pulsation `visitorId` est égale au `VID.` Analytics |

## Données du visiteur

| Clé de requête  | Obligatoire | Définir sur... |  Description  |
| --- | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | Y | `sessionStart` | Identifiant d’entreprise Experience Cloud ; identifie votre organisation dans l’écosystème Adobe Experience Cloud |
| `visitor.marketingCloudUserId` | N | `sessionStart` | Il s’agit de l’identifiant utilisateur Experience Cloud (ECID). Dans la plupart des cas, il s’agit de l’identifiant que vous devez utiliser pour identifier un utilisateur. La pulsation `marketingCloudUserId` est égale au `MID` dans Adobe Analytics. Bien que cela ne soit pas techniquement requis, ce paramètre est nécessaire pour accéder à la famille d’applications Experience Cloud. |
| `visitor.aamLocationHint` | N | `sessionStart` | Fournit les données edge Adobe Audience Manager |
| `appInstallationId` | N | `sessionStart` | L’ID appInstallationId identifie de manière unique l’application et l’appareil |

## Données du contenu

| Clé de requête  | Obligatoire | Définir sur... |  Description  |
| --- | :---: | :---: | --- |
| `media.id` | Y | `sessionStart` | Identifiant unique du contenu |
| `media.name` | N | `sessionStart` | Nom du contenu lisible par l’homme |
| `media.length` | Y | `sessionStart` | Durée du contenu (secondes) |
| `media.contentType` | Y | `sessionStart` | Format de la diffusion (peut correspondre à n’importe quelle chaîne ; quelques valeurs recommandées sont &quot;live&quot;, &quot;VOD&quot; ou &quot;Linear&quot;) |
| `media.playerName` | Y | `sessionStart` | Nom du lecteur responsable du rendu du contenu |
| `media.channel` | Y | `sessionStart` | Chaîne de distribution du contenu. Il peut s’agir du nom d’une application, d’un site web, d’un nom de propriété, etc. |
| `media.resume` | N | `sessionStart` | Indique si un utilisateur reprend ou non une session précédente (au lieu de commencer une nouvelle session). |
| `media.sdkVersion` | N | `sessionStart` | Version SDK utilisée par le lecteur |

## Métadonnées standard du contenu

| Clé de requête  | Obligatoire | Définir sur... |  Description  |
| --- | :---: | :---: | --- |
| `media.streamFormat` | N | `sessionStart` | Format du flux, p. ex. &quot;HD&quot; |
| `media.show` | N | `sessionStart` | Nom du programme ou de la série |
| `media.season` | N | `sessionStart` | Numéro de la saison à laquelle le programme ou la série appartient |
| `media.episode` | N | `sessionStart` | Numéro de l’épisode |
| `media.assetId` | N | `sessionStart` | L’identifiant unique du contenu de la ressource vidéo, tel que l’identifiant d’épisode de la série télévisée, l’identifiant de la ressource de film ou l’identifiant d’événement en direct. En règle générale, ces identifiants sont issus des autorités de métadonnées telles que EIDR, TMS/Gracenote ou Rovi. Ces identifiants peuvent également provenir d’autres systèmes propriétaires ou internes. |
| `media.genre` | N | `sessionStart` | Type de contenu tel que défini par le producteur de contenu |
| `media.firstAirDate` | N | `sessionStart` | Date à laquelle le contenu a été diffusé à la télévision pour la première fois |
| `media.firstDigitalDate` | N | `sessionStart` | Date à laquelle le contenu a été diffusé pour la première fois sur une chaîne ou une plateforme numérique |
| `media.rating` | N | `sessionStart` | Évaluation telle que définie par les directives parentales de la télévision |
| `media.originator` | N | `sessionStart` | Créateur du contenu |
| `media.network` | N | `sessionStart` | Nom du réseau/canal |
| `media.showType` | N | `sessionStart` | Type de contenu, exprimé sous la forme d’un nombre entier compris entre 0 et 3 : <ul> <li>0 - épisode entier </li> <li>1 - aperçu </li> <li>2 - clip </li> <li>3 - autre </li> </ul> |
| `media.adLoad` | N | `sessionStart` | Type de publicité chargée |
| `media.pass.mvpd` | N | `sessionStart` | MVPD fourni par l’authentification Adobe |
| `media.pass.auth` | N | `sessionStart` | Indique que l’utilisateur a été autorisé par l’authentification Adobe (peut uniquement avoir la valeur true si défini) |
| `media.dayPart` | N | `sessionStart` | Heure de la journée à laquelle le contenu a été diffusé |
| `media.feed` | N | `sessionStart` | Type de flux, tel que &quot;West-HD&quot; |

## Données de publicité

| Clé de requête  | Obligatoire | Définir sur... |  Description  |
| --- | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | `adBreakStart` | Nom convivial de la coupure publicitaire |
| `media.ad.podIndex` | Y | `adBreakStart` | Index de la capsule publicitaire dans la vidéo |
| `media.ad.podSecond` | Y | `adBreakStart` | Seconde à laquelle la capsule a commencé |
| `media.ad.podPosition` | Y | `adStart` | Index de la publicité dans la coupure publicitaire commençant à 1 |
| `media.ad.name` | N | `adStart` | Nom convivial de la publicité |
| `media.ad.id` | Y | `adStart` | Nom de la publicité |
| `media.ad.length` | Y | `adStart` | Durée de la publicité vidéo en secondes |
| `media.ad.playerName` | Y | `adStart` | Nom du lecteur responsable du rendu de la publicité |

## Métadonnées standard de la publicité

| Clé de requête  | Obligatoire | Définir sur... |  Description  |
| --- | :---: | :---: | --- |
| `media.ad.advertiser` | N | `adStart` | Entreprise ou marque dont le produit apparaît dans la publicité |
| `media.ad.campaignId` | N | `adStart` | ID de la campagne publicitaire |
| `media.ad.creativeId` | N | `adStart` | ID de l’élément créatif publicitaire |
| `media.ad.siteId` | N | `adStart` | ID du site publicitaire |
| `media.ad.creativeURL` | N | `adStart` | URL de l’élément créatif publicitaire |
| `media.ad.placementId` | N | `adStart` | Identifiant de référencement de la publicité |

## Données du chapitre

| Clé de requête  | Obligatoire | Définir sur... |  Description  |
| --- | :---: | :---: | --- |
| `media.chapter.index` | Y | `chapterStart` | Identifie la position du chapitre dans le contenu |
| `media.chapter.offset` | Y | `chapterStart` | Seconde dans la lecture à laquelle le chapitre commence |
| `media.chapter.length` | Y | `chapterStart` | Durée du chapitre en secondes |
| `media.chapter.friendlyName` | N | `chapterStart` | Nom convivial du chapitre |

## Données de qualité

| Clé de requête  | Obligatoire | Définir sur... |  Description  |
| --- | :---: | :---: | --- |
| `media.qoe.bitrate` | N | N’importe quel(le) | Débit binaire de la diffusion |
| `media.qoe.droppedFrames` | N | N’importe quel(le) | Nombre d’images perdues dans la diffusion |
| `media.qoe.framesPerSecond` | N | N’importe quel(le) | Nombre d’images par seconde |
| `media.qoe.timeToStart` | N | N’importe quel(le) | Durée (en millisecondes) écoulée entre le moment où l’utilisateur lance la lecture et le contenu se charge et commence à être lu |

## Paramètres de la Loi sur la protection du consommateur (CCPA) de Californie {#ccpa-params}

| Clé de requête  | Obligatoire | Définir sur... |  Description  |
| --- | :---: | :---: | --- |
| `analytics.optOutServerSideForwarding` | N | `sessionStart` | Définissez cette variable sur « true » lorsque l’utilisateur final a choisi de ne pas partager ses données entre Adobe Analytics et d’autres solutions Experience Cloud (par exemple, Audience Manager). |
| `analytics.optOutShare` | N | `sessionStart` | Définissez cette variable sur « true » lorsque l’utilisateur final a choisi de ne pas utiliser ses données pour la fédération (par exemple, pour d’autres clients Adobe Analytics). |

## Détails supplémentaires {#additional-details}

### visitor.marketingCloudUserId

Transmettez l’identifiant utilisateur Experience Cloud (également appelé `MID` ou `MCID`) sur l’appel `sessionStart` en l’incluant dans la carte `params` à l’aide de la clé suivante : **visitor.marketingCloudUserId**. Cette fonctionnalité est utile si vous intégrez déjà d’autres produits Experience Cloud et avez déjà obtenu le MCID.

>[!NOTE]
>
>Media Analytics (MA) est intégré à la gamme d’applications Experience Cloud (Adobe Analytics, Audience Manager, Target, etc.). Vous avez besoin d’un Experience Cloud ID pour accéder à ces applications. _L’ECID est ce que vous devez utiliser pour identifier les utilisateurs dans la plupart des scénarios._

### appInstallationId

* **Si vous ne transmettez *pas* de valeur `appInstallationId` :** Le serveur principal MA ne générera plus de MCID, mais à la place s’en remettra à Adobe Analytics pour cela. La recommandation d’Adobe est d’envoyer un MCID s’il est disponible, ou une valeur `appInstallationId` (ainsi que la valeur `marketingCloudOrgId` encore obligatoire) pour que l’API Media Collection génère le MCID et l’envoie sur tous les appels.

* **Si vous ne transmettez *pas* de valeur `appInstallationId` :** Le MCID *peut être* généré par le serveur principal MA, si vous transmettez des valeurs pour les paramètres `appInstallationId` et `marketingCloudOrgId` (obligatoire). Si vous transmettez la valeur `appInstallationId` vous-même, vous devez conserver sa valeur côté client. Elle doit être propre à l’application sur un appareil et doit être permanente tant que l’application n’est pas réinstallée.

>[!NOTE]
>
>Le `appInstallationId` identifie de manière unique l’application *et l’appareil*. Elle doit être unique pour chaque application sur chaque appareil : deux utilisateurs utilisant la même version d’une même application sur différents appareils doivent chacun envoyer une valeur `appInstallationId` différente (unique).

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The .
\<ul id="ul_iwc_fqt_pbb"\>
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li>
</ul> -->

### visitor.marketingCloudOrgId

En plus d’être nécessaire à la génération du MCID lorsqu’il n’est pas fourni, ce paramètre est également utilisé comme valeur de l’identifiant d’éditeur (en fonction de l’instance multimédia Analytics qui procède à l’[association des règles de fédération](/help/federated-analytics.md)).

### Identifiant utilisateur Analytics existant (aid) et identifiants utilisateur déclarés (customerIDs)

* **analytics.aid :**

   La valeur de cette clé doit être une chaîne représentant l’identifiant utilisateur Analytics existant
* **visitor.customerIDs :**

   La valeur de cette clé doit être un objet au format suivant :

   ```js
   "<<insert your ID name here>>": {  
     "id": " <<insert your id here>>",  
      "authState": <<insert one of 0, 1, 2>>
   }
   ```

Notez que la valeur `visitor.customerIDs` peut avoir un nombre quelconque d’objets au format présenté.

### visitor.aamLocationHint

Ce paramètre indique quel edge Adobe Audience Manager (AAM) serait affecté lorsqu’Adobe Analytics envoie les données client à Audience Manager. Si vous ne transmettez pas ce paramètre, Adobe le code en dur sur 1. Cela est particulièrement important lorsque les utilisateurs finaux tendent à utiliser leurs appareils à des emplacements géographiquement distants (par exemple, l’Est ou l’Ouest des États-Unis, l’Europe, l’Asie). Dans le cas contraire, les données utilisateur seront diffusées sur plusieurs edges AAM.

### media.resume

Si l’application détermine qu’une session a été fermée et reprise ultérieurement (par exemple, l’utilisateur a quitté la vidéo puis est revenu et le lecteur a repris la vidéo au curseur de lecture où il s’était arrêté), vous pouvez envoyer un paramètre **media.resume** booléen facultatif dans l’intervalle de paramètres de l’appel `sessionStart`.

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
