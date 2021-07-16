---
title: Paramètres d’état du lecteur
description: « Découvrez les paramètres de suivi de lʼétat du lecteur pour les propriétés plein écran, sous-titres, muet et incrustation dʼimage. »
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: cd51ed3a-fe37-41e9-8243-dfd9deb514c1
feature: « Media Analytics, Variables »
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '2249'
ht-degree: 100%

---

# Paramètres d’état du lecteur{#player-state-parameters}

Cette rubrique présente une liste de données concernant l’état du lecteur collectées par Adobe au moyen de variables de solution.

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
>Ne modifiez pas les noms de classification des variables répertoriées ci-dessous, qui sont décrites sous Variable de création de rapports/réservée comme « classification ».\
>Les classifications des médias sont définies lorsqu’une suite de rapports est activée pour le suivi multimédia. De temps à autre, Adobe ajoute de nouvelles propriétés. Dans ce cas, les clients doivent réactiver leurs suites de rapports pour accéder aux nouvelles propriétés du média. Au cours du processus de mise à jour, Adobe détermine si les classifications sont activées en vérifiant les noms des variables. Si l’un d’eux manque, Adobe l’ajoute à nouveau.

## Propriétés de l’état du lecteur {#player-state-properties}

Les capacités de suivi de l’état du lecteur peuvent être associées à un flux audio ou vidéo. Les mesures de suivi standard de l’état du lecteur sont stockées en tant que variables de solution. Les états standard sont les suivants : fullScreen, mute, closeCaption, pictureInPicture et inFocus.

### Propriétés du plein écran

#### Diffusions affectées par le plein écran

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement  </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Version SDK min.**<br/> 3.0</li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/> Le nombre de diffusions affectées par le plein écran. Cette mesure est définie sur 1 uniquement si au moins un passage en plein écran s’est produit au cours de la session de lecture. <br/> **Important :**<br/> Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> a.media.states.fullscreen.set<br/></li> <li> **Heartbeat :**<br/> S.O. </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Diffusions affectées par le plein écran </li> <li> **Données contextuelles :**<br/> a.media.states.fullscreen.set<br/> </li> <li> **Flux de données :**<br/> videostatefullscreen </li> <li> **Audience Manager :**<br/> c_contextdata.a.media.states.fullscreen.set </li> </ul> |

#### Nombre de plein écrans

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement  </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Version SDK min.**<br/> 3.0</li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/> Le nombre de passages en plein écran. Cette mesure est définie sur 1 uniquement si au moins un passage en plein écran s’est produit au cours de la session de lecture. <br/> **Important :**<br/> Si cet événement est défini, le nombre est égal au nombre de fois où la vidéo est passée en plein écran. Si cet événement n’est pas défini, aucune valeur n’est envoyée.</li> </ul> | <ul> <li> **Adobe Analytics :**<br/> a.media.states.fullscreen.count<br/></li> <li> **Heartbeat :**<br/> S.O. </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Nombre de plein écrans </li> <li> **Données contextuelles :**<br/> a.media.states.fullscreen.count<br/> </li> <li> **Flux de données :**<br/> videostatefullscreencount </li> <li> **Audience Manager :**<br/> c_contextdata.media.states.fullscreen.count </li> </ul> |



#### Durée totale en plein écran

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement  </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Version SDK min.**<br/> 3.0</li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/> La durée du passage en plein écran. Cette mesure est définie sur 1 uniquement si au moins un passage en plein écran s’est produit au cours de la session de lecture. <br/> **Important :**<br/> Si cet événement est défini, la durée correspond à la durée pendant laquelle la vidéo se trouvait en plein écran. Si cet événement n’est pas défini, aucune valeur n’est envoyée.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> a.media.states.fullscreen.time<br/></li> <li> **Heartbeat :**<br/> S.O. </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Durée totale du plein écran </li> <li> **Données contextuelles :**<br/> a.media.states.fullscreen.time<br/> </li> <li> **Flux de données :**<br/> videostatefullscreentime </li> <li> **Audience Manager :**<br/> c_contextdata.media.states.fullscreen.time </li> </ul> |


