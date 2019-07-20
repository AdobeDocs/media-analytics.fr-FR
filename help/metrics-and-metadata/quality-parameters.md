---
seo-title: Paramètres de qualité
title: Paramètres de qualité
uuid: 0 d 9 fa 764-edef -4178-8650-90 c 9 a 0852 a 57
translation-type: tm+mt
source-git-commit: 180eafdfc536039820ade0b52e5c55f874719d8e

---


# Paramètres de qualité{#quality-parameters}

Cette rubrique présente une liste de données de qualité d’expérience (QoE/QoS), y compris les valeurs de données contextuelles, qu’Adobe collecte via des variables de solution.

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

## Métadonnées de qualité {#section_8467F9729DA04A888A2657712234D7C7}

### Débit moyen

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **Clé API :**<br/>media.qoe.bitrate </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/>Fermer </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 800-899 </li><li> **Description :**<br/>Débit moyen (en Kbits/s). La valeur est prédéfinie par intervalles de 100 Kbits/s. Ce débit moyen correspond à la valeur moyenne pondérée de toutes les valeurs de débit liées à la durée des lectures au cours d’une session de lecture.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>Bitrateaveragebucket) </li> <li> **Heartbeat :**<br/> (l : stream : débit) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Débit moyen </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>Bitrateaveragebucket) </li> <li> **Flux de données :**<br/>videoqoebitrateaverageevar </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitrateaveragebucket) </li> </ul> |



### Temps jusqu’au début

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.qoe.timeToStart </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 30 000 </li><li> **Description :**<br/>Cette valeur est définie par défaut sur zéro si vous ne la définissez pas via qosobject. Cette valeur est exprimée en millisecondes. La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Heartbeat :**<br/> (l : stream : startup_ time) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Temps jusqu’au début </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Flux de données :**<br/>videoqoetimetostartevar </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>timeToStart) </li> </ul> |



### FPS

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.qoe.framesPerSecond </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Début du média, Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 24 </li><li> **Description :**<br/>Valeur actuelle du débit d'image de flux (en images par seconde).  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> </li> <li> **Heartbeat :**<br/> (l : stream : i/s) </li> </ul> | <ul> <li> **Disponible :**<br/>Non </li> <li> **Variable réservée :**<br/>S.O. </li> <li> **Nom du rapport :**<br/>S.O. </li> <li> **Données contextuelles :**<br/> </li> <li> **Flux de données :**<br/> </li> <li> **Audience Manager :**<br/> </li> </ul> |



### Perte d’images

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>droppedFrames </li> <li> **Clé API :**<br/>media.qoe.droppedFrames </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 3 </li><li> **Description :**<br/>Nombre d'images perdues (entier). Cette valeur correspond à la somme des pertes d’images survenues au cours d’une session de lecture. Cette valeur est prise à partir de la dernière valeur de (l : stream : dropped_ frames.)  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Heartbeat :**<br/> (l : stream :<br/>dropped_ frames) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Perte d’images </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Flux de données :**<br/>videoqoedroppedframecountevar </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Droppedframecount) </li> </ul> |



### Événements de mémoire tampon

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 2 </li><li> **Description :**<br/>Nombre d'événements de mémoire tampon. Cette mesure correspond au nombre d’états de mémoire tampon qui se sont produits au cours d’une session de lecture. Il s’agit du nombre de fois où le lecteur entre dans l’état de mémoire tampon à partir d’autres états (par exemple, lecture ou pause).  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Heartbeat :**<br/> (s : event :<br/>type = buffer) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Événements de mémoire tampon </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Flux de données :**<br/>videoqoebuffercountevar </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffercount) </li> </ul> |



### Durée totale de la mémoire tampon

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** </li> <li> **Exemple de valeur :**<br/> 30 </li><li> **Description :**<br/>Durée totale, en secondes, de mise en mémoire tampon passée. Cette valeur correspond à la durée totale de tous les événements de mémoire tampon qui se sont produits au cours d’une session de lecture. La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes. <br/>**Date de publication : 13/09/18**  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Heartbeat :**<br/> (l : event : duration) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Durée totale de la mémoire tampon </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Flux de données :**<br/>videoqoebuffertimeevar </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffertime) </li> </ul> |



### Changements de débit

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.qoe.bitrateChange </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 3 </li><li> **Description :**<br/>Nombre de changements de débit (entier). Cette valeur correspond à la somme des événements de changement de débit qui se sont produits au cours d’une session de lecture.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Heartbeat :**<br/> (s : event :<br/>type = bitrate_ change) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Changements de débit </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Flux de données :**<br/>videoqoebitratechangecountevar </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitratechangecount) </li> </ul> |



### Erreurs / Événements d’erreur

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :** <br/> </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 1 </li><li> **Description :**<br/>Nombre d'erreurs survenues (entier). Cette valeur correspond à la somme des événements d’erreur qui se sont produits au cours d’une session de lecture.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>Errorcount) </li> <li> **Heartbeat :**<br/> (s : event :<br/>type = error) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Erreurs </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>Errorcount) </li> <li> **Flux de données :**<br/>videoqoeerrorcountevar </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Errorcount) </li> </ul> |



