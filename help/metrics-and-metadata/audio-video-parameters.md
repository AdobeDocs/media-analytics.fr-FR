---
seo-title: Paramètres audio et vidéo
title: Paramètres audio et vidéo
uuid: fdacfb8b-db3e-46fb-b9ad-c3a749555b2a
translation-type: tm+mt
source-git-commit: 89870fcf20bdfa75a178ffc2124498b94cabe4a7

---


# Paramètres audio et vidéo{#audio-and-video-parameters}

>[!IMPORTANT]
>
>Le 7 février 2019, Adobe Analytics pour la vidéo et l’audio a publié un changement de nom de mesure. La mesure <i>Démarrages de média</i> sera désormais appelée <i>Lancements de média</i>. Ce changement a été apporté afin de refléter les normes du secteur dans les mesures et les rapports et de rendre la mesure facilement identifiable dans les rapports.

>[!NOTE]
>
>À compter du 13 septembre 2018, une modification a été apportée aux libellés de certaines dimensions, mesures et rapports afin de permettre le suivi du contenu croisé des analyses vidéo et audio. Les étiquettes qui ont été modifiées comprennent les suivantes : *démarrages de vidéo* en *démarrages de média*, *durée de la vidéo* en *durée du contenu* et *nom de la vidéo* en *nom du contenu*. Dans Reports and Analytics, les rapports vidéo ont tous été mis à jour de sorte à employer le terme « média » plutôt que « vidéo ». Ces changements apportés aux étiquettes n’ont eu aucune incidence sur la collecte de données ou les données historiques. Veuillez prendre note de ces modifications au cas où vous seriez amené à les utiliser dans le Report Builder ou dans toute autre extraction automatisée de données provenant de sources externes qui pourrait être affectée par celles-ci.

Cette rubrique présente une liste des données de contenu audio et vidéo, y compris les valeurs de données contextuelles, qu’Adobe collecte via les variables de solution.

Description des données de tableau :

* **Mise en œuvre :** Informations sur les valeurs et les exigences de mise en œuvre
   * *Clé* : Variable, définie manuellement dans votre application ou automatiquement par le kit Adobe Media SDK.
   * *Obligatoire* : Indique si le paramètre est requis pour le suivi audio et vidéo de base.
   * *Type* : Spécifie le type de variable à définir, chaîne ou nombre.
   * *Envoyé avec* : indique le moment où les données sont envoyées : *Media Start* est l’appel Analytics envoyé au démarrage du média, *Ad Start* est l’appel Analytics envoyé au démarrage de la publicité, etc. les appels de *fermeture* sont les appels d’analyse compilés envoyés directement du serveur de pulsation au serveur d’analyse à la fin de la session multimédia, ou à la fin de la publicité, du chapitre, etc. Les appels close ne sont pas disponibles dans les appels de paquets réseau.
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
>Ne modifiez pas les noms de classification des variables répertoriées ci-dessous, décrites sous Variable de création de rapports/Réservée comme "classification".\
>Les classifications des médias sont définies lorsqu’une suite de rapports est activée pour le suivi des médias. De temps à autre, Adobe ajoute de nouvelles propriétés et, dans ce cas, les clients doivent réactiver leurs suites de rapports pour accéder aux nouvelles propriétés du média. Au cours du processus de mise à jour, Adobe détermine si les classifications sont activées en vérifiant les noms des variables. Si l’un d’eux est manquant, Adobe en rajoute de nouveau.

## Données audio et vidéo principales {#section_y55_y1m_n1b}

