---
title: 'Paramètres de publicité '
description: Découvrez les paramètres de publicité, y compris les variables d’implémentation, de réseau et de création de rapports pour les données de vidéo publicitaire.
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
exl-id: 949e86cb-d265-4836-8825-a06b87203b15
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '2036'
ht-degree: 89%

---

# Paramètres de publicité {#ad-parameters}

Cette rubrique présente une liste des données de publicité vidéo, y compris les valeurs de données contextuelles, qu’Adobe collecte via les variables de solution.

Description des données de tableau :

* **Mise en œuvre** : informations sur les valeurs et les exigences de mise en œuvre.
   * *Clé* : variable, définie soit manuellement dans votre application, soit automatiquement par le SDK Adobe Media.
   * *Obligatoire* : indique si le paramètre est requis pour le suivi vidéo de base.
   * *Type* : indique le type de variable à définir, chaîne ou nombre.
   * *Envoyé avec* : Indique le moment où les données sont envoyées : *Démarrage du média* est l’appel d’analyse envoyé au début du média, *Démarrage de la publicité* est l’appel d’analyse envoyé au début de la publicité, etc. *Fermer* est l’appel d’analyse compilé envoyé directement du serveur de pulsation au serveur d’analyse à la fin de la session multimédia ou de la publicité, du chapitre, etc. Les appels Fermer ne sont pas disponibles dans les appels de paquets réseau.
   * *Version minimum du SDK* : indique la version du SDK dont vous aurez besoin pour accéder au paramètre.
   * *Exemple de valeur* : fournit un exemple d’utilisation de variables courantes.
* **Paramètres réseau** : affiche les valeurs transmises aux serveurs Adobe Analytics ou Heartbeat. Cette colonne indique les noms des paramètres affichés dans les appels réseau générés par les SDK Adobe Media.
* **Reporting** : informations sur la manière de visualiser et d’analyser les données vidéo.
   * *Disponible* : indique si les données sont disponibles par défaut dans les rapports (*Oui*) ou nécessitent une configuration personnalisée (*Personnalisé*).
   * *Variable réservée* : indique si les données sont capturées sous la forme d’un événement, d’une eVar, d’une prop ou d’une classification dans une variable réservée.
   * *Nom du rapport* : nom du rapport Adobe Analytics pour la variable.
   * *Données contextuelles* : nom des données contextuelles Adobe Analytics transmises au serveur de reporting et utilisées dans les règles de traitement.
   * *Flux de données* : nom de colonne de la variable trouvée dans les flux de données du parcours de navigation ou du flux de données en direct.
   * *Audience Manager* : nom de caractéristique trouvé dans Adobe Audience Manager.

>[!IMPORTANT]
>
>Ne modifiez pas les noms de classification des variables répertoriées ci-dessous qui sont
>&#x200B;>décrits sous Variable de création de rapports/réservée comme « classification ».
>&#x200B;>Les classifications des médias sont définies lorsqu’une suite de rapports est activée pour les médias.
>&#x200B;>Suivi. De temps à autre, Adobe ajoute de nouvelles propriétés et, dans ce cas,
>&#x200B;>les clients doivent réactiver leurs suites de rapports pour accéder aux nouvelles propriétés
>&#x200B;>du média. Au cours du processus de mise à jour, Adobe détermine si les
>&#x200B;>classifications sont activées en vérifiant les noms des variables. Si l’un d’eux manque,
>&#x200B;>Adobe l’ajoute à nouveau.

## Données de publicité vidéo {#ad-video-data}

