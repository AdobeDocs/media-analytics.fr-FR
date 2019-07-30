---
seo-title: Paramètres audio et vidéo
title: Paramètres audio et vidéo
uuid: fdacfb 8 b-db 3 e -46 fb-b 9 ad-c 3 a 749555 b 2 a
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Paramètres audio et vidéo{#audio-and-video-parameters}

>[!IMPORTANT]
>
>Le 7 février 2019, Adobe Analytics pour la vidéo et l'audio a publié un changement de nom de mesure. La mesure <i>Démarrages de média</i> sera désormais appelée <i>Lancements de média</i>. Ce changement vise à refléter les normes du secteur dans les mesures et les rapports et à rendre la mesure facile à identifier dans les rapports.

>[!NOTE]
>
>À compter du 13 septembre 2018, une modification a été apportée aux libellés pour certaines dimensions, mesures et rapports, afin de permettre le suivi inter-contenu des analyses vidéo et audio. Les étiquettes qui ont été modifiées comprennent les suivantes : *démarrages de vidéo* en *démarrages de média*, *durée de la vidéo* en *durée du contenu* et *nom de la vidéo* en *nom du contenu*. Dans Reports and Analytics, les rapports vidéo ont tous été mis à jour de sorte à employer le terme « média » plutôt que « vidéo ». Ces changements apportés aux étiquettes n’ont eu aucune incidence sur la collecte de données ou les données historiques. Veuillez prendre note de ces modifications au cas où vous seriez amené à les utiliser dans le Report Builder ou dans toute autre extraction automatisée de données provenant de sources externes qui pourrait être affectée par celles-ci.

Cette rubrique présente une liste des données de contenu audio et vidéo, y compris les valeurs de données contextuelles, qu’Adobe collecte via les variables de solution.

Description des données de tableau :

* **Mise en œuvre :** Informations sur les valeurs et les exigences de mise en œuvre
   * *Clé* : Variable, définie manuellement dans votre application ou automatiquement par le kit Adobe Media SDK.
   * *Obligatoire* : Indique si le paramètre est requis pour le suivi audio et vidéo de base.
   * *Type* : Spécifie le type de variable à définir, chaîne ou nombre.
   * *Envoyé avec* - Indique quand les données sont envoyées : *Media Start* est l'appel Analytics envoyé au démarrage du média, Démarrage *de publicité* est l'appel Analytics envoyé au démarrage de la publicité, etc. *Les* appels Close sont les appels Analytics compilés envoyés directement depuis le serveur de pulsation vers le serveur d'analyse à la fin de la session multimédia, ou la fin de la publicité, du chapitre, etc. Les appels de fermeture ne sont pas disponibles dans les appels de paquets réseau.
   * *Min. Version SDK* : Indique la version SDK dont vous auriez besoin pour accéder au paramètre.
   * *Exemple de valeur* : Fournit un exemple d’utilisation de variable courante.
* **Paramètres réseau :** Affiche les valeurs transmises aux serveurs Adobe Analytics ou Heartbeat. Cette colonne affiche les noms des paramètres visibles dans les appels réseau générés par les kits Adobe Media SDK.
* **Création de rapports :** Informations sur la façon d’afficher et d’analyser les données audio et vidéo.
   * *Disponible* : Indique si les données sont disponibles dans les rapports par défaut (*Oui*) ou nécessitent une configuration personnalisée (*Personnalisé*).
   * *Variable réservée* : Indique si les données sont capturées en tant qu’événement, valeur eVar, valeur prop ou classification dans une variable réservée.
   * *Expiration* : Indique si les données expirent après chaque accès ou après chaque visite.
   * *Nom du rapport* : Nom du rapport Adobe Analytics pour la variable.
   * *Données contextuelles* : Nom des données contextuelles Adobe Analytics transmises au serveur de rapports et utilisées dans le traitement des règles.
   * *Flux de données* : Nom de colonne pour la variable trouvée dans Clickstream ou les flux de données de diffusion en direct.
   * *Audience Manager* : Nom de caractéristique détecté dans Adobe Audience Manager.

>[!IMPORTANT]
>
>Ne modifiez pas les noms de classification pour les variables répertoriées ci-dessous, décrites sous la section Création de rapports/variable réservée sous la forme de « classification ».\
>Les classifications des médias sont définies lorsqu'une suite de rapports est activée pour le suivi multimédia. De temps à autres, Adobe ajoute de nouvelles propriétés et, dès lors, les clients doivent réactiver leurs suites de rapports pour accéder aux nouvelles propriétés du média. Lors du processus de mise à jour, Adobe détermine si les classifications sont activées en vérifiant les noms des variables. Si l'un d'eux est manquant, Adobe rajoute les autres.

## Données audio et vidéo principales {#section_y55_y1m_n1b}

### Type de diffusion {#stream-type}

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **Clé API :**<br/>media.streamType </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. SDK Version:** 2.2 <br/><br/>Available in [Media Collection API Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li>  <li> **Exemple de valeur :** <br/>"video" </li> <li> **Description :**<br/> Identifie le type de diffusion. Les valeurs valides sont "audio", "video" et "all".  <br/><br/>[Segments](/help/metrics-and-metadata/segments.md): <br/><br/>Streamtype « All » - Segmentez toutes les données de flux multimédia. <br/> **Règle :** Content (ID) existe <br/><br/>streamtype « Audio » - Segment toutes les données de flux audio. <br/>**Règle :** Content (ID) Exists AND Stream Type = audio <br/><br/>streamtype « Video » - Segment de toutes les données de flux vidéo. <br/>**Règle :** Contenu (ID) présent ET type de diffusion = vidéo <br/><br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. streamtype) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. streamtype) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À la fin de la VISITE </li> <li> **Nom du rapport :**<br/>Contenu </li> <li> **Données contextuelles :**<br/> (a. media. streamtype) </li> <li> **Flux de données :** <br/>videostreamtype </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.streamType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### Identifiant de contenu

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **Clé API :**<br/>media.id </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>"4586695ABC" </li> <li>**Description :**<br/> L'ID de contenu du contenu, qui peut être utilisé pour lier d'autres identifiants secteur/CMS, est égal à la dernière valeur de `s:asset:video_id` </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. name) </li> <li> **Pulsations :**<br/> (s : ressource : video_ id) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À la fin de la VISITE </li> <li> **Nom du rapport :**<br/>Contenu </li> <li> **Données contextuelles :**<br/> (a. media. name) </li> <li> **Flux de données :**<br/>vidéo </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.name) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Durée du contenu (variable)

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Clé API :**<br/>media.length </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> VOD : 128 ; Live : 86400 ; Linéaire : 1 800. </li><li> **Description :**<br/> Longueur du clip/Exécution - Longueur maximale (ou durée) du contenu consommé (en secondes). It equals the last value of `l:asset:length` from events of type Main. <br/>Si `l:asset:length` n'est pas défini, la dernière valeur de `l:asset:duration` est utilisée. <br/>Dans la création de rapports, « Durée de la vidéo » est la classification et « Durée du contenu (variable) » est l’eVar.  <br/> **Important :** Cette propriété est utilisée pour calculer plusieurs mesures, telles que les mesures de suivi de progression et l’audience moyenne par minute. Si cette valeur n’est pas définie, ou n’est pas supérieure à zéro, ces mesures ne sont pas disponibles.  Pour les médias en direct ayant une durée indéterminée, la valeur par défaut est 86400. <br/>Version 1.5.1 de pré-version `l:asset:duration`; après 1.5.1, c'est `l:asset:length.`<br/> **Date de publication : 13/09/18** </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. length) </li> <li> **Pulsations :**<br/> (l : ressource : length) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Durée du contenu (variable) </li> <li> **Données contextuelles :**<br/> (a. media. length) </li> <li> **Flux de données :**<br/>videolength </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Durée de la vidéo

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Clé API :**<br/>media.length </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> VOD : 128 ; Live : 86400 ; Linéaire : 1 800. </li> <li> **Description :**<br/> Longueur du clip/Exécution - Longueur maximale (ou durée) du contenu consommé (en secondes). Elle correspond à la dernière valeur de l:asset:length des événements de type Principal. Si l:asset:length n’est pas défini, la dernière valeur de l:asset:duration est utilisée. Dans la création de rapports, « Durée de la vidéo » est la classification et « Durée du contenu (variable) » est l’eVar.  <br/> **Important :** Cette propriété est utilisée pour calculer plusieurs mesures, telles que les mesures de suivi de progression et l’audience moyenne par minute. Si cette valeur n’est pas définie, ou n’est pas supérieure à zéro, ces mesures ne sont pas disponibles.  Pour les médias en direct ayant une durée indéterminée, la valeur par défaut est 86400. Avant la version 1.5.1 : l:asset:duration ; après la version 1.5.1 : l:asset:length.<br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. length) </li> <li> **Pulsations :**<br/> (l : ressource : length) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Durée de la vidéo </li> <li> **Données contextuelles :**<br/> (a. media. length) </li> <li> **Flux de données :** <br/>videoclassificationlength </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Type de contenu

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **Clé API :**<br/>media.contentType </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne limitée </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>"vod" </li> <li> **Description :**<br/> Valeurs disponibles par type **de diffusion**: <br/> _Audio :_ "song", "podcast", "audiobook", "radio" <br/> _Vidéo :_ Les clients « vod », « Direct », « Linéaire », « UGC », « dvod » <br/> peuvent fournir des valeurs personnalisées pour ce paramètre. This equals `s:stream:type.` If that is unset, this equals missing_content_type. </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. contenttype) </li> <li> **Pulsations :**<br/> (s : stream : type) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Type de contenu </li> <li> **Données contextuelles :**<br/> (a. contenttype) </li> <li> **Flux de données :**<br/>videocontenttype </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.<br/>contenttype) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### ID de session multimédia

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>Obtenue à partir du serveur principal </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.8 </li> <li> **Exemple de valeur :**<br/> 1482236761294786918253 </li> <li> **Description :**<br/> Ceci identifie une instance d'un flux de contenu propre à une lecture individuelle.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. vsid) </li> <li> **Heartbeat :**<br/> (s : event : sid) </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement </li> <li> **Variable réservée :**<br/>S.O. </li> <li> **Nom du rapport :**<br/>Personnalisé </li> <li> **Données contextuelles :**<br/> (a. media. vsid) </li> <li> **Flux de données :**<br/>vsid </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.vsid) </li> </ul> |