### Type de diffusion {#stream-type}

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **Clé API :**<br/>media.streamType </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min.** Version du SDK : 2.2 <br/><br/>Disponible dans Présentation [de l’API](/help/media-collection-api/mc-api-overview.md) Media Collection ou [Télécharger des SDK - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li>  <li> **Exemple de valeur :** <br/>"video" </li> <li> ****<br/> Description : Identifie le type de flux. Les valeurs valides sont "audio", "video" et "all".  <br/><br/>[Segments](/help/metrics-and-metadata/segments.md)de création de rapports : Type de flux <br/><br/>multimédia : Tous - <br/>Segmenter toutes les données de flux média ; Règle : Le contenu (ID) existe sous <br/><br/>Type de diffusion multimédia : Audio - <br/>Segmenter toutes les données de flux audio ; Règle : Le contenu (ID) existe ET Type de flux média = Type de flux <br/><br/>média audio : "Vidéo" : <br/>segmente toutes les données de flux vidéo ; Règle : Le contenu (ID) existe ET le type de flux média != audio <br/><br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.streamType) </li> <li> ****<br/> Heartbeats : (s:meta:<br/>a.media.streamType) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À la fin de la VISITE </li> <li> **Nom du rapport :**<br/>Contenu </li> <li> ****<br/> Données contextuelles : (a.media.streamType) </li> <li> **Flux de données :** <br/>videostreamtype </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.streamType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### Identifiant de contenu

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **Clé API :**<br/>media.id </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>"4586695ABC" </li> <li>****<br/> Description: Content ID of the content, which can be used to tie back to other industry / CMS IDs, equal to the last value of `s:asset:video_id.` </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.name) </li> <li> **Heartbeats:**<br/> (s:asset:video_id) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À la fin de la VISITE </li> <li> **Nom du rapport :**<br/>Contenu </li> <li> ****<br/> Données contextuelles : (a.media.name) </li> <li> **Flux de données :**<br/>vidéo </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.name) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Durée du contenu (variable)

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Clé API :**<br/>media.length </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : VOD : 128; En direct : 86400; Linéaire : 1800. </li><li> ****<br/> Description : Longueur d’élément/Durée d’exécution : durée maximale (ou durée) du contenu consommé (en secondes). It equals the last value of `l:asset:length` from events of type Main. <br/>Si `l:asset:length` n’est pas définie, la dernière valeur de `l:asset:duration` est utilisée. <br/>Dans la création de rapports, « Durée de la vidéo » est la classification et « Durée du contenu (variable) » est l’eVar.  <br/> **Important :** Cette propriété est utilisée pour calculer plusieurs mesures, telles que les mesures de suivi de progression et l’audience moyenne par minute. Si cette valeur n’est pas définie, ou n’est pas supérieure à zéro, ces mesures ne sont pas disponibles.  Pour les médias en direct ayant une durée indéterminée, la valeur par défaut est 86400. <br/>Avant la version 1.5.1, il s’agissait de `l:asset:duration`; après 1.5.1, il s’agit `l:asset:length.` de <br/> **Date de publication : 13/09/18** </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.length) </li> <li> ****<br/> Heartbeats : (l:asset:length) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Durée du contenu (variable) </li> <li> ****<br/> Données contextuelles : (a.media.length) </li> <li> **Flux de données :**<br/>videolength </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Durée de la vidéo

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Clé API :**<br/>media.length </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : VOD : 128; En direct : 86400; Linéaire : 1800. </li> <li> ****<br/> Description : Longueur d’élément/Durée d’exécution : durée maximale (ou durée) du contenu consommé (en secondes). It equals the last value of `l:asset:length` from events of type Main. If `l:asset:length` is not set, then the last value of `l:asset:duration` is used. Dans la création de rapports, « Durée de la vidéo » est la classification et « Durée du contenu (variable) » est l’eVar.  <br/> **Important :** Cette propriété est utilisée pour calculer plusieurs mesures, telles que les mesures de suivi de progression et l’audience moyenne par minute. Si cette valeur n’est pas définie, ou n’est pas supérieure à zéro, ces mesures ne sont pas disponibles.  Pour les médias en direct ayant une durée indéterminée, la valeur par défaut est 86400. Pre Version 1.5.1, this was `l:asset:duration`; after 1.5.1, this is `l:asset:length.`<br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.length) </li> <li> ****<br/> Heartbeats : (l:asset:length) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Durée de la vidéo </li> <li> **Context Data:**<br/> (a.media.length) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Type de contenu

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **Clé API :**<br/>media.contentType </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne limitée </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>"vod" </li> <li> **Description:**<br/> Available values per **Stream Type**: <br/> _Audio :_ "song", "podcast", "audiobook", "radio" <br/> __ Vidéo : "VoD", "Live", "Linéaire", "UGC", "DVoD" <br/> Les clients peuvent fournir des valeurs personnalisées pour ce paramètre. Cette valeur est égale à `s:stream:type.` Si elle n’est pas définie, elle est égale à `missing_content_type.` </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.contentType) </li> <li> **Heartbeats:**<br/> (s:stream:type) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Type de contenu </li> <li> **Context Data:**<br/> (a.contentType) </li> <li> **Flux de données :**<br/>videocontenttype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.contentType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### ID de session multimédia

|   Mise en œuvre   | Network Parameters | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>Obtenue à partir du serveur principal </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** 1.5.8 </li> <li> ****<br/> Sample value: 1482236761294786918253 </li> <li> ****<br/> Description : Ceci identifie une instance d’un flux de contenu unique en son genre.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.vsid) </li> <li> ****<br/> Heartbeat : (s:event:sid) </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement </li> <li> **Variable réservée :**<br/>S.O. </li> <li> **Nom du rapport :**<br/>Personnalisé </li> <li> **Context Data:**<br/> (a.media.vsid) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.vsid) </li> </ul> |

