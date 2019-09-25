---
seo-title: Test 1 Lecture standard
title: Test 1 Lecture standard
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

---


# Test 1 : Lecture standard{#test-standard-playback}

This test case validates general playback and sequencing. It is a required element of your certification request.

## Formulaire de demande de certification

**Téléchargez le formulaire de demande de certification ici : ==&gt;** Formulaire de demande de [certification.](cert_req_form.docx)

## Certification Test 1 overview

Media Analytics implementations include two types of tracking calls:
* Calls made directly to your Adobe Analytics (AppMeasurement) server - These calls occur on "Media Start" and "Ad Start" events.
* Appels effectués sur le serveur Media Analytics (pulsations) - Ces appels comprennent les appels in-band et out-of-band :
   * In-band - The SDK sends timed play calls or "pings" at 10-second intervals during content playback, and at one-second intervals during ads.
   * Out-of-band - These calls can happen at any point, and include Pause, Buffering, errors, content complete, ad complete, etc.

>[!NOTE]
>Media tracking behaves the same across all platforms.

## Test procedure

Complete and record the following actions (in order):

1. **Charger la page ou l’application**

   **Serveurs de suivi** (pour tous les sites Web et les applications mobiles) :

   * **Serveur Adobe Analytics (AppMeasurement) :** un serveur de suivi de CRD ou un CNAME qui se résout en serveur de suivi de CRD est requis pour le service d’identification des visiteurs d’Experience Cloud. The Adobe Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Media Analytics (Heartbeats) server - This server always has the format "", where  specifies your company name.**`[namespace].hb.omtrdc.net``[namespace]` This name is provided by Adobe.
   You need to validate certain key variables that are universal across all tracking calls:

   **`mid`Identifiant visiteur Adobe (**) : La `mid` variable permet de capturer la valeur définie dans le cookie AMCV. The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. Elle se trouve dans les appels Adobe Analytics (AppMeasurement) et Media Analytics (pulsations).

   * **Appel Adobe Analytics Start**

      | Paramètre | Valeur (exemple) |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Appel Page du site Web**

      | Paramètre | Valeur (exemple) |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **Appel de cycle de vie**

      | Paramètre | Valeur (exemple) |
      |---|---|
      | `pev2` | ADBINTERNAL:Lifecycle |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Appel Media Analytics Start**

      | Paramètre | Valeur (exemple) |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >Sur les appels Media Analytics Start (`s:event:type=start`), les `mid` valeurs peuvent ne pas être présentes. Ceci est normal. Il se peut qu’ils n’apparaissent pas avant les appels Media Analytics Play ( `s:event:type=play`).

   * **Appel Media Analytics Play**

      | Paramètre | Valeur (exemple) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **Démarrage du lecteur multimédia**

   Lorsque le lecteur multimédia démarre, le SDK Media envoie les appels de clés aux deux serveurs dans l’ordre suivant :

   1. Serveur Adobe Analytics - Appel de démarrage
   1. Serveur Media Analytics - Appel de démarrage
   1. Serveur Media Analytics - "Appel Adobe Analytics Start demandé"
   Les deux premiers appels ci-dessus contiennent des métadonnées et des variables supplémentaires. Pour les paramètres d’appel et les métadonnées, voir [Test des détails d’appel.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   Le troisième appel ci-dessus indique au serveur Media Analytics que le SDK Media a demandé que l’appel Adobe Analytics Start (`pev2=ms_s`) soit envoyé au serveur Adobe Analytics.

1. **Afficher la coupure publicitaire si possible**

   * **Démarrage de publicité**
   Lorsque la publicité démarre, les appels clés suivants sont envoyés dans l’ordre suivant :

   1. Serveur Adobe Analytics - Appel Ad Start
   1. Serveur Media Analytics - Appel Ad Start
   1. Serveur Media Analytics - "Appel Adobe Analytics Ad Start demandé"
   Les deux premiers appels contiennent des métadonnées et des variables supplémentaires. Pour les paramètres d’appel et les métadonnées, voir [Test des détails d’appel.](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   Le troisième appel indique au serveur Media Analytics que le SDK multimédia a demandé que l’appel Adobe Analytics Ad Start (`pev2=msa_s`) soit envoyé au serveur Adobe Analytics.

   * **Lecture de la publicité**

      Pendant la lecture de la publicité, le SDK Media Analytics envoie des événements play de type "publicité" au serveur Media Analytics toutes les secondes.

   * **Fin de la publicité**

      Au point 100 % d’une publicité, un appel de fin d’analyse des médias doit être envoyé.



1. **Suspendre la lecture de la publicité pendant 30 secondes si possible.**  **Pause de la publicité**

   Pendant la Pause de la publicité, les appels de pulsation ou de ping d’Analytics des médias sont envoyés par le SDK au serveur Media Analytics toutes les secondes.

   >[!NOTE]
   >
   >The playhead value should remain constant during the pause.

   Pour les paramètres d’appel et les métadonnées, voir [Test des détails d’appel.](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **Lire le contenu principal pendant 10 minutes sans interruption.**  **Lecture du contenu**

   Lors de la lecture du contenu principal, le SDK multimédia envoie des pulsations (appels de lecture) au serveur Media Analytics toutes les 10 secondes.

   Remarques :

   * La position du curseur de lecture doit être incrémentée de 10 avec chaque appel Play.
   * La valeur `l:event:duration` représente le nombre de millisecondes qui se sont écoulées depuis le dernier appel de suivi, et doit être plus ou moins constante pour chaque appel de 10 secondes.

      Pour les paramètres d’appel et les métadonnées, voir [Test des détails d’appel.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Suspendre la lecture pendant au moins 30 secondes.** Lors de la mise en pause du lecteur multimédia, les appels d’événement pause sont envoyés par le SDK au serveur Media Analytics toutes les 10 secondes. Après la pause, les événements de lecture reprennent normalement.

   Pour les paramètres d’appel et les métadonnées, voir [Test des détails d’appel.](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **Recherchez/nettoyez le média.** Lors du défilement du curseur de lecture multimédia, aucun appel de suivi spécial n’est envoyé, cependant, lorsque la lecture du média reprend après le défilement, la valeur du curseur de lecture doit refléter la nouvelle position dans le contenu principal.

1. **Lecture du média (VOD uniquement).** Lorsque le média est relu, un nouvel ensemble d’appels Media Start doit être envoyé (comme s’il s’agissait d’un nouveau départ).

1. **Afficher le média suivant dans la liste de lecture.** Au début du média suivant dans une liste de lecture, un nouvel ensemble d’appels Media Start doit être envoyé.

1. **Changer de média ou de flux.** Lorsque vous changez de flux en direct, un appel complete Media Analytics pour le premier flux ne doit pas être envoyé. Les appels Media Start et Play doivent commencer par le nouveau nom du programme et du flux, ainsi que par les valeurs de curseur de lecture et de durée correctes pour le nouveau programme.