### Propriétés du sous-titrage codé

#### Diffusions affectées par le sous-titrage codé

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement  </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Version SDK min.**<br/> 3.0</li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/> Le nombre de diffusions affectées par le sous-titrage codé. Cette mesure est définie sur 1 uniquement si au moins un affichage du sous-titrage codé s’est produit au cours de la session de lecture. <br/> **Important :**<br/> Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> a.media.states.closedcaptioning.set<br/></li> <li> **Heartbeat :**<br/> S.O. </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Diffusions affectées par le sous-titrage codé </li> <li> **Données contextuelles :**<br/> a.media.states.closedcaptioning.set<br/> </li> <li> **Flux de données :**<br/> videostateclosedcaptioning </li> <li> **Audience Manager :**<br/> c_contextdata.a.media.states.closedcaptioning.set </li> </ul> |


#### Nombre de sous-titrages codés

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement  </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Version SDK min.**<br/> 3.0</li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/> Le nombre d’affichages du sous-titrage codé. Cette mesure est définie sur 1 uniquement si au moins un affichage du sous-titrage codé s’est produit au cours de la session de lecture. <br/> **Important :**<br/> Si cet événement est défini, le nombre est égal au nombre de fois où le sous-titrage codé a été affiché. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.closedcaptioning.count<br/></li> <li> **Heartbeat :**<br/> S.O. </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Nombre de sous-titrages codés </li> <li> **Données contextuelles :**<br/> a.media.states.closedcaptioning.count<br/> </li> <li> **Flux de données :**<br/> videostateclosedcaptioningcount </li> <li> **Audience Manager :**<br/> c_contextdata.media.states.closedcaptioning.count </li> </ul> |


#### Durée totale du sous-titrage codé

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement  </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Version SDK min.**<br/> 3.0</li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/> La durée de l’affichage du sous-titrage codé. Cette mesure est définie sur 1 uniquement si au moins un passage en plein écran s’est produit au cours de la session de lecture. <br/> **Important :**<br/> Si cet événement est défini, la durée est égale à la durée pendant laquelle le sous-titrage codé a été affiché. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> a.media.states.closedcaptioning.time<br/></li> <li> **Heartbeat :**<br/> S.O. </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Durée totale du sous-titrage codé </li> <li> **Données contextuelles :**<br/> a.media.states.closedcaptioning.time<br/> </li> <li> **Flux de données :**<br/> videostateclosedcaptioningtime </li> <li> **Audience Manager :**<br/> c_contextdata.media.states.closedcaptioning.time </li> </ul> |


### Propriétés du mode muet

#### Diffusions affectées par le mode muet

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement  </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Version SDK min.**<br/> 3.0</li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/> Le nombre de diffusions affectées par le mode muet. Cette mesure est définie sur 1 uniquement si au moins un passage en mode muet s’est produit au cours de la session de lecture. <br/> **Important :**<br/> Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> a.media.states.mute.set<br/></li> <li> **Heartbeat :**<br/> S.O. </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Diffusions affectées par le mode muet </li> <li> **Données contextuelles :**<br/> a.media.states.mute.set<br/> </li> <li> **Flux de données :**<br/> videostatemute </li> <li> **Audience Manager :**<br/> c_contextdata.a.media.states.mute.set </li> </ul> |

#### Nombre d’instances muettes

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement  </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Version SDK min.**<br/> 3.0</li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/> Le nombre de passages en mode muet. Cette mesure est définie sur 1 uniquement si au moins un passage en mode muet s’est produit au cours de la session de lecture. <br/> **Important :**<br/> Si cet événement est défini, le nombre est égal au nombre de passages en mode muet. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> a.media.states.mute.count<br/></li> <li> **Heartbeat :**<br/> S.O. </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Nombre d’instances muettes </li> <li> **Données contextuelles :**<br/> a.media.states.mute.count<br/> </li> <li> **Flux de données :**<br/> videostatemutecount </li> <li> **Audience Manager :**<br/> c_contextdata.media.states.mute.count </li> </ul> |