### ID d’erreur du SDK du lecteur

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :** <br/> </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> </li><li> **Description :**<br/>ID d'erreur unique généré par le SDK du lecteur. Les clients doivent fournir les codes/identifiants d’erreur au moment de la mise en œuvre via les API d’erreur fournies.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>Playersdkerrors) </li> <li> **Heartbeat :**<br/> (s : event :<br/>type = error) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Erreurs </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>Playersdkerrors) </li> <li> **Flux de données :**<br/> videoqoeplayersdkerrors </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Playersdkerrors) </li> </ul> |



### ID d’erreur externes

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :** <br/> </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> </li><li> **Description :**<br/>Identifiants d'erreur uniques provenant d'une source externe, par exemple des erreurs CDN. Les clients doivent fournir les codes/identifiants d’erreur au moment de la mise en œuvre via les API d’erreur fournies.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>Externalerrors) </li> <li> **Heartbeat :**<br/> (s : event :<br/>type = error) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Erreurs </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>Externalerrors) </li> <li> **Flux de données :**<br/> videoqoeextneralerrors </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Externalerrors) </li> </ul> |



### ID d’erreur du SDK Media

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :** <br/> </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> </li><li> **Description :**<br/>ID d'erreur unique généré par Media SDK lors de la lecture.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>Mediasdkerrors) </li> <li> **Heartbeat :**<br/> (s : event :<br/>type = error) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Erreurs </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>Mediasdkerrors) </li> <li> **Flux de données :** <br/>mediaqoeexternalerrors </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Mediasdkerrors) </li> </ul> |




### Fin de session {#session-end}

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :** <br/> </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** 2.1 </li> <li> **Exemple de valeur :**<br/> end </li><li> **Description :**<br/>L'événement end signifie que le SDK envoie un appel close au serveur principal. À la réception de cet événement, le serveur principal ferme la session de cette vidéo et ne procède pas à un autre traitement. <br/>Si le support a été atteint à 100 %, il doit être envoyé après `s:event:type=complete.` la fin de la consultation [du contenu](audio-video-parameters.md#content-complete) pour les informations connexes. </li> </ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> **Pulsations :**<br/> (s : event : type = end) </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement personnalisée </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>S.O. </li> <li> **Données contextuelles :**<br/> </li> <li> **Flux de données :**<br/> </li> <li> **Audience Manager :**<br/> </li> </ul> |



## Mesures de qualité {#section_8EB0C9CBC09340C8915E1D2707D0A9EE}

### Temps jusqu’au début

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 30 000 </li><li> **Description :**<br/>Cette valeur est définie par défaut sur zéro si vous ne la définissez pas via qosobject. Cette valeur est exprimée en millisecondes. La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes. <br/>**Date de publication : 13/09/18**  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Heartbeat :**<br/> (l : stream : startup_ time) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Temps jusqu’au début </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Flux de données :**<br/>videoqoetimetostart </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>timeToStart) </li> </ul> |



### Événements de mémoire tampon

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 2 </li><li> **Description :**<br/>Nombre d'événements de mémoire tampon (entier). Cette mesure correspond au nombre d’événements de mémoire tampon qui se sont produits au cours d’une session de lecture.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Heartbeat :**<br/> (s : event :<br/>type = buffer) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Événements de mémoire tampon </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Flux de données :**<br/>videoqoebuffercount </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffercount) </li> </ul> |



### Durée totale de la mémoire tampon

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 15 </li><li> **Description :**<br/>La durée totale de la mise en mémoire tampon (secondes ; integer). Cette valeur correspond à la durée totale de tous les événements de mémoire tampon qui se sont produits au cours d’une session de lecture. La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes. <br/>**Date de publication : 13/09/18**  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Heartbeat :**<br/> (l : event : duration) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Durée totale de la mémoire tampon </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Flux de données :**<br/>videoqoebuffertime </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffertime) </li> </ul> |



### Changements de débit

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Événement </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> « 3 » </li><li> **Description :**<br/>Nombre de changements de débit. Cette valeur correspond à la somme des événements de changement de débit qui se sont produits au cours d’une session de lecture.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Heartbeat :**<br/> (s : event :<br/>type = bitrate_ change) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Changements de débit </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Flux de données :**<br/>videoqoebitratechangecount </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitratechangecount) </li> </ul> |



### Erreurs

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 1 </li><li> **Description :**<br/>Nombre d'erreurs survenues (entier). Cette valeur correspond à la somme des événements d’erreur qui se sont produits au cours d’une session de lecture.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>Errorcount) </li> <li> **Heartbeat :**<br/> (s : event :<br/>type = error) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Événements d’erreur </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>Errorcount) </li> <li> **Flux de données :**<br/>videoqoeerrorcount </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Errorcount) </li> </ul> |



### Perte d’images

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 1 </li><li> **Description :**<br/>Nombre d'images perdues (entier). Cette valeur correspond à la somme des pertes d’images survenues au cours d’une session de lecture.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Heartbeat :**<br/> (l : stream :<br/>dropped_ frames) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Perte d’images </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Flux de données :**<br/>videoqoedroppedframecount </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Droppedframecount) </li> </ul> |



