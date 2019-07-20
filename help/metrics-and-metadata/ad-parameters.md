---
seo-title: Paramètres de publicité
title: Paramètres de publicité
uuid: 92 cd 7 f 97-bb 5 a -4 de 6-8946-453 d 30271 d 0 f
translation-type: tm+mt
source-git-commit: 180eafdfc536039820ade0b52e5c55f874719d8e

---


# Paramètres de publicité{#ad-parameters}

Cette rubrique présente une liste des données de publicité vidéo, y compris les valeurs de données contextuelles, qu’Adobe collecte via les variables de solution.

Description des données de tableau :

* **Mise en œuvre :** Informations sur les valeurs et les exigences de mise en œuvre
   * *Clé* : Variable, définie manuellement dans votre application ou automatiquement par le kit Adobe Media SDK.
   * *Obligatoire* : Indique si le paramètre est requis pour le suivi de la vidéo de base.
   * *Type* : Spécifie le type de variable à définir, chaîne ou nombre.
   * *Envoyé avec* - Indique quand les données sont envoyées : *Media Start* est l'appel Analytics envoyé au démarrage du média, Démarrage *de publicité* est l'appel Analytics envoyé au démarrage de la publicité, etc. *Les* appels Close sont les appels Analytics compilés envoyés directement depuis le serveur de pulsation vers le serveur d'analyse à la fin de la session multimédia, ou la fin de la publicité, du chapitre, etc. Les appels de fermeture ne sont pas disponibles dans les appels de paquets réseau.
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
>Ne modifiez pas les noms de classification pour les variables répertoriées ci-dessous, décrites sous la section Création de rapports/variable réservée sous la forme de « classification ».\
>Les classifications des médias sont définies lorsqu'une suite de rapports est activée pour le suivi multimédia. De temps à autres, Adobe ajoute de nouvelles propriétés et, dès lors, les clients doivent réactiver leurs suites de rapports pour accéder aux nouvelles propriétés du média. Lors du processus de mise à jour, Adobe détermine si les classifications sont activées en vérifiant les noms des variables. Si l'un d'eux est manquant, Adobe rajoute les autres.

## Données de publicité vidéo {#section_hq3_nbv_51b}

### Identifiant de publicité

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/>media.ad.id </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** Quelconque  </li> <li> **Exemple de valeur :**<br/> « 2125 » </li><li> **Description :**<br/>ID de la publicité. (Nombre entier et/ou combinaison de lettres)  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.na me) </li> <li> **Heartbeat :**<br/> (s : ressource : ad_ id) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À la fin de la VISITE </li> <li> **Nom du rapport :**<br/>Publicité </li> <li> **Données contextuelles :**<br/> (a.media.ad.na me) </li> <li> **Flux de données :**<br/>videoad </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.ad.name) </li> </ul> |



### Position de la publicité dans la capsule

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/>media.ad.podPosition </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 1 </li><li> **Description :**<br/>Position (index) de la publicité à l'intérieur de la coupure publicitaire parent. La première publicité comporte l’index 0, la deuxième publicité l’index 1, etc.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.po Dposition) </li> <li> **Heartbeat :**<br/> (s : ressource : pod_ position) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Position de la publicité dans la capsule </li> <li> **Données contextuelles :**<br/> (a.media.ad.po Dposition) </li> <li> **Flux de données :**<br/>videoadinpod </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.ad.podPosition) </li> </ul> |



### Longueur de la publicité

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/>media.ad.length </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** 1.5.1 </li> <li> **Exemple de valeur :**<br/> « 15 »  </li><li> **Description :**<br/>Durée de la publicité vidéo en secondes.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.le ngth) </li> <li> **Heartbeat :**<br/> (l : ressource : ad_ length) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar et classification </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Longueur de la publicité et Longueur de la publicité (variable) </li> <li> **Données contextuelles :**<br/> (a.media.ad.le ngth) </li> <li> **Flux de données :**<br/>videoadlength </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.ad.length) </li> </ul> |



### Nom du lecteur de publicités

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/>media.ad.playerName </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> « Roue libre » </li><li> **Description :**<br/>Nom du lecteur responsable du rendu de la publicité.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.pl Ayername) </li> <li> **Heartbeat :**<br/> (s : sp : player_ name) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Nom du lecteur de publicités </li> <li> **Données contextuelles :**<br/> (a.media.ad.pl Ayername) </li> <li> **Flux de données :**<br/>videoadplayername </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.ad.playerName) </li> </ul> |