### Nom du lecteur de contenu

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **Clé API :**<br/>media.playerName </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Sample value: "Brightcove" </li> <li> ****<br/> Description: Name of the player.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>playerName) </li> <li> ****<br/> Heartbeats : (s:sp:player_name) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Nom du lecteur de contenu </li> <li> ****<br/> Données contextuelles : (a.media.playerName) </li> <li> **Flux de données :**<br/>videoplayername </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.playerName) </li> </ul> |

### Canal de contenu

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **Clé API :**<br/>media.channel </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>"Sports" </li> <li> ****<br/> Description : Station de distribution/Canaux ou où le contenu est lu. N’importe quelle valeur de chaîne est acceptée ici.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.channel) </li> <li> ****<br/> Heartbeats: (s:sp:channel) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Canal de contenu </li> <li> ****<br/> Données contextuelles : (a.media.channel) </li> <li> **Flux de données :**<br/>videochannel </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.channel) </li> </ul> |

### Segment de contenu

|   Mise en œuvre   | Network Parameters | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Sent with:**<br/> Media Close </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Sample value: "0-10" </li> <li> **Description:**<br/> The interval that describes the part of the content that has been viewed (in minutes). Le segment correspond aux valeurs min. et max. du curseur de lecture au cours d’une session de lecture.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Segment de contenu </li> <li> ****<br/> Données contextuelles : (a.media.segment) </li> <li> **Flux de données :**<br/>videosegment </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.segment) </li> </ul> |

### Nom du contenu (variable)

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **Clé API :**<br/>media.name </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Min. Version SDK min. :** 1.5.1 </li> <li> **Exemple de valeur :**<br/>"The Big Bang Theory" </li> <li> **Description:This is the "friendly" (human-readable) name of the content, equal to the last value of In reporting, Video Name is the classification, and Content Name (variable) is the eVAR.**<br/>`s:asset:name.`<br/><br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>friendlyName) </li> <li> ****<br/> Heartbeats: (s:asset:name) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Nom du contenu (variable) </li> <li> ****<br/> Données contextuelles : (a.media.friendlyName) </li> <li> **Flux de données :**<br/>videoname </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Nom de la vidéo

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **Clé API :**<br/>media.name </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** 1.5.1 </li> <li> **Exemple de valeur :**<br/>"The Big Bang Theory" </li> <li> ****<br/> Description : Il s’agit du nom "convivial" (lisible par l’utilisateur) du contenu, égal à la dernière valeur de `s:asset:name.` <br/>Dans les rapports, Nom de la vidéo est la classification et Nom du contenu (variable) est l’eVAR.  <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.<br/>friendlyName) </li> <li> ****<br/> Heartbeats : (s:asset:name) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Nom de la vidéo </li> <li> ****<br/> Données contextuelles : (a.media.friendlyName) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

### Chemin de la vidéo

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>"4586695ABC" </li> <li> ****<br/> Description : Permet d’effectuer le suivi du chemin d’un lecteur sur un site et/ou une application, de voir le chemin qu’il a emprunté pour afficher une vidéo particulière. Nombre entier et/ou combinaison de lettres.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.name) </li> <li> ****<br/> Heartbeats : (s:asset:video_id) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>prop </li> <li> **Nom du rapport :**<br/>Chemin de la vidéo </li> <li> ****<br/> Données contextuelles : (a.media.name) </li> <li> **Flux de données :**<br/>videopath </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.name) </li> </ul> |

### Version du SDK

|   Mise en œuvre   | Network Parameters | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **Clé API :**<br/>media.sdkVersion </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/>"2.62.0_release" </li> <li> ****<br/> Description : Version du SDK utilisée par le lecteur. Ceci peut avoir une valeur personnalisée ayant un sens pour votre lecteur. <br/><br/>Les clients devront créer leurs propres règles de traitement afin que la valeur soit disponible pour les rapports.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.<br/>sdkVersion) </li> <li> ****<br/> Heartbeats : (s:sp:sdk) </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement personnalisée </li> <li> **Variable réservée :**<br/>S.O. </li> <li> **Nom du rapport :** <br/> </li> <li> **Context Data:**<br/> (a.media.sdkVersion) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### Version de VHL

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/>"js-2.0.1.88-c8c0b1" </li> <li> ****<br/> Description : Version du SDK Media utilisée pour la session de suivi. <br/><br/>Les clients devront créer leurs propres règles de traitement afin que la valeur soit disponible pour les rapports.  <br/><br/>[MediaHeartbeat.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.<br/>vhlVersion) </li> <li> ****<br/> Heartbeats : (s:sp:hb_version) </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement personnalisée </li> <li> **Variable réservée :**<br/>S.O. </li> <li> **Nom du rapport :**<br/>Personnalisé </li> <li> ****<br/> Données contextuelles : (a.media.vhlVersion) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## Métadonnées audio et vidéo standard {#section_pfc_hbm_n1b}

