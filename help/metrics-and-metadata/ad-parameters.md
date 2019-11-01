---
title: Paramètres de publicité
description: null
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Paramètres de publicité{#ad-parameters}

Cette rubrique présente une liste des données de publicité vidéo, y compris les valeurs de données contextuelles, qu’Adobe collecte via les variables de solution.

Description des données de tableau :

* **Mise en œuvre :** Informations sur les valeurs et les exigences de mise en œuvre
   * *Clé* : Variable, définie manuellement dans votre application ou automatiquement par le kit Adobe Media SDK.
   * *Obligatoire* : Indique si le paramètre est requis pour le suivi de la vidéo de base.
   * *Type* : Spécifie le type de variable à définir, chaîne ou nombre.
   * *Envoyé avec* : indique le moment où les données sont envoyées : *Media Start* est l’appel Analytics envoyé au démarrage du média, *Ad Start* est l’appel Analytics envoyé au démarrage de la publicité, etc. les appels de *fermeture* sont les appels d’analyse compilés envoyés directement du serveur de pulsation au serveur d’analyse à la fin de la session multimédia, ou à la fin de la publicité, du chapitre, etc. Les appels close ne sont pas disponibles dans les appels de paquets réseau.
   * *Min. Version SDK* : Indique la version SDK dont vous auriez besoin pour accéder au paramètre.
   * *Exemple de valeur* : Fournit un exemple d’utilisation de variable courante.
* **Paramètres réseau :** Affiche les valeurs transmises aux serveurs Adobe Analytics ou Heartbeat. Cette colonne affiche les noms des paramètres visibles dans les appels réseau générés par les kits Adobe Media SDK.
* **Création de rapports :** Informations sur la façon d’afficher et d’analyser les données vidéo.
   * *Disponible* : Indique si les données sont disponibles dans les rapports par défaut (*Oui*) ou nécessitent une configuration personnalisée (*Personnalisé*).
   * *Variable réservée* : Indique si les données sont capturées en tant qu’événement, valeur eVar, valeur prop ou classification dans une variable réservée.
   * *Nom du rapport* : Nom du rapport Adobe Analytics pour la variable.
   * *Données contextuelles* : Nom des données contextuelles Adobe Analytics transmises au serveur de rapports et utilisées dans le traitement des règles.
   * *Flux de données* : Nom de colonne pour la variable trouvée dans Clickstream ou les flux de données de diffusion en direct.
   * *Audience Manager* : Nom de caractéristique détecté dans Adobe Audience Manager.

>[!IMPORTANT]
>
>Ne modifiez pas les noms de classification des variables répertoriées ci-dessous qui sont
>décrit sous Variable de création de rapports/Réservé comme étant une "classification".
>Les classifications de médias sont définies lorsqu’une suite de rapports est activée pour les médias.
>Suivi. De temps à autre, Adobe ajoute de nouvelles propriétés et, dans ce cas,
>les clients doivent réactiver leurs suites de rapports pour accéder au nouveau média
>propriétés. Au cours du processus de mise à jour, Adobe détermine si la variable
>sont activées en vérifiant les noms des variables. Si l’un des
>ils sont manquants, Adobe les ajoute à nouveau.

## Données de publicité vidéo {#ad-video-data}

### Identifiant de publicité

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/>media.ad.id </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** Quelconque  </li> <li> ****<br/> Exemple de valeur : "2125" </li><li> **Description:**<br/>ID de la publicité. (Nombre entier et/ou combinaison de lettres)  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.ad.<br/>name) </li> <li> ****<br/> Heartbeat : (s:asset:ad_id) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À la fin de la VISITE </li> <li> **Nom du rapport :**<br/>Publicité </li> <li> ****<br/> Données contextuelles : (a.media.ad.<br/>name) </li> <li> **Flux de données :**<br/>videoad </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.ad.name) </li> </ul> |



### Position de la publicité dans la capsule

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/>media.ad.podPosition </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 1 </li><li> **Description:**<br/>Position (index) de la publicité dans la coupure publicitaire parente. La première publicité comporte l’index 0, la deuxième publicité l’index 1, etc.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.ad.<br/>podPosition) </li> <li> ****<br/> Heartbeat : (s:asset:pod_position) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Position de la publicité dans la capsule </li> <li> ****<br/> Données contextuelles : (a.media.ad.<br/>podPosition) </li> <li> **Flux de données :**<br/>videoadinpod </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.ad.podPosition) </li> </ul> |