### Nom de la coupure publicitaire

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/>media.ad.podFriendlyName </li> <li> **Obligatoire :**<br/> SDK : Oui ; API : Non. </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> « preroll » </li><li> **Description :**<br/>Nom convivial de la coupure publicitaire.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.po Dfriendlyname) </li> <li> **Heartbeat :**<br/> (s : ressource : pod_ name) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/>Nom de la capsule </li> <li> **Données contextuelles :**<br/> (a.media.ad.po Dfriendlyname) </li> <li> **Flux de données :**<br/>videoadpod </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.ad.podFriendlyName) </li> </ul> |



### Index de la coupure publicitaire

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/>media.ad.podPosition </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 1 </li><li> **Description :**<br/>Index de la coupure publicitaire à l'intérieur du contenu commençant à 1. Cette propriété est utilisée **uniquement** par le kit SDK Media pour générer l’identifiant de la capsule.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> </li> <li> **Heartbeat :**<br/> </li> </ul> | <ul> <li> **Disponible :**<br/>Non </li> <li> **Variable réservée :**<br/>S.O. </li> <li> **Nom du rapport :**<br/>S.O. </li> <li> **Données contextuelles :**<br/> </li> <li> **Flux de données :**<br/> </li> <li> **Audience Manager :**<br/> </li> </ul> |



### Position de la coupure publicitaire

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/>media.ad.podSecond </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 90 </li><li> **Description :**<br/>Décalage de la coupure publicitaire dans le contenu, en secondes.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.po Dsecond) </li> <li> **Heartbeat :**<br/> (l : ressource : pod_ offset) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/>Position de la capsule </li> <li> **Données contextuelles :**<br/> (a.media.ad.po Dsecond) </li> <li> **Flux de données :**<br/> </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.ad.podSecond) </li> </ul> |



### ID de coupure de publicité

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> c 4 a 577424 c 84067899 b 807 c 76722 d 495_ 1  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.po d) </li> <li> **Heartbeat :**<br/> (l : ressource : pod_ id) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Capsule publicitaire </li> <li> **Données contextuelles :**<br/> (a.media.ad.po d) </li> <li> **Flux de données :**<br/>videoadpod </li> <li> **Audience Manager :**<br/> </li> </ul> |



### Nom de la publicité

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/>media.ad.name </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** 1.5.1 </li> <li> **Exemple de valeur :**<br/> « Ford F -150 » </li><li> **Description :**<br/>Nom convivial de la publicité. Dans la création de rapports, « Nom de la publicité » est la classification et « Nom de la publicité (variable) » la variable eVar.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.fr Iendlyname) </li> <li> **Heartbeat :**<br/> (s : ressource : ad_ name) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar et classification </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Nom de la publicité et Nom de la publicité (variable) </li> <li> **Données contextuelles :**<br/> (a.media.ad.fr Iendlyname) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.ad.friendlyName) </li> </ul> |



## Métadonnées de publicité standard {#section_EFB805867916411E84DE1BA5A183D86A}

### Annonceur

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>ADVERTISER </li> <li> **Clé API :**<br/>media.ad.advertiser </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> </li><li> **Description :**<br/>Société/Marque dont le produit est présenté dans la publicité.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.ad vertiser) </li> <li> **Heartbeat :**<br/> (s : meta :<br/>a.media.ad.ad vertiser) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> <i>Annonceur </i> </li> <li> **Données contextuelles :**<br/> (a.media.ad.ad vertiser) </li> <li> **Flux de données :**<br/>videoadvertiser </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.ad.advertiser) </li> </ul> |



### ID de campagne

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>CAMPAIGN_ID </li> <li> **Clé API :**<br/>media.ad.campaignId </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> Entier ou nom (chaîne).  </li><li> **Description :**<br/>ID de la campagne publicitaire.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.ca mpaign) </li> <li> **Heartbeat :**<br/> (s : meta :<br/>a.media.ad.ca mpaign) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> <i>ID de campagne </i> </li> <li> **Données contextuelles :**<br/> (a.media.ad.ca mpaign) </li> <li> **Flux de données :**<br/>videocampaign </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.ad.campaign) </li> </ul> |