### Identifiant de publicité

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clé SDK :**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/> media.ad.id </li> <li> **Obligatoire :**<br/> Oui </li> <li> **Type :**<br/> Chaîne </li> <li> **Envoyé avec :**<br/> Démarrage de publicité, Fermeture de publicité </li> <li> **Version Version SDK min. :** Quelconque  </li> <li> **Exemple de valeur :**<br/> « 2125 » </li><li> **Description :**<br/> identifiant de la publicité. (Nombre entier et/ou combinaison de lettres)  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.<br/>name) </li> <li> **Heartbeat :**<br/> (<code>s:asset:ad_id</code>) </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> eVar </li> <li> **Expiration :**<br/>&#x200B;À la fin de la VISITE </li> <li> **Nom du rapport :**<br/> Publicité </li> <li> **Données contextuelles :**<br/> (a.media.ad.<br/>name) </li> <li> **Flux de données :**<br/> videoad </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.ad.name) </li> <li> **Chemin d’accès du champ XDM :** (obsolète)<br/> advertising.adAssetReference._id </li> <li> **Chemin d’accès du champ XDM de collection :**<br/> mediaCollection.advertisingDetails.name </li> <li> **Chemin d’accès du champ XDM de création de rapports :**<br/> mediaReporting.advertisingDetails.name </li> </ul> |



### Position de la publicité dans la capsule

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clé SDK :**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/> media.ad.podPosition </li> <li> **Obligatoire :**<br/> Oui </li> <li> **Type :**<br/> Nombre </li> <li> **Envoyé avec :**<br/> Démarrage de publicité, Fermeture de publicité </li> <li> **Version Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 1 </li><li> **Description :**<br/> Position (index) de la publicité dans la coupure publicitaire parente. La première publicité comporte l’index 0, la deuxième publicité l’index 1, etc.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Heartbeat:**<br/> (<code>s:asset:pod_position</code>) </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> eVar </li> <li> **Expiration :**<br/>&#x200B;À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Position de la publicité dans la capsule </li> <li> **Données contextuelles :**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Flux de données :**<br/> videoadinpod </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.ad.podPosition) </li> <li> **Chemin d’accès du champ XDM :** (obsolète)<br/> advertising.adAssetViewDetails.index </li> <li> **Chemin d’accès du champ XDM de collection :**<br/> mediaCollection.advertisingDetails.podPosition </li> <li> **Chemin d’accès du champ XDM de création de rapports :**<br/> mediaReporting.advertisingDetails.podPosition </li> </ul> |



### Longueur de la publicité

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clé SDK :**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/> media.ad.length </li> <li> **Obligatoire :**<br/> Oui </li> <li> **Type :**<br/> Nombre </li> <li> **Envoyé avec :**<br/> Démarrage de publicité, Fermeture de publicité </li> <li> **Version Version SDK min. :** 1.5.1 </li> <li> **Exemple de valeur :**<br/> « 15 »  </li><li> **Description :**<br/> longueur de la publicité vidéo en secondes.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.<br/>length) </li> <li> **Heartbeat :**<br/> (<code>l:asset:ad_length</code>) </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> eVar et classification </li> <li> **Expiration :**<br/>&#x200B;À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Longueur de la publicité et Longueur de la publicité (variable) </li> <li> **Données contextuelles :**<br/> (a.media.ad.<br/>length) </li> <li> **Flux de données :**<br/> videoadlength </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.ad.length) </li> <li> **Chemin d’accès du champ XDM :** (obsolète)<br/> advertising.adAssetReference.<br/>_xmpDM.duration </li> <li> **Chemin d’accès au champ XDM de la collection :**<br/> mediaCollection.advertisingDetails.length </li> <li> **Chemin d’accès au champ XDM de la création de rapports :**<br/> mediaReporting.advertisingDetails.length </li> </ul> |



### Nom du lecteur de publicités

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clé SDK :**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/> media.ad.playerName </li> <li> **Obligatoire :**<br/> Oui </li> <li> **Type :**<br/> Chaîne </li> <li> **Envoyé avec :**<br/> Démarrage de publicité, Fermeture de publicité </li> <li> **Version Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> « Freewheel » </li><li> **Description :**<br/> nom du lecteur responsable du rendu de la publicité.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.<br/>playerName) </li> <li> **Heartbeat:**<br/> (<code>s:sp:player_name</code>) </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> eVar </li> <li> **Expiration :**<br/>&#x200B;À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Nom du lecteur de publicités </li> <li> **Données contextuelles :**<br/> (a.media.ad.<br/>playerName) </li> <li> **Flux de données :**<br/> videoadplayername </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.ad.playerName) </li> <li> **Chemin d’accès du champ XDM :** (obsolète)<br/> advertising.adAssetViewDetails.playerName </li> <li> **Chemin d’accès au cahmp XDM de la collection :**<br/> mediaCollection.advertisingDetails.<br/>playerName </li> <li> **Chemin d’accès au champ XDM de la création de rapports :**<br/> mediaReporting.advertisingDetails.<br/>playerName </li> </ul> |