### Nom du lecteur de contenu

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **Clé API :**<br/>media.playerName </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> « Brightcove » </li> <li> **Description :**<br/> Nom du lecteur.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media.<br/>playerName) </li> <li> **Pulsations :**<br/> (s : sp : player_ name) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Nom du lecteur de contenu </li> <li> **Données contextuelles :**<br/> (a. media. playername) </li> <li> **Flux de données :**<br/>videoplayername </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.playerName) </li> </ul> |

### Canal de contenu

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **Clé API :**<br/>media.channel </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>"Sports" </li> <li> **Description :**<br/> Station de distribution/Canaux ou emplacement de lecture du contenu. N’importe quelle valeur de chaîne est acceptée ici.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. channel) </li> <li> **Pulsations :**<br/> (s : sp : channel) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Canal de contenu </li> <li> **Données contextuelles :**<br/> (a. media. channel) </li> <li> **Flux de données :**<br/>videochannel </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.channel) </li> </ul> |

### Segment de contenu

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> « 0-10 » </li> <li> **Description :**<br/> Intervalle qui décrit la partie du contenu qui a été consultée (en minutes). Le segment correspond aux valeurs min. et max. du curseur de lecture au cours d’une session de lecture.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Segment de contenu </li> <li> **Données contextuelles :**<br/> (a. media. segment) </li> <li> **Flux de données :**<br/>videosegment </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.segment) </li> </ul> |