### ID d’élément créatif

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>CREATIVE_ID </li> <li> **Clé API :**<br/>media.ad.creativeId </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> Entier ou nom (chaîne).  </li><li> **Description :**<br/>ID de la publicité publicitaire.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.cr eative) </li> <li> **Heartbeat :**<br/> (s : meta :<br/>a.media.ad.cr eative) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> <i>ID d’élément créatif </i> </li> <li> **Données contextuelles :**<br/> (a.media.ad.cr eative) </li> <li> **Flux de données :**<br/>adclassificationcreative </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.ad.creative) </li> </ul> |



### ID du site

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>SITE_ID </li> <li> **Clé API :**<br/>media.ad.siteId </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> </li><li> **Description :**<br/>ID du site publicitaire.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.si te) </li> <li> **Heartbeat :**<br/> (s : meta :<br/>a.media.ad.si te) </li> </ul> | <ul> <li> **Disponible :**<br/> <i>Utiliser une règle de traitement personnalisée </i> </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> <i> </i> </li> <li> **Données contextuelles :**<br/> (a.media.ad.si te) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.ad.site) </li> </ul> |



### URL de l’élément créatif

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>CREATIVE_URL </li> <li> **Clé API :**<br/>media.ad.creativeURL </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> </li><li> **Description :**<br/>URL du créatif publicitaire.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.cr Eativeurl) </li> <li> **Heartbeat :**<br/> (s : meta :<br/>a.media.ad.cr Eativeurl) </li> </ul> | <ul> <li> **Disponible :**<br/> <i>Utiliser une règle de traitement personnalisée </i> </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> <i> </i> </li> <li> **Données contextuelles :**<br/> (a.media.ad.cr Eativeurl) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.ad.creativeURL) </li> </ul> |



### Identifiant de référencement

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>PLACEMENT_ID </li> <li> **Clé API :**<br/>media.ad.placementId </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de publicité, Fermeture de publicité </li> <li> **Min. Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> </li><li> **Description :**<br/>ID de placement de la publicité.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.pl acement) </li> <li> **Heartbeat :**<br/> (s : meta :<br/>a.media.ad.pl acement) </li> </ul> | <ul> <li> **Disponible :**<br/> <i>Utiliser une règle de traitement personnalisée </i> </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :** <br/> <i> </i> </li> <li> **Données contextuelles :**<br/> (a.media.ad.pl acement) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.ad.placement) </li> </ul> |




## Mesures publicitaires {#section_22AA1565F11C4F3990E2AB51CD3213F7}

### Démarrage de publicité

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de la publicité </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/>Nombre de démarrages de publicités vidéo.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.vi ew) </li> <li> **Heartbeat :**<br/> (s : event : type = start)<br/> (s : ressource : type = ad) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Démarrages de publicité </li> <li> **Flux de données :**<br/>videoadstart </li> <li> **Données contextuelles :**<br/> (a.media.ad.vi ew) </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.ad.view) </li> </ul> |



### Publicité terminée

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Fermeture de la publicité </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/>Nombre de publicités vidéo terminées.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.com plete) </li> <li> **Heartbeat :**<br/> (s : event : type = complete)<br/> (s : ressource : type = ad)  </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Fins de publicité </li> <li> **Flux de données :**<br/>videoadcomplete </li> <li> **Données contextuelles :**<br/> (a.media.ad.com plete) </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.ad.complete) </li> </ul> |



### passé sur la publicité

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Fermeture de la publicité </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 15 </li><li> **Description :**<br/>Durée totale, en secondes, passée à regarder la publicité (c.-à-d. le nombre de secondes lues). La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes.  <br/>**Date de publication : 13/09/18**  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.ti Meplayed) </li> <li> **Heartbeat :**<br/> </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Temps passé sur la publicité </li> <li> **Flux de données :**<br/>videoadtime </li> <li> **Données contextuelles :**<br/> (a.media.ad.ti Meplayed) </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a.media.ad.timePlayed) </li> </ul> |



## Related APIs {#section_Related_APIs}

### API createadobject :

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### API createadbreakobject :

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### API mediaheartbeatconfig :

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)