### Nom de la coupure publicitaire

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clé SDK :**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/> media.ad.podFriendlyName </li> <li> **Obligatoire :**<br/> SDK : Oui ; API : Non. </li> <li> **Type :**<br/> Chaîne </li> <li> **Envoyé avec :**<br/> Démarrage de publicité, Fermeture de publicité </li> <li> **Version Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> « pre-roll » </li><li> **Description :**<br/> nom convivial de la coupure publicitaire.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Heartbeat:**<br/> (<code>s:asset:pod_name</code>) </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> Classification </li> <li> **Nom du rapport :**<br/> Nom de la capsule </li> <li> **Données contextuelles :**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Flux de données :**<br/> S.O. </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.ad.podFriendlyName) </li> <li> **Chemin d’accès du champ XDM :** (obsolète)<br/> advertising.adAssetViewDetails.<br/>adBreak._dc.title </li> <li> **Chemin d’accès du champ XDM de collection :**<br/> mediaCollection.advertisingPodDetails.<br/>friendlyName </li> <li> **Chemin d’accès du champ XDM de création de rapports :**<br/> mediaReporting.advertisingPodDetails.<br/>friendlyName </li> </ul> |



### Index de la coupure publicitaire

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clé SDK :**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/> media.ad.podIndex </li> <li> **Obligatoire :**<br/> Oui </li> <li> **Type :**<br/> Nombre </li> <li> **Envoyé avec :**<br/> </li> <li> **Version Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 1 </li><li> **Description :**<br/> index de la coupure publicitaire dans le contenu commençant à 1. Cette propriété est utilisée **uniquement** par le SDK Media pour générer l’identifiant de la capsule.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> </li> <li> **Heartbeat :**<br/> </li> </ul> | <ul> <li> **Disponible :**<br/> Non </li> <li> **Variable réservée :**<br/> S.O. </li> <li> **Nom du rapport :**<br/> S.O. </li> <li> **Données contextuelles :**<br/> </li> <li> **Flux de données :**<br/> S.O. </li> <li> **Audience Manager :**<br/> </li> <li> **Chemin d’accès du champ XDM :** (obsolète)<br/> advertising.adAssetViewDetails.index </li> <li> **Chemin d’accès du champ XDM de collection :**<br/> mediaCollection.advertisingPodDetails.index </li> </ul> |



### Position de la coupure publicitaire

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clé SDK :**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/> media.ad.podSecond </li> <li> **Obligatoire :**<br/> Oui </li> <li> **Type :**<br/> Nombre </li> <li> **Envoyé avec :**<br/> Démarrage de publicité, Fermeture de publicité </li> <li> **Version Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 90 </li><li> **Description :**<br/> décalage de la coupure publicitaire dans le contenu, en secondes.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Heartbeat :**<br/> (<code>l:asset:pod_offset</code>) </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> Classification </li> <li> **Nom du rapport :**<br/> Position de la capsule </li> <li> **Données contextuelles :**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Flux de données :**<br/> S.O. </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.ad.podSecond) </li> <li> **Chemin d’accès du champ XDM :** (obsolète)<br/> advertising.adAssetViewDetails.adBreak.<br/>offset </li> <li> **Chemin d’accès du champ XDM de collection :**<br/> mediaCollection.advertisingPodDetails.<br/>offset </li> <li> **Chemin d’accès du champ XDM de création de rapports :**<br/> mediaReporting.advertisingPodDetails.<br/>offset </li> </ul> |



