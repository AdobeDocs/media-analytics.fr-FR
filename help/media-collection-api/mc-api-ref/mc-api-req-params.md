---
seo-title: Paramètres de requête
title: Paramètres de requête
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
translation-type: tm+mt
source-git-commit: 9b6e61e8d97ca44772f5dc2e31472a4f6c54e29c

---


# Paramètres de requête{#request-parameters}

## Données d’analyse

| Request Key  | Obligatoire | Définir sur... |  Description  |
| --- | :---: | :---: | --- |
| `analytics.trackingServer` | O | `sessionStart` | URL de votre serveur Adobe Analytics |
| `analytics.reportSuite` | O | `sessionStart` | ID identifiant vos données de rapport d’analyse |
| `analytics.enableSSL` | N | `sessionStart` | True ou false pour activer SSL |
| `analytics.visitorId` | N | `sessionStart` | The Adobe Visitor ID is a custom ID you can use across multiple Adobe applications. La pulsation `visitorId` est égale à Analytics `VID.` |

## Données du visiteur

| Request Key  | Obligatoire | Définir sur... |  Description  |
| --- | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | O | `sessionStart` | Identifiant d’entreprise Experience Cloud ; identifie votre organisation dans l’écosystème Adobe Experience Cloud |
| `visitor.marketingCloudUserId` | N | `sessionStart` | This is the Experience Cloud User ID (ECID). In most scenarios this is the ID you should use to identify a user. The Heartbeat `marketingCloudUserId` equals the `MID` in Adobe Analytics. While not technically required, this parameter is necessary for accessing the Experience Cloud family of apps. |
| `visitor.aamLocationHint` | N | `sessionStart` | Fournit les données edge Adobe Audience Manager |
| `appInstallationId` | N | `sessionStart` | L’ID appInstallationId identifie de manière unique l’application et l’appareil |

## Données du contenu

| Clé de requête | Obligatoire | Définir sur... |  Description  |
| --- | :---: | :---: | --- |
| `media.id` | O | `sessionStart` | Identifiant unique du contenu |
| `media.name` | N | `sessionStart` | Nom du contenu lisible par l’homme |
| `media.length` | O | `sessionStart` | Durée du contenu (secondes) |
| `media.contentType` | O | `sessionStart` | Format de la diffusion (peut correspondre à n’importe quelle chaîne ; quelques valeurs recommandées sont "live", "VOD" ou "Linear") |
| `media.playerName` | O | `sessionStart` | Nom du lecteur responsable du rendu du contenu |
| `media.channel` | O | `sessionStart` | Canal de distribution du contenu. Il peut s’agir d’un nom d’application mobile ou d’un nom de site Web, un nom de propriété. |
| `media.resume` | N | `sessionStart` | Indicates whether or not a user is resuming a previous session (as opposed to starting a new session) |
| `media.sdkVersion` | N | `sessionStart` | Version SDK utilisée par le lecteur |

## Métadonnées standard du contenu

