---
title: 'Paramètres de chapitre '
description: « Apprenez en plus sur les paramètres des chapitres pour la mise en œuvre, le réseau et la création de rapports. »
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: 73da3e52-9498-478e-bfd7-8ff6c8e6bfc5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: c61e0bce6338a2fa89dafa29c4f600c5640d2d97
workflow-type: ht
source-wordcount: '1109'
ht-degree: 100%

---

# Paramètres de chapitre {#chapter-parameters}

Cette rubrique présente une liste des données de chapitre et/ou de segment, y compris les valeurs de données contextuelles, qu’Adobe collecte via les variables de solution.

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

## Métadonnées de chapitre {#chapter-metadata}

### Nom du chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **Clé API :**<br/> media.chapter.friendlyName </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> Chaîne </li> <li> **Envoyé avec :**<br/> Démarrage de chapitre, Fermeture de chapitre </li> <li> **Version minimum du SDK :**  1.3 </li> <li> **Exemple de valeur :**<br/> « The Big Bang Chapitre 2 - Rendez-vous » </li><li> **Description :**<br/> nom du chapitre et/ou du segment.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Heartbeat :**<br/> (s:stream:chapter_name) </li> </ul> | <ul> <li> **Disponible :**<br/> Créé par défaut...  </li> <li> **Variable réservée :**<br/> Classification </li> <li> **Nom du rapport :**<br/> Nom du chapitre </li> <li> **Données contextuelles :**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Flux de données :**<br/> S.O. </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.chapter.<br/>friendlyName) </li> <li> **Chemin dʼaccès du champ XDM :**<br/> media.mediaTimed.mediaChapter.chapterAssetReference.dc:title </li> </ul> |

### Position du chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **Clé API :**<br/> media.chapter.index </li> <li> **Obligatoire :**<br/> SDK : Non ; API : Oui. </li> <li> **Type :**<br/> Nombre </li> <li> **Envoyé avec :**<br/> Fermeture de chapitre </li> <li> **Version minimum du SDK :**  1.3 </li> <li> **Exemple de valeur :**<br/> 2 </li><li> **Description :**<br/> position (index, entier) du chapitre dans le contenu.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.chapter.<br/>position) </li> <li> **Heartbeat :**<br/> (l:stream:chapter_pos) </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> Classification </li> <li> **Nom du rapport :**<br/> Position du chapitre </li> <li> **Données contextuelles :**<br/> (a.media.chapter.<br/>position) </li> <li> **Flux de données :**<br/> S.O. </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.chapter.<br/>position) </li> <li> **Chemin dʼaccès du champ XDM :**<br/> media.mediaTimed.mediaChapter.chapterAssetViewDetails.index </li> </ul> |

### Décalage de chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **Clé API :**<br/> media.chapter.offset </li> <li> **Obligatoire :**<br/> SDK : Non ; API : Oui. </li> <li> **Type :**<br/> Nombre </li> <li> **Envoyé avec :**<br/> Fermeture de chapitre </li> <li> **Version minimum du SDK :**  1.3 </li> <li> **Exemple de valeur :**<br/> 58 </li><li> **Description :**<br/> décalage du chapitre dans le contenu (en secondes) à partir du début.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.chapter.<br/>offset) </li> <li> **Heartbeat :**<br/> (l:stream:chapter_offset) </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> Classification </li> <li> **Nom du rapport :**<br/> Décalage de chapitre </li> <li> **Données contextuelles :**<br/> (a.media.chapter.<br/>offset) </li> <li> **Flux de données :**<br/> S.O. </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.chapter.<br/>offset) </li> <li> **Chemin dʼaccès du champ XDM :**<br/> media.mediaTimed.mediaChapter.chapterAssetViewDetails.offset </li> </ul> |

### Durée du chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> </li> <li> **Clé API :**<br/> media.chapter.length </li> <li> **Obligatoire :**<br/> SDK : Non ; API : Oui. </li> <li> **Type :**<br/> Nombre </li> <li> **Envoyé avec :**<br/> Fermeture de chapitre </li> <li> **Version minimum du SDK :**  1.3 </li> <li> **Exemple de valeur :**<br/> 486 </li><li> **Description :**<br/> durée du chapitre, en secondes.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.chapter.<br/>length) </li> <li> **Heartbeat :**<br/> (l:stream:chapter_length) </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> Classification </li> <li> **Nom du rapport :**<br/> Durée du chapitre </li> <li> **Données contextuelles :**<br/> (a.media.chapter.<br/>length) </li> <li> **Flux de données :**<br/> S.O. </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.chapter.<br/>length) </li> <li> **Chemin dʼaccès du champ XDM :**<br/> media.mediaTimed.mediaChapter.chapterAssetReference.xmpDM:duration </li> </ul> |

### Chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Non </li> <li> **Type :**<br/> Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture de chapitre </li> <li> **Version minimum du SDK :**  1.3 </li> <li> **Exemple de valeur :**<br/> </li><li> **Description :**<br/> ID généré automatiquement du chapitre.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.chapter.<br/>name) </li> <li> **Heartbeat :**<br/> (s:stream:chapter_id) </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> eVar </li> <li> **Expiration :**<br/>&#x200B;À l’ACCÈS </li> <li> **Nom du rapport :**<br/> Chapitre </li> <li> **Données contextuelles :**<br/> (a.media.chapter.<br/>name) </li> <li> **Flux de données :**<br/> videochapter </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.chapter.<br/>name) </li> <li> **Chemin dʼaccès du champ XDM :**<br/> media.mediaTimed.mediaChapter.chapterAssetReference.@id </li> </ul> |

## Mesures de chapitre {#chapter-Metrics}

### Début du chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement  </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Oui </li> <li> **Type :**<br/> Chaîne </li> <li> **Envoyé avec :**<br/> Démarrage de chapitre </li> <li> **Version minimum du SDK :**  1.3 </li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/> nombre de chapitres qui commencent.  **Important** : si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.chapter.<br/>view) </li> <li> **Heartbeat :**<br/> (s:event:<br/>type=chapter_start) </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Démarrages de chapitre</li> <li> **Données contextuelles :**<br/> (a.media.chapter.<br/>view) </li> <li> **Flux de données :**<br/> S.O. </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.chapter.<br/>view) </li> <li> **Chemin dʼaccès du champ XDM :**<br/> media.mediaTimed.chapterCount.value > 0 => &quot;TRUE&quot; </li> </ul> |

### Chapitre terminé

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement  </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Oui </li> <li> **Type :**<br/> Chaîne </li> <li> **Envoyé avec :**<br/> Fermeture de chapitre </li> <li> **Version minimum du SDK :**  1.3</li> <li> **Exemple de valeur :**<br/> TRUE </li><li> **Description :**<br/> nombre de chapitres terminés.  **Important** : si cet événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.chapter.<br/>complete) </li> <li> **Heartbeat :**<br/> (s:event:<br/>type=chapter_complete) </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Fins de chapitre</li> <li> **Données contextuelles :**<br/> (a.media.chapter.<br/>complete) </li> <li> **Flux de données :**<br/> S.O. </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.chapter.<br/>complete) </li> <li> **Chemin dʼaccès du champ XDM :**<br/> media.mediaTimed.mediaChapter.completes.value </li> </ul> |

### Passé sur le chapitre

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé SDK :**<br/> Définie automatiquement  </li> <li> **Clé API :**<br/> S.O. </li> <li> **Obligatoire :**<br/> Oui </li> <li> **Type :**<br/> Nombre </li> <li> **Envoyé avec :**<br/> Fermeture de chapitre </li> <li> **Version minimum du SDK :**  1.3 </li> <li> **Exemple de valeur :**<br/> </li><li> **Description :**<br/> temps passé sur le chapitre.  La valeur sʼaffichera au format horaire (HH:MM:SS) dans Analysis Workspace et Reports &amp; Analytics. Dans les API Flux de données, Data Warehouse et Création de rapports, les valeurs seront exprimées en secondes. <br/>**Date de publication : 13/09/18**   </li> </ul> | <ul> <li> **Adobe Analytics :**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **Heartbeat :**<br/> </li> </ul> | <ul> <li> **Disponible :**<br/> Oui </li> <li> **Variable réservée :**<br/> event </li> <li> **Nom du rapport :**<br/> Temps passé par chapitre</li> <li> **Données contextuelles :**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **Flux de données :**<br/> S.O. </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.chapter.<br/>timePlayed) </li> <li> **Chemin dʼaccès du champ XDM :**<br/> media.mediaTimed.mediaChapter.timePlayed.value </li> </ul> |

## API connexes {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* JavaScript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