### Pertes avant le début

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/>Nombre de fois où un utilisateur quitte la vidéo avant de commencer. Cette mesure est définie sur 1 uniquement si aucun contenu ne s’est affiché, sans tenir compte des publicités.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>Dropbeforestart) </li> <li> **Heartbeat :**<br/> (s : event :<br/>type = aa_ start) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Pertes avant le début </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>Dropbeforestart) </li> <li> **Flux de données :**<br/>videoqoedropbeforestart </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Dropbeforestart) </li> </ul> |



>[!IMPORTANT]
>Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.

### Flux touchés par la mémoire tampon

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/>Le nombre de flux touchés par la mise en mémoire tampon. Cette mesure est définie sur 1 uniquement si au moins un événement de mémoire tampon s’est produit au cours de la session de lecture.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>buffer) </li> <li> **Heartbeat :**<br/> (s : event :<br/>type = buffer) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Diffusions touchées par la mémoire tampon </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>buffer) </li> <li> **Flux de données :**<br/>videoqoebuffer </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>buffer) </li> </ul> |



>[!IMPORTANT]
>Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.

### Flux touchés par les changements de débit

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/>Nombre de flux dans lesquels des changements de débit se sont produits. Cette mesure est définie sur 1 uniquement si au moins un changement de débit s’est produit au cours de la session de lecture.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>Bitratechange) </li> <li> **Heartbeat :**<br/> (s : event :<br/>type = bitrate_ change) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Diffusions touchées par les changements de mémoire tampon </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>Bitratechange) </li> <li> **Flux de données :**<br/>videoqoebitratechange </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitratechange) </li> </ul> |



>[!IMPORTANT]
>Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.

### Débit moyen

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> 3200 </li><li> **Description :**<br/>Débit moyen (en kbit/s, entier). Cette mesure correspond à la valeur moyenne pondérée de toutes les valeurs de débit liées à la durée des lectures au cours d’une session de lecture.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>Bitrateaverage) </li> <li> **Heartbeat :**<br/> (l : stream : débit) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Débit moyen </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>Bitrateaverage) </li> <li> **Flux de données :**<br/>videoqoebitrateaverage </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitrateaverage) </li> </ul> |



### Flux touchés par les erreurs

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/>Nombre de flux dans lesquels des changements de débit se sont produits. Cette mesure est définie sur 1 uniquement si au moins un changement de débit s’est produit au cours de la session de lecture.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>error) </li> <li> **Heartbeat :**<br/> (s : event :<br/>type = error) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Diffusions touchées par les erreurs </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>error) </li> <li> **Flux de données :**<br/>videoqoeerror </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>error) </li> </ul> |



>[!IMPORTANT]
>Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.

### Flux touchés par la perte d’images

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/>Nombre de flux dans lesquels des cadres ont été déposés. Cette mesure est définie sur 1 uniquement si au moins une image a été perdue au cours de la session de lecture.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>droppedFrames) </li> <li> **Heartbeat :**<br/> (l : stream :<br/>dropped_ frames) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Diffusions touchées par la perte d’images </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>droppedFrames) </li> <li> **Flux de données :**<br/>videoqoedroppedframes </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>droppedFrames) </li> </ul> |



>[!IMPORTANT]
>Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.

### Flux touchés par un blocage

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5+ </li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/>Nombre de flux dans lesquels un événement bloqué a eu lieu. Cette mesure est définie sur 1 uniquement si au moins un événement de blocage s’est produit au cours de la lecture. Les clients devront créer leurs propres règles de traitement afin que la valeur soit disponible pour les rapports.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>stall) </li> <li> **Heartbeat :**<br/> (s : event :<br/>type = stall) </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement personnalisée </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :** <br/> </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>stall) </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>stall) </li> </ul> |



>[!IMPORTANT]
>Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.

### Événements de blocage

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5+ </li> <li> **Exemple de valeur :**<br/> « 3 » </li><li> **Description :**<br/>Nombre de fois où la lecture a été bloquée pendant la session de lecture. Les clients devront créer leurs propres règles de traitement afin que la valeur soit disponible pour les rapports.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>Stallcount) </li> <li> **Heartbeat :**<br/> (s : event :<br/>type = stall) </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement personnalisée </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :** <br/> </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>Stallcount) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Stallcount) </li> </ul> |



### Durée totale de blocage

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5+ </li> <li> **Exemple de valeur :**<br/> 12 </li><li> **Description :**<br/>Durée totale (secondes ; integer) La lecture a été bloquée pendant la session de lecture. Les clients devront créer leurs propres règles de traitement afin que la valeur soit disponible pour les rapports.  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. qoe.<br/>Stalltime) </li> <li> **Heartbeat :**<br/> (s : event :<br/>type = stall) </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement personnalisée </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :** <br/> </li> <li> **Données contextuelles :**<br/> (a. media. qoe.<br/>Stalltime) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Stalltime) </li> </ul> |



## Related APIs {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