### Nom du contenu (variable)

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **Clé API :**<br/>media.name </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.1 </li> <li> **Exemple de valeur :**<br/>"The Big Bang Theory" </li> <li> **Description :**<br/> Dans la création de rapports, le nom de la vidéo est la classification et le nom du contenu (variable) est l'evar. Il s’agit du nom « convivial » (lisible par l’homme) du contenu, égal à la dernière valeur de `s:asset:name.` <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media.<br/>Friendlyname) </li> <li> **Pulsations :**<br/> (s : ressource : name) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Nom du contenu (variable) </li> <li> **Données contextuelles :**<br/> (a. media. friendlyname) </li> <li> **Flux de données :**<br/>videoname </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.friendlyName) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Nom de la vidéo

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **Clé API :**<br/>media.name </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.1 </li> <li> **Exemple de valeur :**<br/>"The Big Bang Theory" </li> <li> **Description :**<br/> Il s'agit du nom « convivial » (lisible) du contenu, égal à la dernière valeur de `s:asset:name.`<br/>la création de rapports, le nom de la vidéo est la classification et le nom du contenu (variable). <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media.<br/>Friendlyname) </li> <li> **Pulsations :**<br/> (s : ressource : name) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Nom de la vidéo </li> <li> **Données contextuelles :**<br/> (a. media. friendlyname) </li> <li> **Flux de données :** <br/>videoclassificationname </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.friendlyName) </li> </ul> |