### Programme

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>SHOW </li> <li> **Clé API :**<br/>media.show </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> ****<br/> Exemple de valeur : "Famille Moderne" "Liste noire" "Nouvelle Fille" </li> <li> ****<br/> Description : Nom du programme/de la série Le nom du <br/>programme n'est requis que si le programme fait partie d'une série.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.show) </li> <li> ****<br/> Heartbeats : (s:meta:<br/>a.media.show) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Programme </li> <li> ****<br/> Données contextuelles : (a.media.show) </li> <li> **Flux de données :**<br/>videoshow </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.show) </li> </ul> |

### Format de diffusion

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>STREAM_FORMAT </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/>"Live" </li> <li> **Description:**<br/> Format of the stream (Live, VOD, Linear).  </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.format) </li> <li> ****<br/> Heartbeats : (s:meta:<br/>a.media.format) </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement personnalisée </li> <li> **Variable réservée :**<br/>S.O. </li> <li> **Nom du rapport :**<br/>Personnalisé </li> <li> **Context Data:**<br/> (a.media.format) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.format) </li> </ul> |

### Saison

|   Mise en œuvre   | Network Parameters | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>SEASON </li> <li> **Clé API :**<br/>media.season </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> ****<br/> Exemple de valeur : "2" </li> <li> ****<br/> Description : Numéro de saison auquel appartient le spectacle.  La série de saisons n’est requise que si le spectacle fait partie d’une série.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.season) </li> <li> ****<br/> Heartbeats : (s:meta:<br/>a.media.season) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Saison </li> <li> **Context Data:**<br/> (a.media.season) </li> <li> **Flux de données :**<br/>videoseason </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.season) </li> </ul> |

### Épisode

|   Mise en œuvre   | Network Parameters | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>EPISODE </li> <li> **Clé API :**<br/>media.episode </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> ****<br/> Exemple de valeur : "13" </li> <li> ****<br/> Description : Numéro de l’épisode.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.episode) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.episode)<br/> </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Épisode </li> <li> ****<br/> Données contextuelles : (a.media.episode) </li> <li> **Flux de données :**<br/>videoepisode </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.episode) </li> </ul> |

### ID de ressource

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>ASSET_ID </li> <li> **Clé API :**<br/>media.assetId </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> ****<br/> Exemple de valeur : "89745363" </li> <li> ****<br/> Description : Il s’agit de l’identifiant unique pour le contenu du fichier multimédia, tel que l’identifiant d’épisode de série TV, l’identifiant de fichier de film ou l’identifiant d’événement en direct. Ces ID sont généralement dérivés des autorités de métadonnées telles que EIDR, TMS/Gracenote ou Rovi. Ces identifiants peuvent également provenir d’autres systèmes propriétaires ou internes.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.asset) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.asset)<br/> </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/> ID de ressource </li> <li> ****<br/> Données contextuelles : (a.media.asset) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.asset) </li> </ul> |

### Genre

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>GENRE </li> <li> **Clé API :**<br/>media.genre </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> ****<br/> Exemple de valeur : "Drama", "Comédie" </li> <li> **Description:**<br/> Type or grouping of content as defined by content producer. Les valeurs doivent être délimitées par une virgule dans la mise en œuvre de la variable. Dans les rapports, la liste eVar scinde chaque valeur en un élément de ligne, chaque élément de ligne recevant un poids de mesure égal.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.genre) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.genre)<br/> </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Liste eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Genre </li> <li> ****<br/> Context Data: (a.media.genre) </li> <li> **Flux de données :**<br/>videogenre </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.genre) </li> </ul> |

### Date de première diffusion

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>FIRST_AIR_DATE </li> <li> **Clé API :**<br/>media.firstAirDate </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> ****<br/> Sample value: "2016-01-25" </li> <li> ****<br/> Description : Date à laquelle le contenu a été diffusé pour la première fois à la télévision. N’importe quel format de date est acceptable, mais Adobe recommande le format AAAA-MM-DD </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.airDate) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.airDate)<br/> </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Date de première diffusion </li> <li> ****<br/> Données contextuelles : (a.media.airDate) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.airDate) </li> </ul> |

### Date de première distribution numérique

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>FIRST_DIGITAL_DATE </li> <li> **Clé API :**<br/>media.firstDigitalDate </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> ****<br/> Sample value: "2016-01-25" </li> <li> ****<br/> Description : Date à laquelle le contenu a été diffusé pour la première fois sur une chaîne ou une plateforme numérique. N’importe quel format de date est acceptable, mais Adobe recommande le format AAAA-MM-DD </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.digitalDate) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.digitalDate)<br/> </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/> Date de première distribution numérique </li> <li> ****<br/> Données contextuelles : (a.media.digitalDate) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.digitalDate) </li> </ul> |

