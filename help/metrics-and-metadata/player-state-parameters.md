---
title: Paramètres d’état du lecteur
description: Cette rubrique décrit les paramètres de suivi de l’état du lecteur.
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 1b48565bcc5c9a87e5fabbc906049ab791bf89cc
workflow-type: tm+mt
source-wordcount: '2236'
ht-degree: 28%

---


# Paramètres d’état du lecteur{#player-state-parameters}

Cette rubrique présente une liste de données d’état du lecteur que Adobe collecte au moyen de variables de solution.

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

Les fonctionnalités de suivi de l’état du lecteur peuvent être associées à un flux audio ou vidéo. Les mesures de suivi normalisées de l’état du lecteur sont stockées en tant que variables de solution. Les normes sont les suivantes : fullScreen, mute, closeCaption, pictureInPicture et inFocus.

### Propriétés du mode Plein écran

#### Diffusions touchées par le plein écran

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre de flux touchés par le plein écran. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Important** <br/> Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.fullscreen.set)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Flux de noms **<br/>de rapport affectés par le plein écran</li> <li> **Données **<br/>contextuelles (a.media.states.fullscreen.set)<br/> </li> <li> **Flux **<br/>de données media.states.fullscreen</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.a.media.states.fullscreen.set)</li> </ul> |

#### Nombre de plein écrans

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre d&#39;affichages d&#39;un plein écran. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Important **<br/>Si ce événement est défini, le nombre est égal au nombre de fois où la vidéo était à l’état Plein écran. Si cet événement n’est pas défini, aucune valeur n’est envoyée.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.fullscreen.count)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Nombre de noms **<br/>du rapport en plein écran</li> <li> **Données **<br/>contextuelles (media.states.fullscreen.count)<br/> </li> <li> **Flux **<br/>de données media.states.fullscreen.count</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.media.states.fullscreen.count)</li> </ul> |



#### Durée totale en plein écran

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionDurée d&#39;affichage d&#39;un écran complet. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Important **<br/>Si ce événement est défini, la durée correspond à la durée pendant laquelle la vidéo se trouvait à l’état Plein écran. Si cet événement n’est pas défini, aucune valeur n’est envoyée.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.fullscreen.time)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Nom **<br/>du rapport Plein écran Durée totale</li> <li> **Données **<br/>contextuelles (media.states.fullscreen.time)<br/> </li> <li> **Flux **<br/>de données media.states.fullscreen.time</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.media.states.fullscreen.time)</li> </ul> |


### Fermer les propriétés de légende

#### Diffusions touchées par le sous-titrage codé

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre de flux touchés par le sous-titrage fermé. This metric is set to 1 only if at least one Closed Caption State occurred during a playback session.<br/> **Important** <br/> Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.closedcaptioning.set)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Flux de noms **<br/>de rapport affectés par le sous-titrage fermé</li> <li> **Données **<br/>contextuelles (a.media.states.closedcaptioning.set)<br/> </li> <li> **Flux **<br/>de données media.states.closedcaptioning</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.a.media.states.closedcaptioning.set)</li> </ul> |


#### Nombre de sous-titrages codés

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre d’affichages du sous-titrage fermé. This metric is set to 1 only if at least one Closed Captioning State occurred during a playback session.<br/> **Important **<br/>Si ce événement est défini, le nombre est égal au nombre de fois où la vidéo se trouvait à l’état Sous-titrage fermé. Si cet événement n’est pas défini, aucune valeur n’est envoyée.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(C19)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Nombre de sous-titres **<br/>fermés du nom du rapport</li> <li> **Données **<br/>contextuelles (media.states.closedcaptioning.count)<br/> </li> <li> **Flux **<br/>de données media.states.closedcaptioning.count</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.media.states.closedcaptioning.count)</li> </ul> |


#### Durée totale du sous-titrage codé

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionDurée d’affichage du sous-titrage fermé. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Important **<br/>Si ce événement est défini, la durée correspond à la durée pendant laquelle la vidéo se trouvait à l’état Sous-titrage fermé. Si cet événement n’est pas défini, aucune valeur n’est envoyée.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.closedcaptioning.time)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Nom **<br/>du rapport Sous-titrage total Durée</li> <li> **Données **<br/>contextuelles (media.states.closedcaptioning.time)<br/> </li> <li> **Flux **<br/>de données media.states.closedcaptioning.time</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.media.states.closedcaptioning.time)</li> </ul> |


### Propriétés du menu

#### Diffusions touchées par le mode muet

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre de flux touchés par le passage en masse. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **Important** <br/> Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.mute.set)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Flux de noms **<br/>de rapport touchés par le silence</li> <li> **Données **<br/>contextuelles (a.media.states.mute.set)<br/> </li> <li> **Flux **<br/>de données media.states.mute</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.a.media.states.mute.set)</li> </ul> |

#### Nombre d’instances muettes

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre d&#39;affichages du paramètre Silence. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **Important **<br/>Si ce événement est défini, le nombre est égal au nombre de fois où la vidéo était à l’état Muet. Si cet événement n’est pas défini, aucune valeur n’est envoyée.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.mute.count)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Nombre de minutes de nom **<br/>du rapport</li> <li> **Données **<br/>contextuelles (media.states.mute.count)<br/> </li> <li> **Flux **<br/>de données media.states.mute.count</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.media.states.mute.count)</li> </ul> |