### Chemin de la vidéo

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Démarrage du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>"4586695ABC" </li> <li> **Description :**<br/> Possibilité de suivre le chemin de la visionneuse sur le site et/ou l'application pour voir le chemin emprunté pour afficher une vidéo particulière. Nombre entier et/ou combinaison de lettres.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. name) </li> <li> **Pulsations :**<br/> (s : ressource : video_ id) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>prop </li> <li> **Nom du rapport :**<br/>Chemin de la vidéo </li> <li> **Données contextuelles :**<br/> (a. media. name) </li> <li> **Flux de données :**<br/>videopath </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.name) </li> </ul> |

### Version du SDK

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **Clé API :**<br/>media.sdkVersion </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/>"2.62.0_release" </li> <li> **Description :**<br/> Version du SDK utilisée par le lecteur. Ceci peut avoir une valeur personnalisée ayant un sens pour votre lecteur. <br/><br/>Les clients devront créer leurs propres règles de traitement afin que la valeur soit disponible pour les rapports.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media.<br/>Sdkversion) </li> <li> **Pulsations :**<br/> (s : sp : sdk) </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement personnalisée </li> <li> **Variable réservée :**<br/>S.O. </li> <li> **Nom du rapport :** <br/> </li> <li> **Données contextuelles :**<br/> (a. media. sdkversion) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### Version de VHL

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/>"js-2.0.1.88-c8c0b1" </li> <li> **Description :**<br/> Version du SDK Heartbeat utilisée pour la session de suivi. <br/><br/>Les clients devront créer leurs propres règles de traitement afin que la valeur soit disponible pour les rapports.  <br/><br/>[Mediaheartbeat. version () ;](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media.<br/>Vhlversion) </li> <li> **Pulsations :**<br/> (s : sp : hb_ version) </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement personnalisée </li> <li> **Variable réservée :**<br/>S.O. </li> <li> **Nom du rapport :**<br/>Personnalisé </li> <li> **Données contextuelles :**<br/> (a. media. vhlversion) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## Métadonnées audio et vidéo standard {#section_pfc_hbm_n1b}

### Programme

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>SHOW </li> <li> **Clé API :**<br/>media.show </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> « Famille moderne » « Blacklist » « New Girl » </li> <li> **Description :**<br/> Nom du programme/Nom du <br/>programme n'est requis que si le programme fait partie d'une série.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. show) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. show) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Programme </li> <li> **Données contextuelles :**<br/> (a. media. show) </li> <li> **Flux de données :**<br/>videoshow </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.show) </li> </ul> |

### Format de diffusion

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>STREAM_FORMAT </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/>"Live" </li> <li> **Description :**<br/> Format du flux (En direct, VOD, Linéaire).  </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. format) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. format) </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement personnalisée </li> <li> **Variable réservée :**<br/>S.O. </li> <li> **Nom du rapport :**<br/>Personnalisé </li> <li> **Données contextuelles :**<br/> (a. media. format) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.format) </li> </ul> |

### Saison

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>SEASON </li> <li> **Clé API :**<br/>media.season </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> « 2 » </li> <li> **Description :**<br/> Numéro de saison auquel le programme appartient. La série de saisons n'est requise que si le programme fait partie d'une série.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. season) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. season) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Saison </li> <li> **Données contextuelles :**<br/> (a. media. season) </li> <li> **Flux de données :**<br/>videoseason </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.season) </li> </ul> |

### Épisode

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>EPISODE </li> <li> **Clé API :**<br/>media.episode </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> « 13 » </li> <li> **Description :**<br/> Numéro de l'épisode.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. episode) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. episode) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Épisode </li> <li> **Données contextuelles :**<br/> (a. media. episode) </li> <li> **Flux de données :**<br/>videoepisode </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.episode) </li> </ul> |

