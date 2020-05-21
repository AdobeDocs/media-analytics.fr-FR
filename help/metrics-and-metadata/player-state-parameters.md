---
title: Paramètres d’état du lecteur
description: Cette rubrique décrit les paramètres de suivi de l’état du lecteur.
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 3c24b69265287084393be830193da14ae85cc5ba
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 28%

---


# Paramètres d’état du lecteur{#player-state-parameters}

Cette rubrique présente une liste de données d’état du lecteur qu’Adobe collecte au moyen de variables de solution.

Description des données de tableau :

* **Mise en œuvre :** informations sur les valeurs et les exigences de mise en œuvre.
   * *Clé* : variable, définie soit manuellement dans votre application, soit automatiquement par le SDK Adobe Media.
   * *Obligatoire* : indique si le paramètre est requis pour le suivi vidéo de base.
   * *Type* : indique le type de variable à définir, chaîne ou nombre.
   * *Envoyé avec* : Indique le moment où les données sont envoyées : *Démarrage du média* est l’appel d’analyse envoyé au début du média, *Démarrage de la publicité* est l’appel d’analyse envoyé au début de la publicité, etc. *Fermer* est l’appel d’analyse compilé envoyé directement du serveur de pulsation au serveur d’analyse à la fin de la session multimédia ou de la publicité, du chapitre, etc. Les appels Fermer ne sont pas disponibles dans les appels de paquets réseau.
   * *Version minimum du SDK* : indique la version du SDK dont vous aurez besoin pour accéder au paramètre.
   * *Exemple de valeur* : fournit un exemple d’utilisation de variables courantes.
* **Paramètres réseau** : affiche les valeurs transmises aux serveurs Adobe Analytics ou Heartbeat. Cette colonne indique les noms des paramètres affichés dans les appels réseau générés par les SDK Adobe Media.
* **Reporting :** informations sur la manière de visualiser et d’analyser les données vidéo.
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



## Propriétés d’état du lecteur {#player-state-properties}

Les tableaux des propriétés de suivi de l&#39;état du lecteur sont organisés en cinq sections :

* Plein écran
   * Flux touchés par le plein écran
   * Comptabilisation en plein écran
   * Durée totale du plein écran
* Fermer la légende
   * Flux touchés par le sous-titrage
   * Comptabilisation des sous-titres fermés
   * Sous-titrage total Durée
* Muet
   * Flux touchés par la coupure
   * Comptabilisation en minute
   * Durée totale de la coupure
* Image dans l&#39;image
   * Flux affecté par l’image dans l’image
   * Nombre d&#39;images
   * Durée totale de l&#39;image dans l&#39;image
* Mise au point
   * Flux touchés par In Focus
   * Dans les comptes de mise au point
   * Durée totale de mise au point

### Propriétés du mode Plein écran

#### Flux touchés par le plein écran

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre de flux touchés par le plein écran. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Important** Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.fullscreen.set)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Flux de noms **<br/>de rapport affectés par le plein écran</li> <li> **Données **<br/>contextuelles (a.media.states.fullscreen.set)<br/> </li> <li> **Écran vidéo **<br/>du flux de données</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.a.media.states.fullscreen.set)</li> </ul> |

#### Comptabilisation en plein écran

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre d&#39;affichages d&#39;un plein écran. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Important** Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateful lscreencount)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Nombre de noms **<br/>du rapport en plein écran</li> <li> **Données **<br/>contextuelles (videostateful lscreencount)<br/> </li> <li> **Vidéo **<br/>du fluxde données - statistiques - remonter à l’écran</li> <li> **Audience Manager **<br/>(c_contextdata.videostateful lscreencount)</li> </ul> |



#### Durée totale du plein écran

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionDurée d&#39;affichage d&#39;un écran complet. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Important** Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateful lscreentime)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Nom **<br/>du rapport Durée plein écran</li> <li> **Données **<br/>contextuelles (videostateful lscreentime)<br/> </li> <li> **Flux **<br/>de données videostateful lscreentime</li> <li> **Audience Manager **<br/>(c_contextdata.videostateful lscreentime)</li> </ul> |


### Fermer les propriétés de légende

#### Flux touchés par le sous-titrage

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre de flux touchés par le sous-titrage fermé. This metric is set to 1 only if at least one Closed Caption State occurred during a playback session.<br/> **Important** Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.closedcaptioning.set)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Flux de noms **<br/>de rapport affectés par le sous-titrage fermé</li> <li> **Données **<br/>contextuelles (a.media.states.closedcaptioning.set)<br/> </li> <li> **Vidéostateclosedcaptioning du flux **<br/>de données</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.a.media.states.closedcaptioning.set)</li> </ul> |


#### Comptabilisation des sous-titres fermés

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre de fois où le sous-titrage a été sélectionné. This metric is set to 1 only if at least one Closed Captioning State occurred during a playback session.<br/> **Important** Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateclosedcaptioningcount)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Nombre de sous-titres **<br/>fermés du nom du rapport</li> <li> **Données **<br/>contextuelles (videostateclosedcaptioningcount)<br/> </li> <li> **Flux **<br/>de données videostateclosedcaptioningcount</li> <li> **Audience Manager **<br/>(c_contextdata.videostateclosedcaptioningcount)</li> </ul> |


