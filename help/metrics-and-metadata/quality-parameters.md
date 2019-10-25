---
seo-title: Paramètres de qualité
title: Paramètres de qualité
uuid: 0d9fa764-edef-4178-8650-90c9a0852a57
translation-type: tm+mt
source-git-commit: 8938e324d570b7e3e2c3c3e971c00ade7e6be8b6

---


# Paramètres de qualité{#quality-parameters}

Cette rubrique présente une liste de données de qualité d’expérience (QoE/QoS), y compris les valeurs de données contextuelles, qu’Adobe collecte via des variables de solution.

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

## Métadonnées de qualité {#quality-metadata}

### Débit moyen

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **Clé API :**<br/>media.qoe.bitrate </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/>Fermer </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 800-899 </li><li> **Description:**<br/>Le débit moyen (en Kbit/s). La valeur est prédéfinie par intervalles de 100 Kbits/s. Ce débit moyen correspond à la valeur moyenne pondérée de toutes les valeurs de débit liées à la durée des lectures au cours d’une session de lecture.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>bitrateAverageBucket) </li> <li> ****<br/> Heartbeat : (l:stream:bitrate) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Débit moyen </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>bitrateAverageBucket) </li> <li> **Flux de données :**<br/>videoqoebitrateaverageevar </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverageBucket) </li> </ul> |



### Temps jusqu’au début

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.qoe.timeToStart </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 30 000 </li><li> **Description :**<br/>cette valeur est définie par défaut sur zéro si vous ne la définissez pas via l’objet QoSObject. Cette valeur est exprimée en millisecondes. La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>timeToStart) </li> <li> ****<br/> Heartbeat : (l:stream:startup_time) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Temps jusqu’au début </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>timeToStart) </li> <li> **Flux de données :**<br/>videoqoetimetostartevar </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> </ul> |



### FPS

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.qoe.framesPerSecond </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Media Start, Media Close </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 24 </li><li> **Description:**<br/>Valeur actuelle de la cadence du flux (en images par seconde).  </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> </li> <li> ****<br/> Heartbeat : (l:stream:fps) </li> </ul> | <ul> <li> **Disponible :**<br/>Non </li> <li> **Variable réservée :**<br/>S.O. </li> <li> **Nom du rapport :**<br/>S.O. </li> <li> **Données contextuelles :**<br/> </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> </li> </ul> |



### Perte d’images

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>droppedFrames </li> <li> **Clé API :**<br/>media.qoe.droppedFrames </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 3 </li><li> **Description:**<br/>Nombre d’images perdues (Int). Cette valeur correspond à la somme des pertes d’images survenues au cours d’une session de lecture. Cette valeur provient de la dernière valeur de (l:stream:dropped_frames).  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>droppedFrameCount) </li> <li> ****<br/> Heartbeat : (l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Perte d’images </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>droppedFrameCount) </li> <li> **Flux de données :**<br/>videoqoedroppedframecountevar </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>droppedFrameCount) </li> </ul> |



### Événements de mémoire tampon

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 2 </li><li> **Description:**<br/>Nombre d'événements de mémoire tampon. Cette mesure correspond au nombre d’états de mémoire tampon qui se sont produits au cours d’une session de lecture. Il s’agit du nombre de fois où le lecteur entre dans l’état de mémoire tampon à partir d’autres états (par exemple, lecture ou pause).  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>bufferCount) </li> <li> ****<br/> Heartbeat : (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Événements de mémoire tampon </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>bufferCount) </li> <li> **Flux de données :**<br/>videoqoebuffercountevar </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> </ul> |



### Durée totale de la mémoire tampon

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** </li> <li> ****<br/> Exemple de valeur : 30 </li><li> **Description:**<br/>Durée totale, en secondes, de la mise en mémoire tampon. Cette valeur correspond à la durée totale de tous les événements de mémoire tampon qui se sont produits au cours d’une session de lecture. La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes. <br/>**Date de publication : 13/09/18**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>bufferTime) </li> <li> ****<br/> Heartbeat : (l:event:length) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Durée totale de la mémoire tampon </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>bufferTime) </li> <li> **Flux de données :**<br/>videoqoebuffertimeevar </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> </ul> |



### Changements de débit

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.qoe.bitrateChange </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 3 </li><li> **Description:**<br/>Nombre de changements de débit (Entier). Cette valeur correspond à la somme des événements de changement de débit qui se sont produits au cours d’une session de lecture.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>bitrateChangeCount) </li> <li> ****<br/> Heartbeat : (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Changements de débit </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Flux de données :**<br/>videoqoebitratechangecountevar </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> </ul> |



### Erreurs / Événements d’erreur

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :** <br/> </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 1 </li><li> **Description :**<br/>nombre d’erreurs (entier). Cette valeur correspond à la somme des événements d’erreur qui se sont produits au cours d’une session de lecture.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>errorCount) </li> <li> ****<br/> Heartbeat : (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Erreurs </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>errorCount) </li> <li> **Flux de données :**<br/>videoqoeerrorcountevar </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> </ul> |