### ID de coupure de publicité

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Oui </li> <li> **Type :**<br/> Chaîne </li> <li> **Envoyé avec :**<br/> Démarrage de publicité, Fermeture de publicité </li> <li> **Version Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.<br/>pod) </li> <li> **Heartbeat:**<br/> (<code>s:asset:pod_id</code>) </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> eVar </li> <li> **Expiration :**<br/>&#x200B;À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Capsule publicitaire </li> <li> **Données contextuelles :**<br/> (a.media.ad.<br/>pod) </li> <li> **Flux de données :**<br/> videoadpod </li> <li> **Audience Manager :**<br/> </li> <li> **Chemin d’accès du champ XDM :** (obsolète)<br/> advertising.adAssetViewDetails.adBreak._id </li> <li> **Chemin d’accès du champ XDM de création de rapports :**<br/> mediaReporting.advertisingPodDetails.<br/>ID </li> </ul> |



### Nom de la publicité

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clé SDK :**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Clé API :**<br/> media.ad.name </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> Chaîne </li> <li> **Envoyé avec :**<br/> Démarrage de publicité, Fermeture de publicité </li> <li> **Version Version SDK min. :** 1.5.1 </li> <li> **Exemple de valeur :**<br/> « Ford F-150 » </li><li> **Description :**<br/> nom convivial de la publicité.  Dans la création de rapports, « Nom de la publicité » est la classification et « Nom de la publicité (variable) » la variable eVar.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **Heartbeat:**<br/> (<code>s:asset:ad_name</code>) </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> eVar et classification </li> <li> **Expiration :**<br/>&#x200B;À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Nom de la publicité et Nom de la publicité (variable) </li> <li> **Données contextuelles :**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **Flux de données : nomvidéo**<br/> </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.ad.friendlyName) </li> <li> **Chemin d’accès du champ XDM :** (obsolète)<br/> advertising.adAssetReference._dc.title </li> <li> **Chemin d’accès du champ XDM de collection :**<br/> mediaCollection.advertisingDetails.friendlyName </li> <li> **Chemin d’accès du champ XDM de création de rapports :**<br/> mediaReporting.advertisingDetails.friendlyName </li> </ul> |



## Métadonnées de publicité standard {#standard-ad-metadata}

### Annonceur

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clé SDK :**<br/> ADVERTISER </li> <li> **Clé API :**<br/> media.ad.advertiser </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> Chaîne </li> <li> **Envoyé avec :**<br/> Démarrage de publicité, Fermeture de publicité </li> <li> **Version Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> </li><li> **Description :**<br/> entreprise ou marque dont le produit apparaît dans la publicité.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.<br/>advertiser) </li> <li> **Heartbeat :**<br/> (<code>s:meta:</code><br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> eVar </li> <li> **Expiration :**<br/>&#x200B;À l’ACCÈS </li> <li> **Nom du rapport :**<br/> <i>Annonceur </i> </li> <li> **Données contextuelles :**<br/> (a.media.ad.<br/>advertiser) </li> <li> **Flux de données :**<br/> videoadadvertiser </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.ad.advertiser) </li> <li> **Chemin d’accès du champ XDM :** (obsolète)<br/> advertising.adAssetReference.advertiser </li> <li> **Chemin d’accès du champ XDM de collection :**<br/> mediaCollection.advertisingDetails.advertiser </li> <li> **Chemin d’accès du champ XDM de création de rapports :**<br/> mediaReporting.advertisingDetails.advertiser </li> </ul> |



### ID de campagne

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clé SDK :**<br/> CAMPAIGN_ID </li> <li> **Clé API :**<br/> media.ad.campaignId </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> Chaîne </li> <li> **Envoyé avec :**<br/> Démarrage de publicité, Fermeture de publicité </li> <li> **Version Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> Nombre entier ou nom (chaîne).  </li><li> **Description :**<br/> ID de la campagne publicitaire.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.<br/>campaign) </li> <li> **Heartbeat :**<br/> (<code>s:meta:</code><br/>a.media.ad.campaign) </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> eVar </li> <li> **Expiration :**<br/>&#x200B;À l’ACCÈS </li> <li> **Nom du rapport :**<br/> <i>ID de campagne </i> </li> <li> **Données contextuelles :**<br/> (a.media.ad.<br/>campaign) </li> <li> **Flux de données :**<br/> videoadcampaign </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.ad.campaign) </li> <li> **Chemin d’accès du champ XDM :** (obsolète)<br/> advertising.adAssetReference.campaign </li> <li> **Chemin d’accès du champ XDM de collection :**<br/> mediaCollection.advertisingDetails.<br/>campaignID </li> <li> **Chemin d’accès du champ XDM de création de rapports :**<br/> mediaReporting.advertisingDetails.<br/>campaignID </li> </ul> |



