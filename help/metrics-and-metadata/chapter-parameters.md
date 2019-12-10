---
title: Paramètres de chapitre
description: null
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Paramètres de chapitre {#chapter-parameters}

Cette rubrique présente une liste des données de chapitre et/ou de segment, y compris les valeurs de données contextuelles, qu’Adobe collecte via les variables de solution.

Description des données de tableau :

* **Mise en œuvre :** Informations sur les valeurs et les exigences de mise en œuvre
   * *Clé* : Variable, définie manuellement dans votre application ou automatiquement par le kit Adobe Media SDK.
   * *Obligatoire* : Indique si le paramètre est requis pour le suivi de la vidéo de base.
   * *Type* : Spécifie le type de variable à définir, chaîne ou nombre.
   * *Envoyé avec* : Indique le moment où les données sont envoyées : *Démarrage du média* est l’appel d’analyse envoyé au début du média, *Démarrage de la publicité* est l’appel d’analyse envoyé au début de la publicité, etc. *Fermer* est l’appel d’analyse compilé envoyé directement du serveur de pulsation au serveur d’analyse à la fin de la session multimédia ou de la publicité, du chapitre, etc. Les appels Fermer ne sont pas disponibles dans les appels de paquets réseau.
   * *min. Version SDK* : Indique la version SDK dont vous auriez besoin pour accéder au paramètre.
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
>Ne modifiez pas les noms de classification des variables répertoriées ci-dessous, qui sont décrites sous Variable de création de rapports/réservée comme « classification ».\
>Les classifications des médias sont définies lorsqu’une suite de rapports est activée pour le suivi multimédia. De temps à autre, Adobe ajoute de nouvelles propriétés. Dans ce cas, les clients doivent réactiver leurs suites de rapports pour accéder aux nouvelles propriétés du média. Au cours du processus de mise à jour, Adobe détermine si les classifications sont activées en vérifiant les noms des variables. Si l’un d’eux manque, Adobe l’ajoute à nouveau.

## Métadonnées de chapitre {#chapter-metadata}

### Nom du chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **Clé API :**<br/>media.chapter.friendlyName </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Démarrage de chapitre, Fermeture de chapitre </li> <li> **min. Version SDK min. :** 1.3 </li> <li> **Exemple de valeur :**<br/> « The Big Bang Chapitre 2 - Rendez-vous » </li><li> **Description :**<br/>Nom du chapitre et/ou du segment.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Heartbeat :**<br/> (s:stream:chapter_name) </li> </ul> | <ul> <li> **Disponible :**<br/>Créé par défaut...  </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/>Nom du chapitre </li> <li> **Données contextuelles :**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.chapter.<br/>friendlyName) </li> </ul> |

### Position du chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **Clé API :**<br/>media.chapter.index </li> <li> **Obligatoire :**<br/> SDK : Non ; API : Oui. </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture de chapitre </li> <li> **min. Version SDK min. :** 1.3 </li> <li> **Exemple de valeur :**<br/> 2 </li><li> **Description :**<br/>Position (index, entier) du chapitre dans le contenu.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.chapter.<br/>position) </li> <li> **Heartbeat :**<br/> (l:stream:chapter_pos) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/>Position du chapitre </li> <li> **Données contextuelles :**<br/> (a.media.chapter.<br/>position) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.chapter.<br/>position) </li> </ul> |

### Décalage de chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **Clé API :**<br/>media.chapter.offset </li> <li> **Obligatoire :**<br/> SDK : Non ; API : Oui. </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture de chapitre </li> <li> **min. Version SDK min. :** 1.3 </li> <li> **Exemple de valeur :**<br/> 58 </li><li> **Description :**<br/>Décalage du chapitre dans le contenu (en secondes) à partir du début.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.chapter.<br/>offset) </li> <li> **Heartbeat :**<br/> (l:stream:chapter_offset) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/>Décalage de chapitre </li> <li> **Données contextuelles :**<br/> (a.media.chapter.<br/>offset) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.chapter.<br/>offset) </li> </ul> |

### Durée du chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/>media.chapter.length </li> <li> **Obligatoire :**<br/> SDK : Non ; API : Oui. </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture de chapitre </li> <li> **min. Version SDK min. :** 1.3 </li> <li> **Exemple de valeur :**<br/> 486 </li><li> **Description :**<br/>Durée du chapitre, en secondes.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.chapter.<br/>length) </li> <li> **Heartbeat :**<br/> (l:stream:chapter_offset) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>Classification </li> <li> **Nom du rapport :**<br/>Durée du chapitre </li> <li> **Données contextuelles :**<br/> (a.media.chapter.<br/>length) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.chapter.<br/>length) </li> </ul> |

### Chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Non </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture de chapitre </li> <li> **min. Version SDK min. :** 1.3 </li> <li> **Exemple de valeur :**<br/> </li><li> **Description :**<br/>ID généré automatiquement du chapitre.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.chapter.<br/>name) </li> <li> **Heartbeat :**<br/> (s:stream:chapter_name) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>eVar </li> <li> **Expiration :**<br/>À l’ACCÈS </li> <li> **Nom du rapport :**<br/>Chapitre </li> <li> **Données contextuelles :**<br/> (a.media.chapter.<br/>name) </li> <li> **Flux de données :**<br/>videochapter </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.chapter.<br/>name) </li> </ul> |

## Mesures de chapitre {#chapter-Metrics}

### Début du chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement  </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/>Démarrage de chapitre </li> <li> **min. Version SDK min. :** 1.3 </li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/>Nombre de chapitres qui commencent.  **Important :** Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.chapter.<br/>view) </li> <li> **Heartbeat :**<br/> (s:event:<br/>type=chapter_start) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/> Démarrages de chapitre </li> <li> **Données contextuelles :**<br/> (a.media.chapter.<br/>view) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.chapter.<br/>view) </li> </ul> |

### Chapitre terminé

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement  </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture de chapitre </li> <li> **min. Version SDK min. :** 1.3</li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/>Nombre de chapitres terminés.  **Important :** Si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.chapter.<br/>complete) </li> <li> **Heartbeat :**<br/> (s:event:<br/>type=chapter_complete) </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :<br/>** Fins de chapitre </li> <li> **Données contextuelles :**<br/> (a.media.chapter.<br/>complete) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.chapter.<br/>complete) </li> </ul> |

### Passé sur le chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>Définie automatiquement  </li> <li> **Clé API :**<br/>S.O. </li> <li> **Obligatoire :**<br/>Oui </li> <li> **Type :**<br/>Nombre </li> <li> **Envoyé avec :**<br/> Fermeture de chapitre </li> <li> **min. Version SDK min. :** 1.3 </li> <li> **Exemple de valeur :**<br/> </li><li> **Description :**<br/>Temps passé sur le chapitre.  La valeur s’affichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes. <br/>**Date de publication : 13/09/18**   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **Heartbeat :**<br/> </li> </ul> | <ul> <li> **Disponible :**<br/>Oui </li> <li> **Variable réservée :**<br/>event </li> <li> **Nom du rapport :**<br/> Temps passé par chapitre </li> <li> **Données contextuelles :**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **Flux de données :**<br/>S.O. </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.chapter.<br/>timePlayed) </li> </ul> |

## API connexes {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* JavaScript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