### ID de ressource

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>ASSET_ID </li> <li> **Clé API :**<br/>media.assetId </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> « 89745363 » </li> <li> **Description :**<br/> Il s'agit de l'identifiant unique du contenu du fichier multimédia, tel que l'identifiant de l'épisode de série télévisée, l'identifiant de l'élément film ou l'identifiant d'événement en direct. Ces ID sont généralement dérivés des autorités de métadonnées telles que EIDR, TMS/Gracenote ou Rovi. Ces identifiants peuvent également provenir d’autres systèmes propriétaires ou internes.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. asset) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. asset) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/> ID de ressource </li> <li> **Données contextuelles :**<br/> (a. media. asset) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.asset) </li> </ul> |

### Genre

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>GENRE </li> <li> **Clé API :**<br/>media.genre </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> « Drame », « Comédie » </li> <li> **Description :**<br/> Type ou regroupement du contenu tel que défini par le producteur de contenu. Les valeurs doivent être délimitées par une virgule dans la mise en œuvre de la variable. Dans les rapports, la liste eVar scinde chaque valeur en un élément de ligne, chaque élément de ligne recevant un poids de mesure égal.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. genre) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. genre) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Liste eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Genre </li> <li> **Données contextuelles :**<br/> (a. media. genre) </li> <li> **Flux de données :**<br/>videogenre </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.genre) </li> </ul> |

### Date de première diffusion

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>FIRST_AIR_DATE </li> <li> **Clé API :**<br/>media.firstAirDate </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Démarrage du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> « 2016-01-25 » </li> <li> **Description :**<br/> date à laquelle le contenu a été diffusé pour la première fois à la télévision. N’importe quel format de date est acceptable, mais Adobe recommande le format AAAA-MM-DD </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. airdate) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. airdate) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Date de première diffusion </li> <li> **Données contextuelles :**<br/> (a. media. airdate) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.airDate) </li> </ul> |

### Date de première distribution numérique

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>FIRST_DIGITAL_DATE </li> <li> **Clé API :**<br/>media.firstDigitalDate </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> « 2016-01-25 » </li> <li> **Description :**<br/> date à laquelle le contenu a d'abord été diffusé sur une plateforme ou une plateforme numérique. N’importe quel format de date est acceptable, mais Adobe recommande le format AAAA-MM-DD </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. digitaldate) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. digitaldate) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/> Date de première distribution numérique </li> <li> **Données contextuelles :**<br/> (a. media. digitaldate) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.digitalDate) </li> </ul> |

### Évaluation du contenu

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>RATING </li> <li> **Clé API :**<br/>media.rating </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/>TVY, TVG, TVPG, TVMA </li> <li> **Description :**<br/> Évaluation telle que définie par les directives des parents télévisés.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. rating) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. rating) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/> Évaluation du contenu </li> <li> **Données contextuelles :**<br/> (a. media. rating) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.rating) </li> </ul> |

### Créateur

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>ORIGINATOR </li> <li> **Clé API :**<br/>media.originator </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/>"Warner Brothers", "Sony", "Disney" </li> <li> **Description :**<br/> Créateur du contenu.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. originator) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. originator) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/> Émetteur </li> <li> **Données contextuelles :**<br/> (a. media. originator) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.originator) </li> </ul> |

### Réseau

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>NETWORK </li> <li> **Clé API :**<br/>media.network </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/>"Fox", "Bravo", "ESPN" </li> <li> **Description :**<br/> Nom réseau/canal.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. network) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. network) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Réseau </li> <li> **Données contextuelles :**<br/> (a. media. network) </li> <li> **Flux de données :**<br/>videonetwork </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.network) </li> </ul> |

### Type de programme

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>SHOW_TYPE </li> <li> **Clé API :**<br/>media.showType </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> « 0 » = épisode complet ; « 1 » = Aperçu/fin ; « 2 » = Clip ; « 3 » = Autre. </li> <li> **Description :**<br/> Type de contenu, exprimé sous la forme d'un nombre entier compris entre 0 et 3.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. type) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. type) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Type de programme </li> <li> **Données contextuelles :**<br/> (a. media. type) </li> <li> **Flux de données :**<br/>videoshowtype </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>MVPD </li> <li> **Clé API :**<br/>media.pass.mvpd </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/>"Comcast", "DirecTV", "Dish" </li> <li> **Description :**<br/> MVPD fourni via l'authentification Adobe.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. pass. mvpd) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. pass.<br/>mvpd) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>MVPD </li> <li> **Données contextuelles :**<br/> (a. media. pass. mvpd) </li> <li> **Flux de données :**<br/>videomvpd </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### Autorisé

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>AUTHORIZED </li> <li> **Clé API :**<br/>media.pass.auth </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> « TRUE » </li> <li> **Description :**<br/> L'utilisateur a été autorisé via adobepass. <br/>**Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. pass. auth) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. pass.<br/>authentique) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Autorisé </li> <li> **Données contextuelles :**<br/> (a. media. pass. auth) </li> <li> **Flux de données :**<br/>videoauthorized </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.pass.auth) </li> </ul> |