### Évaluation du contenu

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>RATING </li> <li> **Clé API :**<br/>media.rating </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/>TVY, TVG, TVPG, TVMA </li> <li> ****<br/> Description : Évaluation telle que définie par les lignes directrices parentales de TV.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.rating) </li> <li> ****<br/> Heartbeats : (s:meta:<br/>a.media.rating) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/> Évaluation du contenu </li> <li> ****<br/> Données contextuelles : (a.media.rating) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.rating) </li> </ul> |

### Créateur

|   Mise en œuvre   | Network Parameters | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>ORIGINATOR </li> <li> **Clé API :**<br/>media.originator </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/>"Warner Brothers", "Sony", "Disney" </li> <li> **Description:**<br/> Creator of the content.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.originator) </li> <li> ****<br/> Heartbeats : (s:meta:<br/>a.media.originator) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/> Émetteur </li> <li> **Context Data:**<br/> (a.media.originator) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.originator) </li> </ul> |

### Réseau

|   Mise en œuvre   | Network Parameters | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>NETWORK </li> <li> **Clé API :**<br/>media.network </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/>"Fox", "Bravo", "ESPN" </li> <li> ****<br/> Description : Nom réseau/canal.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.network) </li> <li> ****<br/> Heartbeats : (s:meta:<br/>a.media.network) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Réseau </li> <li> **Context Data:**<br/> (a.media.network) </li> <li> **Flux de données :**<br/>videonetwork </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.network) </li> </ul> |

### Type de programme

|   Mise en œuvre   | Network Parameters | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>SHOW_TYPE </li> <li> **Clé API :**<br/>media.showType </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> ****<br/> Exemple de valeur : "0" = épisode complet; "1" = Aperçu/fin de session; "2" = Clip; "3" = Autre. </li> <li> ****<br/> Description : Type de contenu, exprimé sous la forme d’un entier compris entre 0 et 3.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.type) </li> <li> ****<br/> Heartbeats : (s:meta:<br/>a.media.type) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Type de programme </li> <li> ****<br/> Données contextuelles : (a.media.type) </li> <li> **Flux de données :**<br/>videoshowtype </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>MVPD </li> <li> **Clé API :**<br/>media.pass.mvpd </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/>"Comcast", "DirecTV", "Dish" </li> <li> ****<br/> Description : MVPD fourni via l’authentification Adobe.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.pass.mvpd) </li> <li> ****<br/> Heartbeats : (s:meta:<br/>a.media.pass.<br/>mvpd) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>MVPD </li> <li> ****<br/> Données contextuelles : (a.media.pass.mvpd) </li> <li> **Flux de données :**<br/>videomvpd </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### Autorisé

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>AUTHORIZED </li> <li> **Clé API :**<br/>media.pass.auth </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> ****<br/> Exemple de valeur : "TRUE" </li> <li> ****<br/> Description : L’utilisateur a été autorisé via l’authentification Adobe.  <br/>**Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.pass.auth) </li> <li> ****<br/> Heartbeats : (s:meta:<br/>a.media.pass.<br/>auth) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Autorisé </li> <li> **Context Data:**<br/> (a.media.pass.auth) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.pass.auth) </li> </ul> |

### Partie de la journée

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>DAY_PART </li> <li> **Clé API :**<br/>media.dayPart </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> </li> <li> ****<br/> Description : Propriété qui définit l’heure de diffusion ou de lecture du contenu. Il peut s’agir d’une valeur quelconque définie selon les besoins par les clients.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.dayPart) </li> <li> ****<br/> Heartbeats : (s:meta:<br/>a.media.dayPart) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Partie de la journée </li> <li> ****<br/> Données contextuelles : (a.media.dayPart) </li> <li> **Flux de données :**<br/>videodaypart </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.dayPart) </li> </ul> |

### Type de flux multimédia

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>FEED </li> <li> **Clé API :**<br/>media.feed </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/>"East-HD", "West-HD", "East-SD" </li> <li> ****<br/> Description : Type de flux.  <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.feed) </li> <li> ****<br/> Heartbeats : (s:meta:<br/>a.media.feed) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Type de flux multimédia </li> <li> ****<br/> Données contextuelles : (a.media.feed) </li> <li> **Flux de données :**<br/>videofeedtype </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.feed) </li> </ul> |