### Longueur de la publicité

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/>media.ad.length </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** 1.5.1 </li> <li> ****<br/> Exemple de valeur : "15"  </li><li> **Description :**<br/>durée de la publicité vidéo en secondes.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.ad.<br/>length) </li> <li> ****<br/> Heartbeat : (l:asset:ad_length) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar et classification </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Longueur de la publicité et Longueur de la publicité (variable) </li> <li> ****<br/> Données contextuelles : (a.media.ad.<br/>length) </li> <li> **Flux de données :**<br/>videoadlength </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.ad.length) </li> </ul> |



### Nom du lecteur de publicités

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/>media.ad.playerName </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : "Roue libre" </li><li> **Description :**<br/>nom du lecteur responsable du rendu de la publicité.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.ad.<br/>playerName) </li> <li> ****<br/> Heartbeat : (s:sp:player_name) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Nom du lecteur de publicités </li> <li> ****<br/> Données contextuelles : (a.media.ad.<br/>playerName) </li> <li> **Flux de données :**<br/>videoadplayername </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.ad.playerName) </li> </ul> |



### Nom de la coupure publicitaire

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/>media.ad.podFriendlyName </li> <li> ****<br/> Obligatoire : SDK : Oui; API :Non. </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : "pre-roll" </li><li> **Description:**<br/>Nom convivial de la coupure publicitaire.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.ad.<br/>podFriendlyName) </li> <li> ****<br/> Heartbeat : (s:asset:pod_name) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/>Nom de la capsule </li> <li> ****<br/> Données contextuelles : (a.media.ad.<br/>podFriendlyName) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.ad.podFriendlyName) </li> </ul> |



### Index de la coupure publicitaire

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/>media.ad.podPosition </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 1 </li><li> **Description:**<br/>Index de la coupure publicitaire dans le contenu commençant à 1. Cette propriété est utilisée **uniquement** par le kit SDK Media pour générer l’identifiant de la capsule.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> </li> <li> **Heartbeat :**<br/> </li> </ul> | <ul> <li> **Disponible :**<br/>Non </li> <li> **Variable réservée :**<br/>S.O. </li> <li> **Nom du rapport :**<br/>S.O. </li> <li> **Données contextuelles :**<br/> </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> </li> </ul> |



### Position de la coupure publicitaire

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/>media.ad.podSecond </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 90 </li><li> **Description:**<br/>Décalage de la coupure publicitaire dans le contenu, en secondes.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.ad.<br/>podSecond) </li> <li> ****<br/> Heartbeat : (l:asset:pod_offset) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/>Position de la capsule </li> <li> ****<br/> Données contextuelles : (a.media.ad.<br/>podSecond) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.ad.podSecond) </li> </ul> |



### ID de coupure de publicité

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.ad.<br/>pod) </li> <li> ****<br/> Heartbeat : (s:asset:pod_id) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Capsule publicitaire </li> <li> ****<br/> Données contextuelles : (a.media.ad.<br/>pod) </li> <li> **Flux de données :**<br/>videoadpod </li> <li> **Audience Manager :**<br/> </li> </ul> |



### Nom de la publicité

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/>media.ad.name </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** 1.5.1 </li> <li> ****<br/> Exemple de valeur : "Ford F-150" </li><li> **Description : nom**<br/>convivial de la publicité.  Dans la création de rapports, « Nom de la publicité » est la classification et « Nom de la publicité (variable) » la variable eVar.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.ad.<br/>friendlyName) </li> <li> ****<br/> Heartbeat : (s:asset:ad_name) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar et classification </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Nom de la publicité et Nom de la publicité (variable) </li> <li> ****<br/> Données contextuelles : (a.media.ad.<br/>friendlyName) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.ad.friendlyName) </li> </ul> |



## Métadonnées de publicité standard {#standard-ad-metadata}

### Annonceur

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>ADVERTISER </li> <li> **Clé API :**<br/>media.ad.advertiser </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> </li><li> **Description :**<br/>Société/Marque dont le produit est présenté dans la publicité.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.ad.<br/>publicitaire) </li> <li> ****<br/> Heartbeat : (s:meta:<br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> <i>Annonceur </i> </li> <li> ****<br/> Données contextuelles : (a.media.ad.<br/>publicitaire) </li> <li> **Flux de données :**<br/>videoadvertiser </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.ad.advertiser) </li> </ul> |