### ID d’erreur du SDK du lecteur

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :** <br/> </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> </li><li> **Description:**<br/>Identifiants d’erreur uniques générés par le SDK du lecteur. Les clients doivent fournir les codes/identifiants d’erreur au moment de la mise en œuvre via les API d’erreur fournies.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>playerSdkErrors) </li> <li> ****<br/> Heartbeat : (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Erreurs </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>playerSdkErrors) </li> <li> ****<br/> Flux de données : videoqoeplayersdkerrors </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>playerSdkErrors) </li> </ul> |



### ID d’erreur externes

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :** <br/> </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> </li><li> **Description:**<br/>Identifiants d’erreur uniques provenant de toute source externe, par exemple les erreurs CDN. Les clients doivent fournir les codes/identifiants d’erreur au moment de la mise en œuvre via les API d’erreur fournies.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>externalErrors) </li> <li> ****<br/> Heartbeat : (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Erreurs </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>externalErrors) </li> <li> ****<br/> Flux de données : videoqoeextneralerreurs </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>externalErrors) </li> </ul> |



### ID d’erreur du SDK Media

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :** <br/> </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> **Exemple de valeur :**<br/> </li><li> **Description :**<br/>ID d’erreur unique générés par le SDK multimédia pendant la lecture.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>mediaSdkErrors) </li> <li> ****<br/> Heartbeat : (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Erreurs </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>mediaSdkErrors) </li> <li> **Flux de données :** <br/>mediaqoeexternalerrors </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>mediaSdkErrors) </li> </ul> |




### Fin de session {#session-end}

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :** <br/> </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** 2.1 </li> <li> ****<br/> Exemple de valeur : end </li><li> **Description:**<br/>L’événement end signifie que le SDK envoie un appel de fin au serveur principal. À la réception de cet événement, le serveur principal ferme la session de cette vidéo et ne procède pas à un autre traitement. <br/>Si le média a été complété à 100 %, il doit être envoyé après `s:event:type=complete.` la fin [du](audio-video-parameters.md#content-complete) contenu pour obtenir des informations connexes. </li> </ul> | <ul> <li> **Adobe Analytics :**<br/>S.O. </li> <li> ****<br/> Heartbeats : (s:event:type=end) </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement personnalisée </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>S.O. </li> <li> **Données contextuelles :**<br/> </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> </li> </ul> |



## Mesures de qualité {#quality-metrics}

### Temps jusqu’au début

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 30 000 </li><li> **Description :**<br/>cette valeur est définie par défaut sur zéro si vous ne la définissez pas via l’objet QoSObject. Cette valeur est exprimée en millisecondes. La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes. <br/>**Date de publication : 13/09/18**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>timeToStart) </li> <li> ****<br/> Heartbeat : (l:stream:startup_time) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Temps jusqu’au début </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>timeToStart) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> </ul> |



### Événements de mémoire tampon

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 2 </li><li> **Description:**<br/>Nombre d'événements de mémoire tampon (Entier). Cette mesure correspond au nombre d’événements de mémoire tampon qui se sont produits au cours d’une session de lecture.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>bufferCount) </li> <li> ****<br/> Heartbeat : (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Événements de mémoire tampon </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>bufferCount) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> </ul> |



### Durée totale de la mémoire tampon

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 15 </li><li> **Description:**<br/>Durée totale de mise en mémoire tampon (secondes; integer). Cette valeur correspond à la durée totale de tous les événements de mémoire tampon qui se sont produits au cours d’une session de lecture. La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes. <br/>**Date de publication : 13/09/18**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>bufferTime) </li> <li> ****<br/> Heartbeat : (l:event:length) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Durée totale de la mémoire tampon </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>bufferTime) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> </ul> |



### Changements de débit

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Événement </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : "3" </li><li> **Description:**<br/>Nombre de changements de débit. Cette valeur correspond à la somme des événements de changement de débit qui se sont produits au cours d’une session de lecture.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>bitrateChangeCount) </li> <li> ****<br/> Heartbeat : (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Changements de débit </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> </ul> |



### Erreurs

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 1 </li><li> **Description :**<br/>nombre d’erreurs survenues (entier). Cette valeur correspond à la somme des événements d’erreur qui se sont produits au cours d’une session de lecture.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>errorCount) </li> <li> ****<br/> Heartbeat : (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Événements d’erreur </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>errorCount) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> </ul> |



### Perte d’images

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 1 </li><li> **Description:**<br/>Nombre d’images perdues (Entier). Cette valeur correspond à la somme des pertes d’images survenues au cours d’une session de lecture.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>droppedFrameCount) </li> <li> ****<br/> Heartbeat : (l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Perte d’images </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>droppedFrameCount) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>droppedFrameCount) </li> </ul> |