#### Durée totale du mode muet

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement  </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Version SDK min.**<br/> 3.0</li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/> La durée du passage en mode muet. Cette mesure est définie sur 1 uniquement si au moins un passage en mode muet s’est produit au cours de la session de lecture. <br/> **Important :**<br/> Si cet événement est défini, la durée est égale à la durée du passage en mode muet. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> a.media.states.mute.time<br/></li> <li> **Heartbeat :**<br/> S.O. </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Durée totale du mode muet </li> <li> **Données contextuelles :**<br/> a.media.states.mute.time<br/> </li> <li> **Flux de données :**<br/> videostatemutetime </li> <li> **Audience Manager :**<br/> c_contextdata.media.states.mute.time </li> </ul> |


### Propriétés du mode « Image dans l’Image »


#### Diffusions affectées par le mode « Image dans l’Image »

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement  </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Version SDK min.**<br/> 3.0</li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/> Le nombre de diffusions affectées par le mode « Image dans l’Image ». Cette mesure est définie sur 1 uniquement si au moins un passage en mode « Image dans l’Image » s’est produit au cours de la session de lecture. <br/> **Important :**<br/> Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> a.media.states.pictureinpicture.set<br/></li> <li> **Heartbeat :**<br/> S.O. </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Diffusions affectées par le mode « Image dans l’Image » </li> <li> **Données contextuelles :**<br/> a.media.states.pictureinpicture.set<br/> </li> <li> **Flux de données :**<br/> videostatepictureinpicture </li> <li> **Audience Manager :**<br/> c_contextdata.a.media.states.pictureinpicture.set </li> </ul> |


#### Nombre d’instances en mode « Image dans l’Image »

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement  </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Version SDK min.**<br/> 3.0</li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/> Le nombre de passages en mode « Image dans l’Image ». Cette mesure est définie sur 1 uniquement si au moins un passage en mode « Image dans l’Image » s’est produit au cours de la session de lecture. <br/> **Important :** <br/> Si cet événement est défini, le nombre est égal au nombre de passages en mode « Image dans l’Image ». Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> a.media.states.pictureinpicture.count<br/></li> <li> **Heartbeat :**<br/> S.O. </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Nombre d’instances en mode « Image dans l’Image » </li> <li> **Données contextuelles :**<br/> a.media.states.pictureinpicture.count<br/> </li> <li> **Flux de données :**<br/> videostatepictureinpicturecount </li> <li> **Audience Manager :**<br/> c_contextdata.a.media.states.pictureinpicture.count </li> </ul> |


#### Durée totale du mode « Image dans l’Image »

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement  </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Version SDK min.**<br/> 3.0</li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/> La durée du passage en mode « Image dans l’Image ». Cette mesure est définie sur 1 uniquement si au moins un passage en mode « Image dans l’Image » s’est produit au cours de la session de lecture. <br/> **Important :** <br/> Si cet événement est défini, la durée est égale à la durée du passage en mode « Image dans l’Image ». Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> a.media.states.pictureinpicture.time<br/></li> <li> **Heartbeat :**<br/> S.O. </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Durée totale du mode « Image dans l’Image » </li> <li> **Données contextuelles :**<br/> a.media.states.pictureinpicture.time<br/> </li> <li> **Flux de données :**<br/> videostatepictureinpicturetime </li> <li> **Audience Manager :**<br/> c_contextdata.media.states.pictureinpicture.time </li> </ul> |


### Propriétés du mode « En point de mires »

