---
seo-title: Test 1 standard
title: Test 1 standard
uuid: c 4 b 3 fead -1 b 27-484 b-ab 6 a -39 f 1 ae 0 f 03 f 2
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

---


# Test 1 : Lecture standard{#test-standard-playback}

Ce cas de test valide la lecture et le séquencement général. Il s'agit d'un élément obligatoire de votre demande de certification.

## Formulaire de demande de certification

**Téléchargez le formulaire de demande de certification ici : = = &gt;**  [Formulaire de demande de certification.](cert_req_form.docx)

## Présentation du test de certification 1

Les implémentations de Media Analytics comprennent deux types d'appels de suivi :
* Appels effectués directement sur votre serveur Adobe Analytics (appmeasurement) : ces appels ont lieu sur les événements « Démarrage multimédia » et « Démarrage de publicité ».
* Appels au serveur Media Analytics (pulsations) : ces appels comprennent les appels à bande et hors bande :
   * In-band : le SDK envoie les appels de lecture minutés ou les « pings » à des intervalles de 10 secondes pendant la lecture du contenu et à intervalles d'une seconde durant les publicités.
   * Hors bande : ces appels peuvent se produire à tout moment et inclure Pause, Mise en mémoire tampon, erreurs, contenu terminé, publicité terminée, etc.

>[!NOTE]
>Le suivi des médias se comporte de la même manière sur toutes les plates-formes.

## Procédure de test

Terminez et enregistrez les actions suivantes (dans l'ordre) :

1. **Charger la page ou l’application**

   **Serveurs de suivi** (pour tous les sites Web et les applications mobiles) :

   * **Serveur Adobe Analytics (appmeasurement) :** un serveur de suivi de CRD ou un CNAME qui résout un serveur de suivi RDC est requis pour le service d'identification des visiteurs Experience Cloud. The Adobe Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Serveur Media Analytics (Heartbeats) :** ce serveur comporte toujours le format « `[namespace].hb.omtrdc.net`, où `[namespace]` spécifie le nom de votre entreprise. Ce nom est fourni par Adobe.
   Vous devez valider certaines variables clés universelles dans tous les appels de suivi :

   **Adobe Visitor ID (`mid`) :** La `mid` variable est utilisée pour capturer la valeur définie dans le cookie AMCV. The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. Elle se trouve dans les appels Adobe Analytics (appmeasurement) et Media Analytics (pulsations).

   * **Appel Démarrer Adobe Analytics**

      | Paramètre | Valeur (exemple) |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Appel de page Web**

      | Paramètre | Valeur (exemple) |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **Appel de cycle de vie**

      | Paramètre | Valeur (exemple) |
      |---|---|
      | `pev2` | ADBINTERNAL:Lifecycle |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Appel de démarrage Media Analytics**

      | Paramètre | Valeur (exemple) |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >Dans les appels Start Media Analytics (`s:event:type=start`), il est possible que `mid` les valeurs ne soient pas présentes. Ceci est normal. Ils peuvent ne pas s'afficher avant les appels de Media Analytics Play ( `s:event:type=play`).

   * **Appel de lecture Media Analytics**

      | Paramètre | Valeur (exemple) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **Démarrage du lecteur multimédia**

   Lorsque le lecteur multimédia démarre, le kit de développement multimédia envoie les appels clés aux deux serveurs dans l'ordre suivant :

   1. Serveur Adobe Analytics - Appel Démarrer
   1. Serveur Media Analytics - Appel Démarrer
   1. Serveur Media Analytics - « Appel de démarrage Adobe Analytics requis »
   Les deux premiers appels ci-dessus contiennent des métadonnées et des variables supplémentaires. Pour les paramètres d'appel et les métadonnées, voir [Test des détails de l'appel.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   Le troisième appel ci-dessus indique au serveur Media Analytics que le kit de développement multimédia demande que l'appel Adobe Analytics Start (`pev2=ms_s`) soit envoyé au serveur Adobe Analytics.

1. **Afficher la coupure publicitaire si possible**

   * **Démarrage de publicité**
   Lorsque la publicité démarre, les appels clés suivants sont envoyés dans l'ordre suivant :

   1. Serveur Adobe Analytics - Appel de démarrage de publicité
   1. Serveur Media Analytics - Appel de démarrage de publicité
   1. Serveur Media Analytics - « Appel de démarrage de publicité Adobe Analytics requis »
   Les deux premiers appels contiennent des métadonnées et des variables supplémentaires. Pour les paramètres d'appel et les métadonnées, voir [Test des détails de l'appel.](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   Le troisième appel indique au serveur Media Analytics que le kit de développement multimédia demande que l'appel de démarrage de publicité Adobe Analytics (`pev2=msa_s`) soit envoyé au serveur Adobe Analytics.

   * **Lecture de la publicité**

      Lors de la lecture de la publicité, le SDK Media Analytics envoie les événements play de type « ad » au serveur Media Analytics toutes les secondes.

   * **Fin de la publicité**

      Au point de 100 % d'une publicité, un appel Complete Analytics Complete doit être envoyé.



1. **Suspendre la lecture de la publicité pendant 30 secondes si possible.**  **Pause de la publicité**

   Lors de la mise en pause de la publicité, les appels de pulsation ou de pulsation Media Analytics sont envoyés par le SDK au serveur Media Analytics toutes les secondes.

   >[!NOTE]
   >
   >La valeur du curseur de lecture doit rester constante pendant la mise en pause.

   Pour les paramètres d'appel et les métadonnées, voir [Test des détails de l'appel.](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **Lecture du contenu principal pendant 10 minutes sans interruption.**  **Lecture du contenu**

   Pendant la lecture du contenu principal, le kit de développement multimédia envoie les pulsations (appels Play) au serveur Media Analytics toutes les 10 secondes.

   Remarques :

   * La position du curseur de lecture doit être incrémentée de 10 avec chaque appel Play.
   * La valeur `l:event:duration` représente le nombre de millisecondes qui se sont écoulées depuis le dernier appel de suivi, et doit être plus ou moins constante pour chaque appel de 10 secondes.

      Pour les paramètres d'appel et les métadonnées, voir [Test des détails de l'appel.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Suspendre la lecture pendant au moins 30 secondes.** Lors de la mise en pause du lecteur multimédia, les appels d'événement de mise en pause sont envoyés par le SDK au serveur Media Analytics toutes les 10 secondes. Après la pause, les événements de lecture reprennent normalement.

   Pour les paramètres d'appel et les métadonnées, voir [Test des détails de l'appel.](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **Recherche/lecture multimédia.** Lors du défilement de la tête de lecture multimédia, aucun appel de suivi spécial n'est envoyé. Toutefois, lorsque la lecture du média reprend après la lecture, la valeur du curseur de lecture doit refléter la nouvelle position dans le contenu principal.

1. **Relecture du support (VOD uniquement).** Lorsque le média est relancé, un nouvel ensemble d'appels Media Start doit être envoyé (comme s'il s'agissait d'un nouveau démarrage).

1. **Affichez le support suivant dans la liste de lecture.** Sur le support média du support suivant dans une liste de lecture, un nouveau jeu d'appels Media Start doit être envoyé.

1. **Basculer le média ou le flux.** Lors du changement de flux en direct, un appel complete Media Analytics pour le premier flux ne doit pas être envoyé. Les appels de démarrage multimédia et les appels Play doivent commencer par le nouveau nom de flux et de flux, ainsi que les valeurs de curseur de lecture et de durée correctes pour le nouveau programme.