### Partie de la journée

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>DAY_PART </li> <li> **Clé API :**<br/>media.dayPart </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> </li> <li> **Description :**<br/> Propriété qui définit l'heure du jour de diffusion ou de lecture du contenu. Il peut s’agir d’une valeur quelconque définie selon les besoins par les clients.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. daypart) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. daypart) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Partie de la journée </li> <li> **Données contextuelles :**<br/> (a. media. daypart) </li> <li> **Flux de données :**<br/>videodaypart </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.dayPart) </li> </ul> |

### Type de flux multimédia

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>FEED </li> <li> **Clé API :**<br/>media.feed </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/>"East-HD", "West-HD", "East-SD" </li> <li> **Description :**<br/> Type de flux. <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. feed) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. feed) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Type de flux multimédia </li> <li> **Données contextuelles :**<br/> (a. media. feed) </li> <li> **Flux de données :**<br/>videofeedtype </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.feed) </li> </ul> |

### Artiste

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.artist </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemple de valeur :** <br/>"The Beatles" </li> <li> **Description :**<br/> Nom de l'artiste. <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. artist) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. artist) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> </li> <li> **Données contextuelles :**<br/> (a. media. artist) </li> <li> **Flux de données :** <br/>videoaudioartist </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.artist) </li> </ul> |

### Album

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.album </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemple de valeur :**<br/>"Revolver" </li> <li> **Description :**<br/> Nom de l'album. <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. album) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. album) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> </li> <li> **Données contextuelles :**<br/> (a. media. album) </li> <li> **Flux de données :** <br/>videoaudioalbum </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.album) </li> </ul> |

### Étiquette

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.label </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemple de valeur :**<br/>"Revolver" </li> <li> **Description :**<br/> Nom du libellé d'enregistrement. <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. label) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. label) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> </li> <li> **Données contextuelles :**<br/> (a. media. label) </li> <li> **Flux de données :** <br/>videoaudiolabel </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.label) </li> </ul> |

### Auteur

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.author </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemple de valeur :** <br/>"John Kennedy Toole" </li> <li> **Description :**<br/> Nom de l'auteur (d'un audiobook). <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. author) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. author) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> </li> <li> **Données contextuelles :**<br/> (a. media. author) </li> <li> **Flux de données :** <br/>videoaudioauthor </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.author) </li> </ul> |

### Station

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.station </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemple de valeur :** <br/>"NPR" </li> <li> **Description :**<br/> Nom/ID de la station radio. <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. station) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. station) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> </li> <li> **Données contextuelles :**<br/> (a. media. station) </li> <li> **Flux de données :**<br/>videoaudiostation </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.station) </li> </ul> |

### Éditeur

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.publisher </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemple de valeur :** <br/>"Random Bauhaus" </li> <li> **Description :**<br/> Nom de l'éditeur de contenu audio. <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. publisher) </li> <li> **Pulsations :**<br/> (s : meta :<br/>a. media. publisher) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> </li> <li> **Données contextuelles :**<br/> (a. media. publisher) </li> <li> **Flux de données :**<br/>videoaudiopublisher </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.publisher) </li> </ul> |

## Mesures audio et vidéo {#section_3D5F9C555274428AA6030D07596177E9}

### Démarrage du contenu multimédia

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement</li> <li> **Clé API :**<br/>S.O.</li> <li> **Type :**<br/>Chaîne</li> <li> **Envoyé avec :**<br/> Démarrage du média</li> <li> **Min. Version SDK min. :** Quelconque</li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> **Description :**<br/> Chargement de l'événement pour le média. (Ceci se produit lorsque le spectateur clique sur le bouton _Lecture_.) Ceci compte même en cas de publicités preroll, de mises en mémoire tampon, d’erreurs, etc.  <br/>**Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. view) </li> <li> **Pulsations :**<br/> (s : event :<br/>type = start) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/> Démarrages de médias </li> <li> **Données contextuelles :**<br/> (a. media. view) </li> <li> **Flux de données :**<br/>videostart </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.view) </li> </ul> |