#### Diffusions affectées par le mode « En point de mires »

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement  </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Version SDK min.**<br/> 3.0</li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/> Le nombre de diffusions affectées par le mode « En point de mires ». Cette mesure est définie sur 1 uniquement si au moins un passage en mode « En point de mires » s’est produit au cours de la session de lecture. <br/> **Important :**<br/> Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> a.media.states.infocus.set<br/></li> <li> **Heartbeat :**<br/> S.O. </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Diffusions affectées par le mode « En point de mires » </li> <li> **Données contextuelles :**<br/> a.media.states.infocus.set<br/> </li> <li> **Flux de données :**<br/> videostateinfocus </li> <li> **Audience Manager :**<br/> c_contextdata.a.media.states.infocus.set </li> </ul> |


#### Nombre d’instances en mode « En point de mires »

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement  </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Version SDK min.**<br/> 3.0</li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/> Le nombre de passages en mode « En point de mires ». Cette mesure est définie sur 1 uniquement si au moins un passage en mode « En point de mires » s’est produit au cours de la session de lecture. <br/> **Important :**<br/> Si cet événement est défini, le nombre est égal au nombre de passages en mode « En point de mires ». Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> a.media.states.infocus.count<br/></li> <li> **Heartbeat :**<br/> S.O. </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Nombre d’instances en mode « En point de mires » </li> <li> **Données contextuelles :**<br/> a.media.states.infocus.count<br/> </li> <li> **Flux de données :**<br/> videostateinfocuscount </li> <li> **Audience Manager :**<br/> c_contextdata.media.states.infocus.count </li> </ul> |


#### Durée totale du mode « En point de mires »

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement  </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Version SDK min.**<br/> 3.0</li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/> La durée du passage en mode « En point de mires ». Cette mesure est définie sur 1 uniquement si au moins un passage en mode « En point de mires » s’est produit au cours de la session de lecture. <br/> **Important :** <br/> Si cet événement est défini, la durée est égale à la durée du passage en Mode « En point de mires ». Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> a.media.states.infocus.time<br/></li> <li> **Heartbeat :**<br/> S.O. </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Durée totale du mode « En point de mires » </li> <li> **Données contextuelles :**<br/> a.media.states.infocus.time<br/> </li> <li> **Flux de données :**<br/> videostateinfocustime </li> <li> **Audience Manager :**<br/> c_contextdata.media.states.infocus.time </li> </ul> |

## Liste de propriétés des identités XDM

Les données stockées dans Analytics peuvent être utilisées à n’importe quelle fin, et les mesures d’état du lecteur peuvent être importées dans Adobe Experience Platform à l’aide de XDM et utilisées avec Customer Journey Analytics.

| Propriété de l’état du lecteur | Mappage |
|---------------------------------------|------------------------------------|
| a.media.states.fullScreen.set | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateSet |
| a.media.states.fullScreen.count | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateCount |
| a.media.states.fullScreen.time | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateTime |
| a.media.states.mute.set | media.mediaTimed.primaryAssetViewDetails.mute.playerStateSet |
| a.media.states.mute.count | media.mediaTimed.primaryAssetViewDetails.mute.playerStateCount |
| a.media.states.mute.time | media.mediaTimed.primaryAssetViewDetails.mute.playerStateTime |
| a.media.states.closeCaption.set | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateSet |
| a.media.states.closeCaption.count | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateCount |
| a.media.states.closeCaption.time | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateTime |
| a.media.states.pictureInPicture.set | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateSet |
| a.media.states.pictureInPicture.count | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateCount |
| a.media.states.pictureInPicture.time | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateTime |
| a.media.states.inFocus.set | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateSet |
| a.media.states.inFocus.count | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateCount |
| a.media.states.inFocus.time | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateTime |

## API connexes {#related_apis_section}

* Android - [createStateObject](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* iOS - [createStateObjectWithName](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* Javascript - [createStateObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)