### ID de campagne

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>CAMPAIGN_ID </li> <li> **Clé API :**<br/>media.ad.campaignId </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> ****<br/> Exemple de valeur : Entier ou nom (chaîne).  </li><li> **Description:**<br/>ID de la campagne publicitaire.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.ad.<br/>campaign) </li> <li> ****<br/> Heartbeat : (s:meta:<br/>a.media.ad.cacampaign) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> <i>ID de campagne </i> </li> <li> ****<br/> Données contextuelles : (a.media.ad.<br/>campaign) </li> <li> **Flux de données :**<br/>videocampaign </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.ad.campaign) </li> </ul> |



### ID d’élément créatif

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>CREATIVE_ID </li> <li> **Clé API :**<br/>media.ad.creativeId </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> ****<br/> Exemple de valeur : Entier ou nom (chaîne).  </li><li> **Description:**<br/>ID du créatif de la publicité.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.ad.<br/>créatif) </li> <li> ****<br/> Heartbeat : (s:meta:<br/>a.media.ad.créative) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> <i>ID d’élément créatif </i> </li> <li> ****<br/> Données contextuelles : (a.media.ad.<br/>créatif) </li> <li> **Flux de données :**<br/>adclassificationcreative </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.ad.creative) </li> </ul> |



### ID du site

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>SITE_ID </li> <li> **Clé API :**<br/>media.ad.siteId </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> </li><li> **Description:**<br/>ID du site publicitaire.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.ad.<br/>site) </li> <li> ****<br/> Heartbeat : (s:meta:<br/>a.media.ad.site) </li> </ul> | <ul> <li> **Disponible :**<br/> <i>Utiliser une règle de traitement personnalisée </i> </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> <i> </i> </li> <li> ****<br/> Données contextuelles : (a.media.ad.<br/>site) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.ad.site) </li> </ul> |



### URL de l’élément créatif

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>CREATIVE_URL </li> <li> **Clé API :**<br/>media.ad.creativeURL </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> </li><li> **Description:**<br/>URL de l’élément créatif de la publicité.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.ad.<br/>creativeURL) </li> <li> ****<br/> Heartbeat : (s:meta:<br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **Disponible :**<br/> <i>Utiliser une règle de traitement personnalisée </i> </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> <i> </i> </li> <li> ****<br/> Données contextuelles : (a.media.ad.<br/>creativeURL) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.ad.creativeURL) </li> </ul> |



### Identifiant de référencement

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>PLACEMENT_ID </li> <li> **Clé API :**<br/>media.ad.placementId </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> </li><li> **Description:**<br/>Identifiant de placement de la publicité.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.ad.<br/>placement) </li> <li> ****<br/> Heartbeat : (s:meta:<br/>a.media.ad.placement) </li> </ul> | <ul> <li> **Disponible :**<br/> <i>Utiliser une règle de traitement personnalisée </i> </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> <i> </i> </li> <li> ****<br/> Données contextuelles : (a.media.ad.<br/>placement) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.ad.placement) </li> </ul> |




## Mesures publicitaires {#ad-metrics}

### Démarrage de publicité

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de la publicité </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : TRUE </li><li> **Description :**<br/>Nombre de démarrages de publicités vidéo.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.ad.<br/>view) </li> <li> ****<br/> Heartbeat :  (s:event:type=start)<br/> (s:asset:type=ad) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Démarrages de publicité </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Données contextuelles : (a.media.ad.<br/>view) </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.ad.view) </li> </ul> |



### Publicité terminée

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Fermeture de la publicité </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : TRUE </li><li> **Description :**<br/>Nombre de vidéos terminées.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.ad.<br/>complete) </li> <li> ****<br/> Heartbeat : (s:event:type=complete)<br/> (s:asset:type=ad)  </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Fins de publicité </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Données contextuelles : (a.media.ad.<br/>complete) </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.ad.complete) </li> </ul> |



### passé sur la publicité

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Fermeture de la publicité </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 15 </li><li> **Description:**<br/>Durée totale, en secondes, passée à regarder la publicité (c.-à-d. le nombre de secondes de lecture).  La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes.  <br/>**Date de publication : 13/09/18**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.ad.<br/>timePlayed) </li> <li> **Heartbeat :**<br/> </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Temps passé sur la publicité </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Données contextuelles : (a.media.ad.<br/>timePlayed) </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.ad.timePlayed) </li> </ul> |



## API connexes {#section_Related_APIs}

### API createAdObject :

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### API createAdBreakObject :

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### API MediaHeartbeatConfig :

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)

