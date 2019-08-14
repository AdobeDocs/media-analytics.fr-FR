---
seo-title: Test 1 standard
title: Test 1 standard
uuid: c 4 b 3 fead -1 b 27-484 b-ab 6 a -39 f 1 ae 0 f 03 f 2
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# Test 1 : Lecture standard{#test-standard-playback}

Ce cas de test valide la lecture et le séquencement général. Il est obligatoire dans le Formulaire de demande de certification.

**Téléchargez le formulaire de demande de certification ici : = = &gt;**  [Formulaire de demande de certification.](cert_req_form.docx)

Les implémentations de médias sont composées des types suivants d'appels de suivi :
* Les appels Media et Ad Start sont envoyés directement au serveur appmeasurement (Adobe Analytics).
* Les appels de pulsation Media Analytics sont envoyés au démarrage et toutes les dix secondes (pour le contenu) ou une seconde (pour les publicités) au serveur de suivi Media Analytics.

>[!NOTE]
>Le suivi des médias se comporte de la même manière sur toutes les plates-formes.

Vous devez terminer et enregistrer ces actions dans l'ordre suivant :

1. **Charger la page ou l’application**

   **Serveurs de suivi** (pour tous les sites Web et les applications mobiles) :

   * **Appmeasurement (Adobe Analytics) -** Un serveur de suivi de CRD ou un CNAME qui résout un serveur de suivi RDC est requis pour le service d'identification des visiteurs Experience Cloud. The Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Media Analytics (Heartbeats) :** ce serveur comporte toujours le format « `[namespace].hb.omtrdc.net`, où `[namespace]` spécifie le nom de votre entreprise. Ce nom est fourni par Adobe.
   Vous devez valider certaines variables clés universelles dans tous les appels de suivi :

   **Adobe Visitor ID (`mid`) :** La `mid` variable est utilisée pour capturer la valeur définie dans le cookie AMCV. The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. Elle est trouvée dans les appels appmeasurement et Media Analytics.

   * **Appel de lecture Media Analytics**

      | Paramètre | Valeur (exemple) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |

   * **Appel de démarrage de Media Analytics**

      | Paramètre | Valeur (exemple) |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Appel de page de site Web**

      | Paramètre | Valeur (exemple) |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **Appel de cycle de vie**

      | Paramètre | Valeur (exemple) |
      |---|---|
      | `pev2` | ADBINTERNAL:Lifecycle |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Appel de démarrage de Heartbeat**

      | Paramètre | Valeur (exemple) |
      |---|---|
      | `s:event:type` | start |

   * **Appel de démarrage de VA**

      >[!NOTE]
      >
      >On VA Start Calls (`s:event:type=start`) the `mid` values may not be present. Ceci est normal. They may not appear until the VA Play Calls ( `s:event:type=play`).

      | Paramètre | Valeur (exemple) |
      |---|---|
      | `pev2` | ms_s |


1. **Démarrage du lecteur multimédia**

   Lorsque le lecteur multimédia démarre, les appels clés sont envoyés dans l'ordre suivant :

   1. Démarrage de Media Analytics
   1. Démarrage de Heartbeat
   1. Démarrage de l’analyse Heartbeat
   Les deux premiers appels ci-dessus contiennent des métadonnées et des variables supplémentaires. Pour les paramètres d'appel et les métadonnées, voir [Test des détails de l'appel.](/help/sdk-implement/validation/test-call-details.md)

1. **Afficher la coupure publicitaire si possible**

   * **Démarrage de publicité**
   Lorsque la publicité multimédia démarre, les appels clés suivants sont envoyés dans l'ordre suivant :

   1. Démarrage des analyses de publicité multimédia
   1. Démarrage de la publicité Heartbeat
   1. Démarrage de l’analyse de la publicité Heartbeat
   Les deux premiers appels contiennent des métadonnées et des variables supplémentaires. Pour les paramètres d'appel et les métadonnées, voir [Test des détails de l'appel.](/help/sdk-implement/validation/test-call-details.md#section_wz3_yff_f2b)

   * **Lecture de la publicité**

      Lors de la lecture de la publicité, des appels Heartbeat sont envoyés au serveur Heartbeat toutes les secondes.

   * **Fin de la publicité**

      Au point de 100 % sur une publicité multimédia, un appel Heartbeat Complete est envoyé.



1. **Suspendre la lecture de la publicité pendant 30 secondes si possible.**  **Pause de la publicité**

   Lors de la pause de la publicité, des appels Heartbeat sont envoyés au serveur Heartbeat toutes les secondes.

   >[!NOTE]
   >
   >La valeur du curseur de lecture doit rester constante pendant la mise en pause.

1. **Lecture du contenu principal de contenu pendant 10 minutes sans interruption.**  **Lecture du contenu**

   Pendant la lecture du contenu principal, les appels de pulsation sont envoyés au serveur Media Analytics toutes les dix secondes.

   Remarques :

   * La position du curseur de lecteur doit augmenter de 10 à chaque appel de lecture.
   * La valeur `l:event:duration` représente le nombre de millisecondes qui se sont écoulées depuis le dernier appel de suivi, et doit être plus ou moins constante pour chaque appel de 10 secondes.

      Pour les paramètres d'appel et les métadonnées, voir [Test des détails de l'appel.](/help/sdk-implement/validation/test-call-details.md#section_u1l_1gf_f2b)

1. **Suspendre la lecture pendant au moins 30 secondes.** Lors de la mise en pause du lecteur multimédia, les appels d'événement de pause sont envoyés toutes les 10 secondes. Une fois la pause terminée, les événements de lecture doivent reprendre.

1. **Recherche/lecture multimédia.** Lors du défilement de la tête de lecture multimédia, aucun appel de suivi spécial n'est envoyé, toutefois, lorsque la lecture du média reprend après la lecture de la valeur du curseur de lecture, la valeur du curseur de lecture doit refléter la nouvelle position dans le contenu principal.

1. **Relecture du support (VOD uniquement).** Lorsque le média est relancé, un nouveau jeu d'appels de démarrage multimédia doit être envoyé, comme s'il s'agissait d'une vue de média Fresh.

1. **Affichez le support suivant dans la liste de lecture.** Lors du début du média suivant dans une liste de lecture, un nouveau jeu d'appels de démarrage multimédia doit être envoyé.

1. **Basculer le média ou le flux.** Lors du changement de diffusion en direct, un appel de fin Heartbeat pour la première diffusion ne doit pas être envoyé. Les appels de démarrage de média et les appels play play doivent commencer par le nouveau nom et le nouveau nom de flux et avec les valeurs de curseur de lecture et de durée correctes pour le nouveau programme.