### Artiste

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.artist </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min.** SDK Version: 1.5.7 Available in Media Collection Overview or Download SDKs - Versions 2.2.<br/>[](/help/media-collection-api/mc-api-overview.md)[](/help/sdk-implement/download-sdks.md)  </li> <li> **Exemple de valeur :** <br/>"The Beatles" </li> <li> ****<br/> Description: Name of the artist.  <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.artist) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.artist)<br/> </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> </li> <li> ****<br/> Données contextuelles : (a.media.artiste) </li> <li> **Flux de données :** <br/>videoaudioartist </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.artist) </li> </ul> |

### Album

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.album </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Min.** SDK Version: 1.5.7 Available in Media Collection Overview or Download SDKs - Versions 2.2.<br/>[](/help/media-collection-api/mc-api-overview.md)[](/help/sdk-implement/download-sdks.md)  </li> <li> **Exemple de valeur :**<br/>"Revolver" </li> <li> ****<br/> Description: Name of the album.  <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.album) </li> <li> ****<br/> Heartbeats : (s:meta:<br/>a.media.album) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> </li> <li> ****<br/> Données contextuelles : (a.media.album) </li> <li> **Flux de données :** <br/>videoaudioalbum </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.album) </li> </ul> |

### Étiquette

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.label </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Min.** SDK Version: 1.5.7 Available in Media Collection Overview or Download SDKs - Versions 2.2.<br/>[](/help/media-collection-api/mc-api-overview.md)[](/help/sdk-implement/download-sdks.md)  </li> <li> **Exemple de valeur :**<br/>"Revolver" </li> <li> ****<br/> Description : Nom du libellé de l’enregistrement.  <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.label) </li> <li> ****<br/> Heartbeats : (s:meta:<br/>a.media.label) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> </li> <li> ****<br/> Données contextuelles : (a.media.label) </li> <li> **Flux de données :** <br/>videoaudiolabel </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.label) </li> </ul> |

### Auteur

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.author </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min.** Version du SDK : 1.5.7 <br/>Disponible dans Présentation [de la collection](/help/media-collection-api/mc-api-overview.md) multimédia ou [Télécharger des SDK - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemple de valeur :** <br/>"John Kennedy Toole" </li> <li> ****<br/> Description : Nom de l’auteur (d’un livre audio).  <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.author) </li> <li> ****<br/> Heartbeats : (s:meta:<br/>a.media.author) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> </li> <li> **Context Data:**<br/> (a.media.author) </li> <li> **Flux de données :** <br/>videoaudioauthor </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.author) </li> </ul> |

### Station

|   Mise en œuvre   | Network Parameters | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.station </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min.** Version du SDK : 1.5.7 <br/>Disponible dans Présentation [de la collection](/help/media-collection-api/mc-api-overview.md) multimédia ou [Télécharger des SDK - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemple de valeur :** <br/>"NPR" </li> <li> ****<br/> Description : Nom / ID de la station de radio.  <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.station) </li> <li> ****<br/> Heartbeats : (s:meta:<br/>a.media.station) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> </li> <li> ****<br/> Données contextuelles : (a.media.station) </li> <li> **Flux de données :**<br/>videoaudiostation </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.station) </li> </ul> |

### Éditeur

|   Mise en œuvre   | Network Parameters | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.publisher </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min.** Version du SDK : 1.5.7 <br/>Disponible dans Présentation [de la collection](/help/media-collection-api/mc-api-overview.md) multimédia ou [Télécharger des SDK - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemple de valeur :** <br/>"Random Bauhaus" </li> <li> **Description:**<br/> Name of the audio content publisher.  <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.publisher) </li> <li> ****<br/> Heartbeats : (s:meta:<br/>a.media.publisher) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> </li> <li> ****<br/> Données contextuelles : (a.media.publisher) </li> <li> **Flux de données :**<br/>videoaudiopublisher </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.publisher) </li> </ul> |

## Mesures audio et vidéo {#section_3D5F9C555274428AA6030D07596177E9}

### Démarrage du contenu multimédia

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement</li> <li> **Clé API :**<br/>S.O.</li> <li> **Type :**<br/>Chaîne</li> <li> ****<br/> Envoyé avec : Media Start</li> <li> **Min. Version SDK min. :** Quelconque</li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> ****<br/> Description : Evénement Load pour le média. (Ceci se produit lorsque le spectateur clique sur le bouton _Lecture_.) Ceci compte même en cas de publicités preroll, de mises en mémoire tampon, d’erreurs, etc.  <br/>**Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.view) </li> <li> ****<br/> Heartbeats : (s:event:<br/>type=start) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> ****<br/> Nom du rapport : Début du média </li> <li> ****<br/> Données contextuelles : (a.media.view) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.view) </li> </ul> |