### Démarrages de contenu

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> **Description :**<br/> La première image du média est consommée. If the user drops during ad, buffering, etc., then there would be no "Content Start" event.  <br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Le contenu commence </li> <li> **Données contextuelles :**<br/> (a. media. play) </li> <li> **Flux de données :**<br/>videoplay </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.play) </li> </ul> |

### Fin de contenu {#content-complete}

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> **Description :**<br/> Flux qui a été visionné jusqu'à la fin. Cela ne signifie pas nécessairement que l'utilisateur visionne ou écoute le flux entier ; ils auraient pu sauté. Cela signifie que l'utilisateur a atteint la fin du flux, 100 %. <br/>Voir également Fin [de session](quality-parameters.md#session-end)<br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Pulsations :**<br/> (s : event :<br/>type = complete) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Contenu terminé </li> <li> **Données contextuelles :**<br/> (a. media. complete) </li> <li> **Flux de données :**<br/>videocomplete </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.complete) </li> </ul> |

### Temps passé sur le contenu

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 105 </li> <li> **Description :**<br/> Additionne la durée de l'événement (en secondes) pour tous les événements de type PLAY sur le contenu principal. La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes.  <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Temps passé sur le contenu </li> <li> **Données contextuelles :**<br/> (a. media. timeplayed) </li> <li> **Flux de données :**<br/>videotime </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.timePlayed) </li> </ul> |

### passé sur le média

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 120 </li> <li> **Description :**<br/> Additionne la durée de l'événement (en secondes) pour tous les événements de type PLAY, à la fois sur le contenu principal et sur la publicité. La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes.  <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Temps passé sur le média </li> <li> **Données contextuelles :**<br/> (a. media. totaltimeplayed) </li> <li> **Flux de données :**<br/>videototaltime </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### Durée de lecture unique

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 94 </li> <li> **Description :**<br/> Valeur en secondes des segments uniques de contenu lus au cours d'une session. Exclut la durée de lecture des scénarios de retour en arrière, lorsqu’un utilisateur visionne le même segment de contenu plusieurs fois.  La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes.  <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Personnalisé </li> <li> **Données contextuelles :**<br/> (a. media. uniquetimeplayed) </li> <li> **Flux de données :**<br/>videouniquetimeplayed </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. uniquetimeplayed) </li> </ul> |

### Dix marqueurs de progression

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> **Description :**<br/> La tête de lecture transmet le marqueur de 10 % du contenu en fonction de la longueur. Le marqueur est compté une seule fois, même s’il effectue une recherche vers l’arrière. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés.  <br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Marqueur de progression de 10 % </li> <li> **Données contextuelles :**<br/> (a. media. progress 10) </li> <li> **Flux de données :**<br/>videoprogress10 </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.progress10) </li> </ul> |

### Marqueur de progression de 25 à 5 %

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> **Description :**<br/> La tête de lecture transmet le marqueur de 25 % du contenu en fonction de la longueur du contenu. Le marqueur n’est compté qu’une seule fois, même en cas de recherche vers l’arrière. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés.  <br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Marqueur de progression de 25 % </li> <li> **Données contextuelles :**<br/> (a. media. progress 25) </li> <li> **Flux de données :**<br/>videoprogress25 </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.progress25) </li> </ul> |

### Marqueur de progression cinquante %

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> **Description :**<br/> La tête de lecture transmet le marqueur 50 % du contenu en fonction de la longueur du contenu. Le marqueur n’est compté qu’une seule fois, même en cas de recherche vers l’arrière. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés.  <br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Marqueur de progression de 50 % </li> <li> **Données contextuelles :**<br/> (a. media. progress 50) </li> <li> **Flux de données :**<br/>videoprogress50 </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.progress50) </li> </ul> |

### Marqueur de progression soixante-dix-cinq

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :** <br/> **S.O.** </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> **Description :**<br/> La tête de lecture transmet le marqueur de 75 % du contenu en fonction de la longueur du contenu. Le marqueur n’est compté qu’une seule fois, même en cas de recherche vers l’arrière. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés.  <br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Marqueur de progression de 75 % </li> <li> **Données contextuelles :**<br/> (a. media. progress 75) </li> <li> **Flux de données :**<br/>videoprogress75 </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.progress75) </li> </ul> |

