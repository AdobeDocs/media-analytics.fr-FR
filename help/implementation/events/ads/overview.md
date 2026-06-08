---
title: Suivi des publicités
description: Présentation de l’implémentation du suivi des publicités avec le SDK Media.
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PguxKIzAL95WbMl5c0yJq9rYSqZgOGbbAYtxOI4eVOs
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 513
ht-degree: 3%

---


# Suivi des publicités

Le suivi de la lecture des publicités couvre les pauses publicitaires, les démarrages de publicités, les publicités terminées et les publicités ignorées. Utilisez l’API du lecteur multimédia pour identifier les événements clés du lecteur et renseigner les variables publicitaires requises.

## Événements du lecteur

| Événement du lecteur | Action |
| --- | --- |
| Début de la coupure publicitaire | Créer un objet ad break ; appeler AdBreakStart |
| Démarrage de la publicité | Créer un objet publicitaire ; appeler AdStart |
| Publicité terminée | AdComplete de l&#39;appel |
| Annonce publicitaire ignorée | Appel AdSkip |
| Coupure publicitaire terminée | Appeler AdBreakComplete |

## Procédure de mise en œuvre

1. Identifiez le moment où la limite de coupure publicitaire commence, y compris le pré-roll, et créez un objet de coupure publicitaire. Voir [Nom de la coupure publicitaire](/help/implementation/variables/ads/ad-break-name.md) et [Heure de début de la coupure publicitaire](/help/implementation/variables/ads/ad-break-start-time.md) pour obtenir des définitions de champ.
1. Appelez [Début de la coupure publicitaire](/help/implementation/events/ads/ad-break-start.md) pour commencer à suivre la coupure publicitaire.
1. Identifiez le moment où la publicité démarre et créez un objet publicitaire. Pour obtenir la définition des champs, voir [Nom de l’annonce](/help/implementation/variables/ads/ad-name.md), [ID de l’annonce](/help/implementation/variables/ads/ad-id.md), [Longueur de l’annonce](/help/implementation/variables/ads/ad-length.md), [Annonce en position capsule](/help/implementation/variables/ads/ad-in-pod-position.md) et [Nom du lecteur d’annonces](/help/implementation/variables/ads/ad-player-name.md).
1. Vous pouvez éventuellement joindre des métadonnées d’annonce publicitaire standard. Pour connaître les clés disponibles, consultez [Annonceur](/help/implementation/variables/ads/advertiser.md), [Identifiant de campagne](/help/implementation/variables/ads/campaign-id.md), [Identifiant de Creative](/help/implementation/variables/ads/creative-id.md), [URL de Creative](/help/implementation/variables/ads/creative-url.md), [Identifiant d’emplacement](/help/implementation/variables/ads/placement-id.md) et [Identifiant de site](/help/implementation/variables/ads/site-id.md).
1. Appelez [Ad start](/help/implementation/events/ads/ad-start.md) pour commencer à suivre la publicité.
1. Lorsque la lecture de l’annonce est terminée, appelez [Fin de l’annonce](/help/implementation/events/ads/ad-complete.md).
1. Si la visionneuse a ignoré la publicité, appelez [Annonce ignorée](/help/implementation/events/ads/ad-skip.md) au lieu de Annonce terminée.
1. Pour d’autres publicités dans la même coupure publicitaire, répétez les étapes 3 à 7.
1. Une fois la coupure publicitaire terminée, appelez [Fin de la coupure publicitaire](/help/implementation/events/ads/ad-break-complete.md).

>[!IMPORTANT]
>
>**Annonces preroll : ne pas appeler `trackPlay` avant `AdBreakStart` et `AdStart`.** Le premier ping de `play` sur les incréments de contenu principaux [Le contenu démarre](/help/reporting/metrics/content-starts.md). Si `trackPlay` est appelé avant le déclenchement des événements de publicité preroll et que la visionneuse abandonne pendant la publicité, les démarrages de contenu sont incrémentés même si aucun contenu principal n’a jamais été lu. Pour les scénarios de preroll, retardez le `trackPlay` jusqu’à ce que les `AdBreakStart` et `AdStart` aient été envoyés.

>[!NOTE]
>
>La valeur du curseur de lecture signalée pendant la lecture de la publicité représente la position de la visionneuse dans le **contenu principal**, et non dans la publicité. Pour une publicité preroll précédant une vidéo de 10 minutes, le curseur de lecture est `0` tout au long de la publicité. Pour une publicité mid-roll qui démarre à 5 minutes, le curseur de lecture reste à `300` (secondes) pendant la durée de la publicité.

## Problèmes courants

### Appels principaux:play inattendus entre les publicités

Si des appels `main:play` se produisent entre des publicités consécutives, un écart de plus de 250 millisecondes existe entre l’appel AdComplete et le prochain appel AdStart. Lorsque cet écart se produit, Media SDK retourne à l’envoi de pings de contenu principaux, ce qui peut définir la mesure Débuts du contenu plus tôt pour les scénarios de preroll.

**Cause :** aucune information publicitaire n’est définie pour le SDK Media et le lecteur est en cours de lecture. Il attribue donc la durée de l’écart au contenu principal.

**Résolution :** retardez l’appel AdComplete pour chaque publicité (à l’exception de la dernière) plutôt que de l’appeler immédiatement à la fin de la publicité. Traitez les appels par lots comme suit :

* À chaque **lancement de publicité** : si une publicité précédente existe et n’a pas encore été marquée comme terminée, appelez AdComplete *avant* pour la nouvelle publicité.
* À chaque **fin de ressource publicitaire** : n’appelez pas AdComplete immédiatement ; différez-la.
* Lors de la **coupure publicitaire terminée** : appelez AdComplete pour la dernière publicité (si elle n’est pas déjà appelée), puis appelez AdBreakComplete.

Ce modèle garantit qu’AdComplete et le produit AdStart suivant se déclenchent l’un après l’autre, éliminant ainsi tout écart.