### Démarrages de contenu

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> **Description:**<br/> First frame of media is consumed. If the user drops during ad, buffering, etc., then there would be no "Content Start" event.  <br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Le contenu commence </li> <li> ****<br/> Données contextuelles : (a.media.play) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.play) </li> </ul> |

### Fin de contenu {#content-complete}

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> ****<br/> Description : Un flux qui a été visionné jusqu’à la fin. Cela ne signifie pas nécessairement que l'utilisateur a regardé ou écouté l'ensemble du flux; ils auraient pu sauter. Cela signifie uniquement que l’utilisateur a atteint la fin du flux, à 100 %. <br/>Voir aussi [Fin](quality-parameters.md#session-end) de session <br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> ****<br/> Heartbeats : (s:event:<br/>type=complete) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Contenu terminé </li> <li> ****<br/> Données contextuelles : (a.media.complete) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.complete) </li> </ul> |

### Temps passé sur le contenu

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 105 </li> <li> **Description:**<br/> Sums the event duration (in seconds) for all events of type PLAY on the main content.  La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes.  <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Temps passé sur le contenu </li> <li> **Context Data:**<br/> (a.media.timePlayed) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.timePlayed) </li> </ul> |

### passé sur le média

|   Mise en œuvre   | Network Parameters | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Nombre </li> <li> **Sent with:**<br/> Media Close </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 120 </li> <li> **Description:**<br/> Sums the event duration (in seconds) for all events of type PLAY, both main and ad content.  La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes.  <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Temps passé sur le média </li> <li> ****<br/> Données contextuelles : (a.media.totalTimePlayed) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### Durée de lecture unique

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Nombre </li> <li> **Sent with:**<br/> Media Close </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 94 </li> <li> ****<br/> Description : Valeur en secondes des segments uniques de contenu lus au cours d’une session. Exclut la durée de lecture des scénarios de retour en arrière, lorsqu’un utilisateur visionne le même segment de contenu plusieurs fois.  La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes.  <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Personnalisé </li> <li> ****<br/> Données contextuelles : (a.media.uniqueTimePlayed) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.uniqueTimePlayed) </li> </ul> |

### Marqueur de progression de 10 %

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> ****<br/> Description : La tête de lecture transmet le marqueur 10 % du contenu en fonction de la longueur. Le marqueur est compté une seule fois, même s’il effectue une recherche vers l’arrière. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés.  <br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Marqueur de progression de 10 % </li> <li> ****<br/> Données contextuelles : (a.media.progress10) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.progress10) </li> </ul> |

### Marqueur de progression de 25 %

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> **Description:**<br/> Playhead passes the 25% marker of content based on content length. Le marqueur n’est compté qu’une seule fois, même en cas de recherche vers l’arrière. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés.  <br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Marqueur de progression de 25 % </li> <li> **Context Data:**<br/> (a.media.progress25) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress25) </li> </ul> |

### Marqueur de progression de 50 %

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> **Description:**<br/> Playhead passes the 50% marker of content based on content length. Le marqueur n’est compté qu’une seule fois, même en cas de recherche vers l’arrière. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés.  <br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Marqueur de progression de 50 % </li> <li> **Context Data:**<br/> (a.media.progress50) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.progress50) </li> </ul> |

### Marqueur de progression de 75 %

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :** <br/> **S.O.** </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> ****<br/> Description : La tête de lecture transmet le marqueur 75 % du contenu en fonction de la longueur du contenu. Le marqueur n’est compté qu’une seule fois, même en cas de recherche vers l’arrière. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés.  <br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Marqueur de progression de 75 % </li> <li> ****<br/> Données contextuelles : (a.media.progress75) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.progress75) </li> </ul> |

### Marqueur de progression de 95 %

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> ****<br/> Description : La tête de lecture transmet le marqueur 95 % du contenu en fonction de la longueur du contenu. Le marqueur n’est compté qu’une seule fois, même en cas de recherche vers l’arrière. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés.  <br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Marqueur de progression de 95 % </li> <li> ****<br/> Données contextuelles : (a.media.progress95) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.progress95) </li> </ul> |

### Audience moyenne par minute

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>Supérieur ou égal à 1 </li> <li> ****<br/> Description : La mesure Audience moyenne par minute est calculée comme Durée totale de la visite du contenu pour un élément multimédia spécifique, divisée par sa durée pour toutes ses sessions de lecture : <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Audience moyenne par minute </li> <li> ****<br/> Données contextuelles : (a.media.mediumMinuteAudience) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### Données fédérées

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> ****<br/> Type: boolean </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Sample value:**<br/> true  </li> <li> ****<br/> Description: Set to true when the hit is federated (i.e., received by the customer as part of a federated data share, rather than their own implementation). </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement personnalisée </li> <li> **Variable réservée :**<br/>S.O. </li> <li> **Nom du rapport :**<br/>S.O. </li> <li> ****<br/> Context Data: (a.media.federated) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.federated) </li> </ul> |

