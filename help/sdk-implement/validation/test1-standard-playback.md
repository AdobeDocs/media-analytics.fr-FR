---
seo-title: Test 1 standard
title: Test 1 standard
uuid: c 4 b 3 fead -1 b 27-484 b-ab 6 a -39 f 1 ae 0 f 03 f 2
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Test 1 : Lecture standard{#test-standard-playback}

Ce cas de test valide la lecture et le séquencement général et est requis dans le formulaire de demande de certification. Pour télécharger le formulaire de demande de certification, cliquez sur[ Formulaire de demande de certification.](cert_req_form_nielsen.docx)

Les mises en œuvre vidéo sont composées des types suivants d’appels de suivi :
* Les appels de démarrage de la vidéo et de la publicité sont envoyés directement au serveur AppMeasurement.
* Les appels de pulsation Media Analytics (MA) sont envoyés au démarrage et toutes les dix secondes sur le serveur de suivi Adobe VA.

>[!NOTE]
>Le suivi vidéo se comportera de le même manière sur toutes les plates-formes, de poste de travail comme mobiles.

Vous devez effectuer et enregistrer les actions dans l’ordre suivant :

1. **Charger la page ou l’application**

   **Serveurs de suivi** (pour tous les sites Web et les applications mobiles) :

   * **AppMeasurement (Adobe Analytics) :** Un serveur de suivi RDC ou CNAME se résolvant sur un serveur RDC est requis pour le service d’identifiant visiteur Experience Cloud. The analytics tracking server should end in `.sc.omtrdc.net` or be a CNAME.

   * **Media Analytics (Heartbeats) :** ce serveur contient toujours le format `[namespace].hb.omtrdc.net`, où `[namespace]` est défini par votre société de connexion et fourni par Adobe.
   Vous devez valider certaines clés et variables universelles pour tous les appels de suivi:

   **Adobe Visitor ID (`mid`) :** La `mid` variable est utilisée pour capturer la valeur définie dans le cookie AMCV. The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. Elle se trouve dans les appels appmeasurement et Media Analytics (MA).

   * **Appel de lecture de Heartbeat**

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
      >On VA Start Calls ( `s:event:type=start`) the `mid` values may not be present. Ceci est normal. They may not appear until the VA Play Calls ( `s:event:type=play`).

      | Paramètre | Valeur (exemple) |
      |---|---|
      | `pev2` | ms_s |


1. **Démarrer le lecteur vidéo**

   Au démarrage du lecteur vidéo, les appels clés sont envoyés dans l’ordre suivant :

   1. Démarrage de Video Analytics
   1. Démarrage de Heartbeat
   1. Démarrage de l’analyse Heartbeat
   Les deux premiers appels ci-dessus contiennent des métadonnées et des variables supplémentaires. For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md)

1. **Afficher la coupure publicitaire si possible**

   * **Démarrage de publicité**
   Au démarrage de la publicité vidéo, les appels clés ci-dessous sont envoyés dans l’ordre suivant :

   1. Démarrage de l’analyse de la publicité vidéo
   1. Démarrage de la publicité Heartbeat
   1. Démarrage de l’analyse de la publicité Heartbeat
   Les deux premiers appels contiennent des métadonnées et des variables supplémentaires. For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md#section_wz3_yff_f2b)

   * **Lecture de la publicité**

      Lors de la lecture de la publicité, des appels Heartbeat sont envoyés au serveur Heartbeat toutes les secondes.

   * **Fin de la publicité**

      Au point 100 % sur une publicité vidéo, un appel de fin Heartbeat est envoyé.



1. **Suspendre la lecture de la publicité pendant 30 secondes si possible.**  **Pause de la publicité**

   Lors de la pause de la publicité, des appels Heartbeat sont envoyés au serveur Heartbeat toutes les secondes.

   >[!NOTE]
   >
   >La valeur du curseur de lecture doit rester constante pendant la mise en pause.

1. **Lire la vidéo de contenu principal pendant 10 minutes sans interruption.** **Lecture du contenu **

   Lors de la lecture du contenu principal standard, des appels Heartbeat sont envoyés au serveur Heartbeat toutes les 10 secondes.

   Remarques :

   * La position du curseur de lecteur doit augmenter de 10 à chaque appel de lecture.
   * La valeur `l:event:duration` représente le nombre de millisecondes qui se sont écoulées depuis le dernier appel de suivi, et doit être plus ou moins constante pour chaque appel de 10 secondes.

      For call parameters and metadata, see [Test call details](../../sdk-implement/validation/test-call-details.md#section_u1l_1gf_f2b) in *Test Call Details*

1. **Suspendre la lecture pendant au moins 30 secondes.** Lors de la pause du lecteur vidéo, les appels d’événement de pause sont envoyés toutes les 10 secondes. Une fois la pause terminée, les événements de lecture doivent reprendre.

1. **Effectuer une recherche dans/parcourir la vidéo** Lors du défilement du curseur de lecture de vidéo, aucun appel de suivi spécial n’est envoyé. Toutefois, lorsque la lecture vidéo reprend après le défilement, la valeur du curseur de lecture doit refléter la nouvelle position dans le contenu principal.

1. **Effectuer une nouvelle lecture de la vidéo (VOD uniquement)** Lorsqu’une vidéo est lue de nouveau, un nouvel ensemble d’appels de démarrage de vidéo doit être envoyé, comme s’il s’agissait d’un nouvel affichage de vidéo.

1. **Afficher la vidéo suivante dans la liste de lecture** Au démarrage de la vidéo suivante dans une liste de lecture, un nouvel ensemble d’appels de démarrage de vidéo doit être envoyé.

1. **Changer de vidéo ou de diffusion** Lors du changement de diffusion en direct, un appel de fin Heartbeat pour la première diffusion ne doit pas être envoyé. Les appels de démarrage de la vidéo et de lecture de la vidéo doivent commencer par le nouveau nom d’affichage et de diffusion et avec les valeurs du curseur de lecture et de durée correctes pour le nouvel affichage.