### ID d’élément créatif

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clé SDK :**<br/> CREATIVE_ID </li> <li> **Clé API :**<br/> media.ad.creativeId </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> Chaîne </li> <li> **Envoyé avec :**<br/> Démarrage de publicité, Fermeture de publicité </li> <li> **Version Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> Nombre entier ou nom (chaîne).  </li><li> **Description :**<br/> ID de l’élément créatif publicitaire.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.<br/>creative) </li> <li> **Heartbeat :**<br/> (<code>s:meta:</code><br/>a.media.ad.creative) </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> eVar </li> <li> **Expiration :**<br/>&#x200B;À l’ACCÈS </li> <li> **Nom du rapport :**<br/> <i>ID d’élément créatif </i> </li> <li> **Données contextuelles :**<br/> (a.media.ad.<br/>creative) </li> <li> **Flux de données :**<br/> adclassificationcreative </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.ad.creative) </li> <li> **Chemin d’accès du champ XDM :** (obsolète)<br/> advertising.adAssetReference.creativeID </li> <li> **Chemin d’accès du champ XDM de collection :**<br/> mediaCollection.advertisingDetails.creativeID </li> <li> **Chemin d’accès du champ XDM de création de rapports :**<br/> mediaReporting.advertisingDetails.creativeID </li> </ul> |



### ID du site

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clé SDK :**<br/> SITE_ID </li> <li> **Clé API :**<br/> media.ad.siteId </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> Chaîne </li> <li> **Envoyé avec :**<br/> Démarrage de publicité, Fermeture de publicité </li> <li> **Version Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> </li><li> **Description :**<br/> ID du site de la publicité.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.<br/>site) </li> <li> **Heartbeat :**<br/> (<code>s:meta:</code><br/>a.media.ad.site) </li> </ul> | <ul> <li> **Disponible :**<br/> <i>Utiliser la règle de traitement personnalisée </i> </li> <li> **Variable réservée :**<br/> eVar </li> <li> **Expiration :**<br/>&#x200B;À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Personnalisé </li> <li> **Données contextuelles :**<br/> (a.media.ad.<br/>site) </li> <li> **Flux de données :**<br/> S.O. </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.ad.site) </li> <li> **Chemin d’accès du champ XDM :** (obsolète)<br/> advertising.adAssetReference.siteID </li> <li> **Chemin d’accès au champ XDM de la collection :**<br/> mediaCollection.advertisingDetails.siteID </li> <li> **Chemin d’accès au champ XDM de la création de rapports :**<br/> mediaReporting.advertisingDetails.siteID </li> </ul> |