#### Sous-titrage total Durée

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionDurée pendant laquelle le sous-titrage a été sélectionné. This metric is set to 1 only if at least one Closed Caption State occurred during a playback session.<br/> **Important** Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateclosedcaptioningtime)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Nom **<br/>du rapport Durée du sous-titrage</li> <li> **Données **<br/>contextuelles (videostateclosedcaptioningtime)<br/> </li> <li> **Flux **<br/>de données videostateclosedcaptioningtime</li> <li> **Audience Manager **<br/>(c_contextdata.videostateclosedcaptioningtime)</li> </ul> |


### Propriétés du menu

#### Flux touchés par la coupure

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre de flux touchés par le passage en masse. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **Important** Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.mute.set)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Flux de noms **<br/>de rapport touchés par le silence</li> <li> **Données **<br/>contextuelles (a.media.states.mute.set)<br/> </li> <li> **Vidéo-déclaration **<br/>du flux de données</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.a.media.states.mute.set)</li> </ul> |

#### Comptabilisation en minute

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre de fois où l&#39;option Silence a été sélectionnée. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **Important** Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatemutecount)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Nombre de minutes de nom **<br/>du rapport</li> <li> **Données **<br/>contextuelles (videostatemutecount)<br/> </li> <li> **Vidéo **<br/>du flux de données : statemutecount</li> <li> **Audience Manager **<br/>(c_contextdata.videostatemutecount)</li> </ul> |

#### Durée totale de la coupure

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionDurée pendant laquelle le paramètre Silence a été sélectionné. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **Important** Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatemutetime)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Durée de coupure du nom **<br/>du rapport</li> <li> **Données **<br/>contextuelles (videostatemutetime)<br/> </li> <li> **Flux **<br/>de données videostatemutetime</li> <li> **Audience Manager **<br/>(c_contextdata.videostatemutetime)</li> </ul> |


### Image dans les propriétés de l&#39;image


#### Flux touchés par l&#39;image dans l&#39;image

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre de flux touchés par l&#39;image dans l&#39;image. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **Important** Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.pictureinpicture.set)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Flux de noms **<br/>de rapport affectés par l&#39;image dans l&#39;image</li> <li> **Données **<br/>contextuelles (a.media.states.pictureinpicture.set)<br/> </li> <li> **Flux de données **<br/>videostatepictureinpicture</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.a.media.states.pictureinpicture.set)</li> </ul> |


#### Nombre d&#39;images

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre d&#39;affichages de l&#39;image dans l&#39;image. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **Important** Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatepictureinpicturecount)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Image du nom **<br/>du rapport dans le nombre d&#39;images</li> <li> **Données **<br/>contextuelles (videostatepictureinpicturecount)<br/> </li> <li> **Flux de données **<br/>videostatepictureinpicturecount</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.videostatepictureinpicturecount)</li> </ul> |


#### Durée totale de l&#39;image dans l&#39;image

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionLa durée d&#39;affichage de l&#39;image dans l&#39;image. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **Important** Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatepictureinpicturetime)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Image du nom **<br/>du rapport dans la durée de l&#39;image</li> <li> **Données **<br/>contextuelles (videostatepictureinpicturetime)<br/> </li> <li> **Flux **<br/>de données videostatepictureinpicturetime</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.videostatepictureinpicturetime)</li> </ul> |


### Propriétés de mise au point

#### Flux touchés par In Focus

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre de flux touchés par In Focus. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **Important** Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.infocus.set)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Flux de noms **<br/>de rapport affectés par In Focus</li> <li> **Données **<br/>contextuelles (a.media.states.infocus.set)<br/> </li> <li> **Flux **<br/>de données videostateinfocus</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.a.media.states.infocus.set)</li> </ul> |


#### Dans les comptes de mise au point

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre d&#39;affichages de l&#39;option Mise au point. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **Important** Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateinfocuscount)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Nom **<br/>du rapport dans le décompte des focus</li> <li> **Données **<br/>contextuelles (videostateinfocuscount)<br/> </li> <li> **Flux **<br/>de données videostateinfocuscount</li> <li> **Audience Manager **<br/>(c_contextdata.videostateinfocuscount)</li> </ul> |


#### Durée totale de mise au point

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionLa durée d&#39;affichage de l&#39;option Mise au point. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **Important** Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateinfocustime)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Nom **<br/>Du Rapport Dans La Durée De Mise Au Point</li> <li> **Données **<br/>contextuelles (videostateinfocustime)<br/> </li> <li> **Flux **<br/>de données videostateinfocustime</li> <li> **Audience Manager **<br/>(c_contextdata.videostateinfocustime)</li> </ul> |



## API connexes {#related_apis_section}

BESOIN : Ajouter d’API liens vers des documents :
* Android - [createStateObject](https://need)
* iOS - [createStateObjectWithName](https://need)
* JavaScript - [createStateObject](https://need)