#### Durée totale du mode muet

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionDurée d&#39;affichage du paramètre Silence. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **Important **<br/>Si ce événement est défini, la durée correspond à la durée pendant laquelle la vidéo était à l’état Muet. Si cet événement n’est pas défini, aucune valeur n’est envoyée.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.mute.time)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Nom **<br/>du rapport - Durée totale en demi-coupure</li> <li> **Données **<br/>contextuelles (media.states.mute.time)<br/> </li> <li> **Flux **<br/>de données media.states.mute.time</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.media.states.mute.time)</li> </ul> |


### Image dans les propriétés de l&#39;image


#### Flux touchés par l&#39;image dans l&#39;image

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre de flux touchés par l&#39;image dans l&#39;image. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **Important** <br/> Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.pictureinpicture.set)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Flux de noms **<br/>de rapport affectés par l&#39;image dans l&#39;image</li> <li> **Données **<br/>contextuelles (a.media.states.pictureinpicture.set)<br/> </li> <li> **Flux **<br/>de données media.states.pictureinpicture</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.a.media.states.pictureinpicture.set)</li> </ul> |


#### Nombre d&#39;images

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre d&#39;affichages de l&#39;image dans l&#39;image. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **Important**<br/> Si ce événement est défini, le nombre est égal au nombre de fois où la vidéo se trouvait dans l’état Image de l’image. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.pictureinpicture.count)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Image du nom **<br/>du rapport dans le nombre d&#39;images</li> <li> **Données **<br/>contextuelles (media.states.pictureinpicture.count)<br/> </li> <li> **Flux **<br/>de données media.states.pictureinpicture.count</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.media.states.pictureinpicture.count)</li> </ul> |


#### Durée totale de l&#39;image dans l&#39;image

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionLa durée d&#39;affichage de l&#39;image dans l&#39;image. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **Important**<br/> Si ce événement est défini, la durée correspond à la durée pendant laquelle la vidéo se trouvait dans l’état Image dans l’image. Si cet événement n’est pas défini, aucune valeur n’est envoyée..   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.pictureinpicture.time)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Image du nom **<br/>du rapport dans la durée totale de l&#39;image</li> <li> **Données **<br/>contextuelles (media.states.pictureinpicture.time)<br/> </li> <li> **Flux **<br/>de données media.states.pictureinpicture.time</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.media.states.pictureinpicture.time)</li> </ul> |


### Propriétés de mise au point

#### Diffusions touchées par le mode « In Focus » (En point de mire)

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre de flux touchés par In Focus. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **Important** <br/> Si ce événement est défini, la seule valeur possible est TRUE. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.infocus.set)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Flux de noms **<br/>de rapport affectés par In Focus</li> <li> **Données **<br/>contextuelles (a.media.states.infocus.set)<br/> </li> <li> **Flux **<br/>de données media.states.infocus</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.a.media.states.infocus.set)</li> </ul> |


#### Nombre d’instances en mode « In Focus »

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionNombre d&#39;affichages de l&#39;option Mise au point. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **Important **<br/>Si ce événement est défini, le nombre est égal au nombre de fois où la vidéo était à l’état Mise au point. Si cet événement n’est pas défini, aucune valeur n’est envoyée.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.infocus.count)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Nom **<br/>du rapport dans le décompte des focus</li> <li> **Données **<br/>contextuelles (media.states.infocus.count)<br/> </li> <li> **Flux **<br/>de données media.states.infocus.count</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.media.states.infocus.count)</li> </ul> |


#### Durée totale du mode « In Focus »

|   Mise en œuvre   | Paramètres réseau | Création de rapports |
| --- | --- | --- |
| <ul> <li> **Clé&#x200B;**<br/>SDK définie automatiquement</li> <li> **Clé&#x200B;**<br/>API N/A</li> <li> **Non requis **<br/></li> <li> **Numéro de type **<br/></li> <li> **Envoyé avec **<br/>fermeture du média</li> <li> **Version SDK Version **<br/>3.0</li> <li> **Exemple de valeur **<br/>TRUE</li><li> ****<br/>DescriptionLa durée d&#39;affichage de l&#39;option Mise au point. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **Important**<br/> Si ce événement est défini, la durée correspond à la durée pendant laquelle la vidéo était à l’état Mise au point. Si cet événement n’est pas défini, aucune valeur n’est envoyée.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.infocus.time)<br/></li> <li> **Pulsation **<br/>N/A</li> </ul> | <ul> <li> **Disponible **<br/>Oui</li> <li> **événement de variables **<br/>réservées</li> <li> **Nom **<br/>du rapport dans la durée totale de mise au point</li> <li> **Données **<br/>contextuelles (media.states.infocus.time)<br/> </li> <li> **Flux **<br/>de données media.states.infocus.time</li> <li> **Gestionnaire **<br/>d’Audiences (c_contextdata.media.states.infocus.time)</li> </ul> |

## Liste de propriétés pour les identités XDM

Les données stockées dans Analytics peuvent être utilisées à n’importe quel usage et les mesures d’état du lecteur peuvent être importées dans la plateforme d’expérience Adobe à l’aide de XDM et utilisées avec les analyses de parcours du client.

| Player State, propriété | Correspondance |
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
* JavaScript - [createStateObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)