### URL de l’élément créatif

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clé SDK :**<br/> CREATIVE_URL </li> <li> **Clé API :**<br/> media.ad.creativeURL </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> Chaîne </li> <li> **Envoyé avec :**<br/> Démarrage de publicité, Fermeture de publicité </li> <li> **Version Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> </li><li> **Description :**<br/> URL de l’élément créatif publicitaire.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Heartbeat:**<br/> (<code>s:meta:&lt;c/ode><br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **Disponible :**<br/> <i>Utiliser la règle de traitement personnalisée </i> </li> <li> **Variable réservée :**<br/> eVar </li> <li> **Expiration :**<br/>&#x200B;À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Personnalisé </li> <li> **Données contextuelles :**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Flux de données :**<br/> S.O. </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.ad.creativeURL) </li> <li> **Chemin d’accès du champ XDM :** (obsolète)<br/> advertising.adAssetReference.creativeURL </li> <li> **Chemin d’accès au champ XDM de la collection :**<br/> mediaCollection.advertisingDetails.<br/>creativeURL </li> <li> **Chemin d’accès au champ XDM de la création de rapports :**<br/> mediaReporting.advertisingDetails.<br/>creativeURL </li> </ul> |



### Identifiant de référencement

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clé SDK :**<br/> PLACEMENT_ID </li> <li> **Clé API :**<br/> media.ad.placementId </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> Chaîne </li> <li> **Envoyé avec :**<br/> Démarrage de publicité, Fermeture de publicité </li> <li> **Version Version SDK min. :** 1.5.7 </li> <li> **Exemple de valeur :**<br/> </li><li> **Description :**<br/> identifiant de référencement de la publicité.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.<br/>placement) </li> <li> **Heartbeat :**<br/> (<code>s:meta:</code><br/>a.media.ad.placement) </li> </ul> | <ul> <li> **Disponible :**<br/> <i>Utiliser la règle de traitement personnalisée </i> </li> <li> **Variable réservée :**<br/> eVar </li> <li> **Expiration :**<br/>&#x200B;À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Personnalisé </li> <li> **Données contextuelles :**<br/> (a.media.ad.<br/>placement) </li> <li> **Flux de données :**<br/> S.O. </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.ad.placement) </li> <li> **Chemin d’accès du champ XDM :** (obsolète)<br/> advertising.adAssetReference.placementID </li> <li> **Chemin d’accès du champ XDM de collection :**<br/> mediaCollection.advertisingDetails.<br/>placementID </li> <li> **Chemin d’accès du champ XDM de création de rapports :**<br/> mediaReporting.advertisingDetails.<br/>placementID </li> </ul> |




## Mesures publicitaires {#ad-metrics}

### Démarrage de publicité

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Oui </li> <li> **Type :**<br/> Chaîne </li> <li> **Envoyé avec :**<br/> Démarrage de la publicité </li> <li> **Version Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/> nombre de démarrages de publicité vidéo.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.<br/>view) </li> <li> **Heartbeat:**<br/> (<code>s:event:type=start</code>)<br/> (<code>s:asset:type=ad<code>) </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Démarrages de publicité </li> <li> **Flux de données :**<br/> videoadstart </li> <li> **Données contextuelles :**<br/> (a.media.ad.<br/>view) </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.ad.view) </li> <li> **Chemin d’accès du champ XDM :** (obsolète)<br/> advertising.impressions.value > 0 => « TRUE » </li> <li> **Chemin d’accès du champ XDM de création de rapports :**<br/> mediaReporting.advertisingDetails.isStarted </li> </ul> |



### Publicité terminée

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Oui </li> <li> **Type :**<br/> Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture de la publicité </li> <li> **Version Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/> nombre de publicités vidéo terminées.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.<br/>complete) </li> <li> **Heartbeat:**<br/> (<code>s:event:type=complete</code>)<br/> (<code>s:asset:type=ad</code>)  </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Fins de publicité </li> <li> **Flux de données :**<br/> videoadcomplete </li> <li> **Données contextuelles :**<br/> (a.media.ad.<br/>complete) </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.ad.complete) </li> <li> **Chemin d’accès du champ XDM :** (obsolète)<br/> advertising.completes.value > 0 => « TRUE » </li> <li> **Chemin d’accès du champ XDM de création de rapports :**<br/> mediaReporting.advertisingDetails.<br/>isCompleted </li> </ul> |



### Passé sur la publicité

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Oui </li> <li> **Type :**<br/> Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture de la publicité </li> <li> **Version Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 15 </li><li> **Description :**<br/> le temps total, en secondes, passé à regarder la publicité (c.-à-d., le nombre de secondes lues).  La valeur s’affiche au format horaire (<code>HH:MM:SS</code>) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes.  <br/>**Date de publication : 13/09/18**  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Heartbeat :**<br/> </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Temps passé sur la publicité </li> <li> **Flux de données :**<br/> videoadtime </li> <li> **Données contextuelles :**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.ad.timePlayed) </li> <li> **Chemin d’accès du champ XDM :** (obsolète)<br/> advertising.timePlayed.value </li> <li> **Chemin d’accès du champ XDM de création de rapports :**<br/> mediaReporting.advertisingDetails.<br/>timePlayed </li> </ul> |



## API connexes {#section_Related_APIs}

### API createAdObject :

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### API createAdBreakObject :

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### API MediaHeartbeatConfig :

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)