### Marqueur de progression quatre-vingt-dix-cinq

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> **Description :**<br/> La tête de lecture transmet le marqueur de 95 % du contenu en fonction de la longueur du contenu. Le marqueur n’est compté qu’une seule fois, même en cas de recherche vers l’arrière. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés.  <br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Marqueur de progression de 95 % </li> <li> **Données contextuelles :**<br/> (a. media. progress 95) </li> <li> **Flux de données :**<br/>videoprogress95 </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.progress95) </li> </ul> |

### Audience moyenne par minute

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>Supérieur ou égal à 1 </li> <li> **Description :**<br/> La mesure Audience moyenne moyenne correspond à la Durée totale de la visite du contenu, pour un élément média spécifique, divisé par sa longueur pour toutes ses sessions de lecture : <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Audience moyenne par minute </li> <li> **Données contextuelles :**<br/> (a. media. averageminuteaudience) </li> <li> **Flux de données :**<br/>videoaverageminuteaudience </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### Diffusions estimées

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 1 - Pendant une lecture de 19 minutes ; <br/>2 - Pendant une lecture de 31 minutes ; <br/>3 - Pendant une lecture de 78 minutes. </li> <li> **Description :**<br/> Nombre estimé de flux vidéo ou audio par contenu individuel. Cette valeur est augmentée pour chaque 30 minutes de temps de lecture (contenu + publicités). Les clients devront créer leurs propres règles de traitement afin que la valeur soit disponible pour les rapports. <br/><br/>Un flux est comptabilisé toutes les 30 minutes, en fonction de l'heure `ms_s` (ou de totaltimeplayed = Durée totale de la vidéo), semblable à : <br/> `estimatedStreams = ` <br/> `&nbsp;&nbsp;FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement personnalisée </li> <li> **Variable réservée :**<br/>S.O. </li> <li> **Nom du rapport :**<br/>Personnalisé </li> <li> **Données contextuelles :**<br/> (a. media. estimatedstreams) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. estimatedstreams) </li> </ul> |

### Flux touchés en pause

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.6 </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> **Description :**<br/> Cette valeur est true ou false. La valeur est égale à true si une ou plusieurs pauses ont eu lieu pendant la lecture d’un seul élément multimédia.  <br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Pulsations :**<br/> (s : event :<br/>type = pause) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Diffusion touchée en pause </li> <li> **Données contextuelles :**<br/> (a. media. pause) </li> <li> **Flux de données :**<br/>videopause </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.pause) </li> </ul> |

### Événements de mise en pause

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.6 </li> <li> **Exemple de valeur :**<br/> 2 </li> <li> **Description :**<br/> Cette mesure correspond au nombre de points de pause qui se sont produits au cours d'une session de lecture.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Pulsations :**<br/> (s : event :<br/>type = pause) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Événements de mise en pause </li> <li> **Données contextuelles :**<br/> (a. media. pausecount) </li> <li> **Flux de données :**<br/>videopausecount </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.pauseCount) </li> </ul> |

### Durée totale de pause

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.6 </li> <li> **Exemple de valeur :**<br/> 190 </li> <li> **Description :**<br/> Additionne la durée (en secondes) de tous les événements de type PAUSE. La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes. <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Durée totale de pause </li> <li> **Données contextuelles :**<br/> (a. media. pausetime) </li> <li> **Flux de données :**<br/>videopausetime </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.pauseTime) </li> </ul> |

### Le contenu reprend

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :** <br/> **media.resume** </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.6 </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> **Description :**<br/> Une reprise est comptabilisée pour chaque lecture qui reprend après plus de 30 minutes de mise en mémoire tampon, de mise en pause ou de blocage ou si cette valeur est définie par le lecteur sur videoinfo trackplay. <br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Pulsations :**<br/> (s : event :<br/>type = resume) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Reprises de contenu </li> <li> **Données contextuelles :**<br/> (a. media. resume) </li> <li> **Flux de données :**<br/>videoresume </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.resume) </li> </ul> |

### Affichages de segments de contenu

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> **Description :**<br/> Nombre de vues du contenu principal. Un affichage de segments du contenu est comptabilisé lorsqu’au moins une image est visionnée.  <br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée. </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Affichages de segments du contenu </li> <li> **Données contextuelles :**<br/> (a. media. segmentview) </li> <li> **Flux de données :**<br/>videosegmentviews </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.segmentView) </li> </ul> |

## Related APIs {#section_Related_APIs}

### createMediaObject APIs {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartbeatConfig APIs {#config-media-object}

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)