### Pertes avant le début

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : TRUE </li><li> **Description :**<br/>nombre de fois où un utilisateur a quitté la vidéo avant son démarrage. Cette mesure est définie sur 1 uniquement si aucun contenu ne s’est affiché, sans tenir compte des publicités.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>dropBeforeStart) </li> <li> ****<br/> Heartbeat : (s:event:<br/>type=aa_start) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Pertes avant le début </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>dropBeforeStart) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>dropBeforeStart) </li> </ul> |



>[!IMPORTANT]
>Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.

### Flux touchés par la mémoire tampon

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : TRUE </li><li> **Description:**<br/>Nombre de flux touchés par la mise en mémoire tampon. Cette mesure est définie sur 1 uniquement si au moins un événement de mémoire tampon s’est produit au cours de la session de lecture.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>buffer) </li> <li> ****<br/> Heartbeat : (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Diffusions touchées par la mémoire tampon </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>buffer) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>buffer) </li> </ul> |



>[!IMPORTANT]
>Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.

### Flux touchés par les changements de débit

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : TRUE </li><li> **Description :**<br/>nombre de flux dans lesquels des changements de débit se sont produits. Cette mesure est définie sur 1 uniquement si au moins un changement de débit s’est produit au cours de la session de lecture.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>bitrateChange) </li> <li> ****<br/> Heartbeat : (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> ****<br/> Nom du rapport : Flux touchés par les changements de débit </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>bitrateChange) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>bitrateChange) </li> </ul> |



>[!IMPORTANT]
>Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.

### Débit moyen

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : 3200 </li><li> **Description:**<br/>Le débit moyen (en kbit/s, entier). Cette mesure correspond à la valeur moyenne pondérée de toutes les valeurs de débit liées à la durée des lectures au cours d’une session de lecture.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>bitrateAverage) </li> <li> ****<br/> Heartbeat : (l:stream:bitrate) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Débit moyen </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>bitrateAverage) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverage) </li> </ul> |



### Flux touchés par les erreurs

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : TRUE </li><li> **Description :**<br/>nombre de flux dans lesquels un événement d’erreur s’est produit (c.-à-d. `trackError` a été appelé pendant la session de lecture et un appel de `type=error` pulsation a été généré). </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>error) </li> <li> ****<br/> Heartbeat : (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Diffusions touchées par les erreurs </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>error) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>error) </li> </ul> |



>[!IMPORTANT]
>Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.

### Flux touchés par la perte d’images

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** Quelconque </li> <li> ****<br/> Exemple de valeur : TRUE </li><li> **Description:**<br/>Nombre de flux dans lesquels des images ont été ignorées. Cette mesure est définie sur 1 uniquement si au moins une image a été perdue au cours de la session de lecture.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>droppedFrames) </li> <li> ****<br/> Heartbeat : (l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/>Diffusions touchées par la perte d’images </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>droppedFrames) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>droppedFrames) </li> </ul> |



>[!IMPORTANT]
>Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.

### Flux touchés par un blocage

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5+ </li> <li> ****<br/> Exemple de valeur : TRUE </li><li> **Description:**<br/>Nombre de flux dans lesquels un événement bloqué s’est produit. Cette mesure est définie sur 1 uniquement si au moins un événement de blocage s’est produit au cours de la lecture. Les clients devront créer leurs propres règles de traitement afin que la valeur soit disponible pour les rapports.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>stall) </li> <li> ****<br/> Heartbeat : (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement personnalisée </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :** <br/> </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>stall) </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>stall) </li> </ul> |



>[!IMPORTANT]
>Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.

### Événements de blocage

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5+ </li> <li> ****<br/> Exemple de valeur : "3" </li><li> **Description :**<br/>nombre de fois où la lecture a été bloquée au cours d’une session de lecture. Les clients devront créer leurs propres règles de traitement afin que la valeur soit disponible pour les rapports.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>stallCount) </li> <li> ****<br/> Heartbeat : (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement personnalisée </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :** <br/> </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>stallCount) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>stallCount) </li> </ul> |



### Durée totale de blocage

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Nombre </li> <li> ****<br/> Envoyé avec : Fermeture du média </li> <li> **Min. Version SDK min. :** 1.5+ </li> <li> ****<br/> Exemple de valeur : 12 </li><li> **Description:**<br/>Durée totale (secondes; entier) la lecture a été bloquée pendant une session de lecture. Les clients devront créer leurs propres règles de traitement afin que la valeur soit disponible pour les rapports.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics : (a.media.qoe.<br/>stallTime) </li> <li> ****<br/> Heartbeat : (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Disponible :**<br/>Utiliser la règle de traitement personnalisée </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :** <br/> </li> <li> ****<br/> Données contextuelles : (a.media.qoe.<br/>stallTime) </li> <li> **Flux de données :**<br/>S.O. </li> <li> ****<br/> Audience Manager : (c_contextdata.<br/>a.media.qoe.<br/>stallTime) </li> </ul> |



## API connexes {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* JavaScript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