| Request Key  | Obligatoire | Définir sur... |  Description  |
| --- | :---: | :---: | --- |
| `media.show` | N | `sessionStart` | Nom du programme ou de la série |
| `media.season` | N | `sessionStart` | Numéro de la saison à laquelle le programme ou la série appartient |
| `media.episode` | N | `sessionStart` | Numéro de l’épisode |
| `media.assetId` | N | `sessionStart` | Identifiant unique du contenu de la ressource vidéo, tel que l’identifiant d’épisode de la série télévisée, l’identifiant de la ressource de film ou l’identifiant d’événement en direct. Ces ID sont généralement dérivés des autorités de métadonnées telles que EIDR, TMS/Gracenote ou Rovi. Ces identifiants peuvent également provenir d’autres systèmes propriétaires ou internes. |
| `media.genre` | N | `sessionStart` | Type de contenu tel que défini par le producteur de contenu |
| `media.firstAirDate` | N | `sessionStart` | Date à laquelle le contenu a été diffusé à la télévision pour la première fois |
| `media.firstDigitalDate` | N | `sessionStart` | Date à laquelle le contenu a été diffusé pour la première fois sur une chaîne ou une plate-forme numérique |
| `media.rating` | N | `sessionStart` | Évaluation telle que définie par les directives parentales de la télévision |
| `media.originator` | N | `sessionStart` | Créateur du contenu |
| `media.network` | N | `sessionStart` | Nom du réseau/canal |
| `media.showType` | N | `sessionStart` | Type de contenu, exprimé sous la forme d’un nombre entier compris entre 0 et 3 : <ul> <li>0 - Épisode entier </li> <li>1 - Aperçu </li> <li>2 - Clip </li> <li>3 - Autre </li> </ul> |
| `media.adLoad` | N | `sessionStart` | Type de publicité chargée |
| `media.pass.mvpd` | N | `sessionStart` | MVPD fourni par l’authentification Adobe |
| `media.pass.auth` | N | `sessionStart` | Indique que l’utilisateur a été autorisé par l’authentification Adobe (peut uniquement avoir la valeur true si défini) |
| `media.dayPart` | N | `sessionStart` | Heure de la journée à laquelle le contenu a été diffusé |
| `media.feed` | N | `sessionStart` | Type de flux, tel que "West-HD" |

## Données de publicité

| Request Key  | Obligatoire | Définir sur... |  Description  |
| --- | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | `adBreakStart` | Nom convivial de la coupure publicitaire |
| `media.ad.podIndex` | O | `adBreakStart` | Index de la capsule publicitaire dans la vidéo |
| `media.ad.podSecond` | O | `adBreakStart` | Seconde à laquelle la capsule a commencé |
| `media.ad.podPosition` | O | `adStart` | Index de la publicité dans la coupure publicitaire commençant à 1 |
| `media.ad.name` | N | `adStart` | Nom convivial de la publicité |
| `media.ad.id` | O | `adStart` | Nom de la publicité |
| `media.ad.length` | O | `adStart` | Durée de la publicité vidéo en secondes |
| `media.ad.playerName` | O | `adStart` | Nom du lecteur responsable du rendu de la publicité |

## Métadonnées standard de la publicité

| Request Key  | Obligatoire | Définir sur... |  Description  |
| --- | :---: | :---: | --- |
| `media.ad.advertiser` | N | `adStart` | Entreprise ou marque dont le produit apparaît dans la publicité |
| `media.ad.campaignId` | N | `adStart` | ID de la campagne publicitaire |
| `media.ad.creativeId` | N | `adStart` | ID de l’élément créatif publicitaire |
| `media.ad.siteId` | N | `adStart` | ID du site publicitaire |
| `media.ad.creativeURL` | N | `adStart` | URL de l’élément créatif publicitaire |
| `media.ad.placementId` | N | `adStart` | Identifiant de référencement de la publicité |

## Données du chapitre

| Clé de requête | Obligatoire | Définir sur... |  Description  |
| --- | :---: | :---: | --- |
| `media.chapter.index` | O | `chapterStart` | Identifie la position du chapitre dans le contenu |
| `media.chapter.offset` | O | `chapterStart` | Seconde dans la lecture à laquelle le chapitre commence |
| `media.chapter.length` | O | `chapterStart` | Durée du chapitre en secondes |
| `media.chapter.friendlyName` | N | `chapterStart` | Nom convivial du chapitre |

## Données de qualité

| Clé de requête | Obligatoire | Définir sur... |  Description  |
| --- | :---: | :---: | --- |
| `media.qoe.bitrate` | N | Quelconque | Débit binaire de la diffusion |
| `media.qoe.droppedFrames` | N | Quelconque | Nombre d’images perdues dans la diffusion |
| `media.qoe.framesPerSecond` | N | Quelconque | Nombre d’images par seconde |
| `media.qoe.timeToStart` | N | Quelconque | Durée (en millisecondes) écoulée entre le moment où l’utilisateur appuie sur Lecture et le moment où le contenu se charge et commence à être lu |

