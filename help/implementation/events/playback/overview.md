---
title: Suivi de la lecture
description: Découvrez les événements de lecture et comment implémenter le suivi de la lecture, de la mise en pause, de la mise en mémoire tampon, du ping et des changements de débit.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Cc5T13Z1S15MyG-CxpxMoHX-ckULmIe0dfUOe7650DE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889beid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 231
ht-degree: 2%

---


# Suivi de la lecture

Les événements de lecture effectuent le suivi des transitions d’état dans le lecteur multimédia tout au long d’une session. Ils constituent le cœur du flux d’événements et s’appliquent à tout type de contenu.

## Événements du lecteur

| Événement du lecteur | Action |
| --- | --- |
| Lectures ou reprises de médias | Lecture d’appel |
| Pauses du média | Début de la pause de l’appel |
| La mise en mémoire tampon commence | Début de la mémoire tampon d&#39;appel |
| Fin de la mise en mémoire tampon | Lecture d’appel |
| Changements de débit | Changement de débit d’appel |
| Timer se déclenche | Ping d&#39;appel |

## Procédure de mise en œuvre

1. **Appeler [Lire](play.md)** après [Début de session](../session/session-start.md) lorsque la première image de contenu s’affiche à l’écran. Envoyez également une lecture lorsque la lecture reprend après une pause ou un blocage de la mémoire tampon. Il n’existe pas d’événement de reprise distinct.
1. **Appel [Démarrage de la pause](pause-start.md)** lorsque l’utilisateur met la lecture en pause. Envoyer la lecture lorsque la lecture reprend.
1. **Appel [Début de la mémoire tampon](buffer-start.md)** lorsque le lecteur se bloque en attente de données. Sur les API basées sur XDM, la fin de la mémoire tampon est déduite lorsque vous envoyez l’événement de lecture suivant. Sur Mobile SDK, appelez également `BufferComplete` explicitement lors de la résolution de la mise en mémoire tampon.
1. **Appel [Ping](ping.md)** toutes les 10 secondes pendant la lecture du contenu principal et toutes les secondes pendant la lecture des publicités. Ping maintient la session active et enregistre les mouvements du curseur de lecture. Les SDK mobiles envoient automatiquement les pings ; toutes les autres plateformes doivent les envoyer manuellement.
1. **Appeler [Modification du débit](bitrate-change.md)** chaque fois que le lecteur négocie un nouveau débit. Incluez les données QoE actuelles (débit, images par seconde, images perdues) afin que le serveur principal puisse calculer le [débit moyen](/help/reporting/metrics/average-bitrate.md) et les mesures de qualité associées.
