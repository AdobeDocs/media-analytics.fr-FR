---
seo-title: Paramètres de chapitre
title: Paramètres de chapitre
uuid: 2 a 6 b 9247-a 694-46 e 9-98 e 1-424 c 08 c 27 ec 2
translation-type: tm+mt
source-git-commit: f7ffb9a88f1cf3ffefba0ae5508a857fa3de8432

---


# Paramètres de chapitre{#chapter-parameters}

Cette rubrique présente une liste des données de chapitre et/ou de segment, y compris les valeurs de données contextuelles, qu’Adobe collecte via les variables de solution.

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

## Métadonnées de chapitre {#section_534D3A6BFEB24D1884F80AD6A50BF13C}

### Nom du chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **Clé API :**<br/>media.chapter.friendlyName </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Début du chapitre, Fermeture du chapitre </li> <li> **Min. Version SDK min. :** 1.3 </li> <li> **Exemple de valeur :**<br/> « The Big Bang Chapter 2 - Dating » </li><li> **Description :**<br/>Nom du chapitre et/ou du segment.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. chapter.<br/>Friendlyname) </li> <li> **Heartbeat :**<br/> (s : stream : chapter_ name) </li> </ul> | <ul> <li> **Disponible :**<br/>Créé par défaut...  </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/>Nom du chapitre </li> <li> **Données contextuelles :**<br/> (a. media. chapter.<br/>Friendlyname) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>Friendlyname) </li> </ul> |

### Position du chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **Clé API :**<br/>media.chapter.index </li> <li> **Obligatoire :**<br/> SDK : Non ; API : Oui. </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du chapitre </li> <li> **Min. Version SDK min. :** 1.3 </li> <li> **Exemple de valeur :**<br/> 2 </li><li> **Description :**<br/>Position (index, entier) du chapitre à l'intérieur du contenu.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. chapter.<br/>position) </li> <li> **Heartbeat :**<br/> (l : stream : chapter_ pos) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/>Position du chapitre </li> <li> **Données contextuelles :**<br/> (a. media. chapter.<br/>position) </li> <li> **Flux de données :**<br/> </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>position) </li> </ul> |

### Décalage de chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **Clé API :**<br/>media.chapter.offset </li> <li> **Obligatoire :**<br/> SDK : Non ; API : Oui. </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du chapitre </li> <li> **Min. Version SDK min. :** 1.3 </li> <li> **Exemple de valeur :**<br/> 58 </li><li> **Description :**<br/>Décalage du chapitre à l'intérieur du contenu (en secondes) à partir du début.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. chapter.<br/>offset) </li> <li> **Heartbeat :**<br/> (l : stream : chapter_ offset) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/>Décalage de chapitre </li> <li> **Données contextuelles :**<br/> (a. media. chapter.<br/>offset) </li> <li> **Flux de données :**<br/> </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>offset) </li> </ul> |

### Durée du chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.chapter.length </li> <li> **Obligatoire :**<br/> SDK : Non ; API : Oui. </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du chapitre </li> <li> **Min. Version SDK min. :** 1.3 </li> <li> **Exemple de valeur :**<br/> 486 </li><li> **Description :**<br/>Durée du chapitre, en secondes.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. chapter.<br/>length) </li> <li> **Heartbeat :**<br/> (l : stream : chapter_ length) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/>Durée du chapitre </li> <li> **Données contextuelles :**<br/> (a. media. chapter.<br/>length) </li> <li> **Flux de données :**<br/> </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>length) </li> </ul> |

### Chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du chapitre </li> <li> **Min. Version SDK min. :** 1.3 </li> <li> **Exemple de valeur :**<br/> </li><li> **Description :**<br/>Identifiant généré automatiquement du chapitre.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. chapter.<br/>name) </li> <li> **Heartbeat :**<br/> (s : stream : chapter_ id) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Chapitre </li> <li> **Données contextuelles :**<br/> (a. media. chapter.<br/>name) </li> <li> **Flux de données :**<br/>videochapter </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>name) </li> </ul> |

## Mesures de chapitre {#section_1C47D6FB1DF343C39CE7A8F724406F33}

### Début du chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement  </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de chapitre </li> <li> **Min. Version SDK min. :** 1.3 </li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/>Le nombre de chapitres commence. Important : Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. chapter.<br/>view) </li> <li> **Heartbeat :**<br/> (s : event :<br/>type = chapter_ start) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/> Le chapitre commence g </li> <li> **Données contextuelles :**<br/> (a. media. chapter.<br/>view) </li> <li> **Flux de données :**<br/>videochapterstart </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>view) </li> </ul> |

### Chapitre terminé

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement  </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture du chapitre </li> <li> **Min. Version SDK min. :** 1.3</li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/>Nombre de chapitres terminés. Important : Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. chapter.<br/>complete) </li> <li> **Heartbeat :**<br/> (s : event :<br/>type = chapter_ complete) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/> Chapitre terminé g </li> <li> **Données contextuelles :**<br/> (a. media. chapter.<br/>complete) </li> <li> **Flux de données :**<br/>videochaptercomplete </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>complete) </li> </ul> |

### passé sur le chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports   |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement  </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture du chapitre </li> <li> **Min. Version SDK min. :** 1.3 </li> <li> **Exemple de valeur :**<br/> </li><li> **Description :**<br/>Temps passé sur le chapitre. La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes. <br/>**Date de publication : 13/09/18**   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a. media. chapter.<br/>Timeplayed) </li> <li> **Heartbeat :**<br/> </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/> Durée de consultation du chapitre g </li> <li> **Données contextuelles :**<br/> (a. media. chapter.<br/>Timeplayed) </li> <li> **Flux de données :**<br/>videochaptertime </li> <li> **Audience Manager :**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>Timeplayed) </li> </ul> |

## Related APIs {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