## Détails supplémentaires {#section_ryt_ccy_lcb}

### visitor.marketingCloudUserId

Pass the Experience Cloud User ID (also known as the `MID` or `MCID`) on the `sessionStart` call by including it inside the `params` map using the following key: **visitor.marketingCloudUserId**. Cette fonctionnalité est utile si vous intégrez déjà d’autres produits Experience Cloud et avez déjà obtenu le MCID.

>[!NOTE]
>
>Media Analytics (MA) est intégré à la famille d’applications Experience Cloud (Adobe Analytics, Audience Manager, Target, etc.). Vous avez besoin d’un Experience Cloud ID pour accéder à ces applications. _The ECID is what you should use to identify users in most scenarios._

### appInstallationId

* **Si vous *ne transmettez pas*de`appInstallationId`valeur -** le serveur principal MA ne génère plus de MCID, mais compte sur Adobe Analytics pour ce faire. La recommandation d’Adobe est d’envoyer un MCID s’il est disponible, ou une valeur `appInstallationId` (ainsi que la valeur `marketingCloudOrgId` encore obligatoire) pour que l’API Media Collection génère le MCID et l’envoie sur tous les appels.

* **Si vous *transmettez*`appInstallationId`la valeur -** Le MCID *peut être* généré par le serveur principal MA, si vous transmettez des valeurs pour `appInstallationId` et les paramètres (requis) . `marketingCloudOrgId` Si vous transmettez la valeur `appInstallationId` vous-même, vous devez conserver sa valeur côté client. Elle doit être propre à l’application sur un appareil et doit être permanente tant que l’application n’est pas réinstallée.

>[!NOTE]
>
>The `appInstallationId` uniquely identifies the app *and the device*. Elle doit être unique pour chaque application sur chaque appareil : deux utilisateurs utilisant la même version d’une même application sur différents appareils doivent chacun envoyer une valeur `appInstallationId` différente (unique).

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The . 
\<ul id="ul_iwc_fqt_pbb"\> 
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li> 
</ul> -->

### visitor.marketingCloudOrgId

In addition to being necessary for MCID generation when that is not provided, this parameter is also used as the value for the publisher ID (based on which Media Analytics performs [federation rule matching.](/help/data-sharing/federated-analytics.md))

### Identifiant utilisateur hérité (aid) d’Analytics et ID utilisateur déclaré (ID client)

* **analytics.aid:**

   La valeur de cette clé doit être une chaîne représentant l’ID utilisateur hérité d’Analytics.
* **visitor.customerIDs:**

   La valeur de cette clé doit être un objet au format suivant :

   ```js
   "<<insert your ID name here>>": {  
     "id": " <<insert your id here>>",  
      "authState": <<insert one of 0, 1, 2>> 
   }
   ```

Notez que la valeur `visitor.customerIDs` peut avoir un nombre quelconque d’objets au format présenté.

### visitor.aamLocationHint

Ce paramètre indique le bord Adobe Audience Manager (AAM) qui sera atteint lorsque Adobe Analytics enverra les données client à Audience Manager. Si vous ne transmettez pas ce paramètre, Adobe le code en dur sur 1. Ceci est particulièrement important lorsque les utilisateurs finaux tendent à utiliser leurs appareils à des emplacements géographiquement distants (par exemple, l’Est ou l’Ouest des États-Unis, l’Europe, l’Asie). Dans le cas contraire, les données utilisateur seront diffusées sur plusieurs edges AAM.

### media.resume

Si l’application détermine qu’une session a été fermée et reprise ultérieurement (par exemple, l’utilisateur a quitté la vidéo puis est revenu et le lecteur a repris la vidéo au curseur de lecture où il s’était arrêté), vous pouvez envoyer un paramètre **media.resume** booléen facultatif dans l’intervalle de paramètres de l’appel `sessionStart`.

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