### Diffusions estimées

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Sample value: 1 - For a 19 minutes playback; 2 - For a 31 minutes playback; 3 - For a 78 minutes playback.<br/><br/> </li> <li> ****<br/> Description : Nombre estimé de flux vidéo ou audio par contenu individuel. Cette valeur est augmentée pour chaque 30 minutes de temps de lecture (contenu + publicités). Les clients devront créer leurs propres règles de traitement afin que la valeur soit disponible pour les rapports. <br/><br/>Un flux est comptabilisé toutes les 30 minutes, en fonction du `ms_s` (ou totalTimePlayed = Durée totale de la vidéo), comme suit : <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement personnalisée </li> <li> **Variable réservée :**<br/>S.O. </li> <li> **Nom du rapport :**<br/>Personnalisé </li> <li> ****<br/> Données contextuelles : (a.media.estimationStreams) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.estimationStreams) </li> </ul> |

### Flux touchés en pause

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.6 </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> ****<br/> Description : Cette valeur est vraie ou fausse. La valeur est égale à true si une ou plusieurs pauses ont eu lieu pendant la lecture d’un seul élément multimédia.  <br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> ****<br/> Heartbeats : (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Diffusion touchée en pause </li> <li> ****<br/> Données contextuelles : (a.media.pause) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.pause) </li> </ul> |

### Événements de mise en pause

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Nombre </li> <li> **Sent with:**<br/> Media Close </li> <li> **Min. Version SDK min. :** 1.5.6 </li> <li> ****<br/> Exemple de valeur : 2 </li> <li> **Description:**<br/> This metric is computed as a count of pause periods that occurred during a playback session.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats:**<br/> (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Événements de mise en pause </li> <li> **Context Data:**<br/> (a.media.pauseCount) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pauseCount) </li> </ul> |

### Durée totale de pause

|   Mise en œuvre   | Network Parameters | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Nombre </li> <li> **Sent with:**<br/> Media Close </li> <li> **Min. Version SDK min. :** 1.5.6 </li> <li> ****<br/> Exemple de valeur : 190 </li> <li> ****<br/> Description : Indique la durée (en secondes) de tous les événements de type PAUSE. La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes. <br/> **Date de publication : 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Durée totale de pause </li> <li> ****<br/> Données contextuelles : (a.media.pauseTime) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.pauseTime) </li> </ul> |

### Le contenu reprend

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :** <br/> **media.resume** </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5.6 </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> **Description:**<br/> A Resume is counted for each playback that resumes after more than 30 minutes of buffer, pause, or stall period OR if this value is set by the player on the VideoInfo trackPlay. <br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée.  </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats:**<br/> (s:event:<br/>type=resume) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Reprises de contenu </li> <li> ****<br/> Données contextuelles : (a.media.resume) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.resume) </li> </ul> |

### Affichages de segments de contenu

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/>TRUE </li> <li> ****<br/> Description : Nombre d’affichages du contenu principal. Un affichage de segments du contenu est comptabilisé lorsqu’au moins une image est visionnée.  <br/> **Important :** Cette valeur ne peut être égale à true que si elle est définie. Si elle n’est pas définie, aucune valeur n’est renvoyée. </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Affichages de segments du contenu </li> <li> ****<br/> Données contextuelles : (a.media.segmentView) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.segmentView) </li> </ul> |

### Nombre de publicités

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> ****<br/> Clé SDK : S/O </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 2 </li> <li> ****<br/> Description : Nombre de publicités démarrées au cours de la session multimédia.   <br/> </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement personnalisée </li> <li> **Variable réservée :**<br/>S.O. </li> <li> **Nom du rapport :**<br/>Personnalisé </li> <li> ****<br/> Données contextuelles : (a.media.adCount) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.adCount) </li> </ul> |

### Nombre de chapitres

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> ****<br/> Clé SDK : S/O </li> <li> **Clé API :**<br/>S.O. </li> <li> **Type :**<br/>Nombre </li> <li> **Sent with:**<br/> Media Close </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 2 </li> <li> ****<br/> Description : Nombre de chapitres démarrés au cours de la session média.   <br/> </li></ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Heartbeats :**<br/>S.O. </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement personnalisée </li> <li> **Variable réservée :**<br/>S.O. </li> <li> **Nom du rapport :**<br/>Personnalisé </li> <li> ****<br/> Données contextuelles : (a.media.chapterCount) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapterCount) </li> </ul> |

## API connexes {#section_Related_APIs}

### createMediaObject APIs {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartbeatConfig APIs {#config-media-object}

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)

