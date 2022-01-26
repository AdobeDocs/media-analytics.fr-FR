---
title: Envoi de données QoE
description: Découvrez comment envoyer des événements avec une clé JSON qoeData.
uuid: 52a02d92-195d-4ce8-8ce3-585ed68969f9
exl-id: 41a20410-78e6-481d-bd5c-0febadb290d8
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '55'
ht-degree: 100%

---

# Envoi de données QoE {#sending-qoe-data}

Chaque événement peut être accompagné d’une clé JSON supplémentaire appelée `qoeData`, qui est placée à côté de la clé `params` dans le corps de la requête JSON.

>[!NOTE]
>
>Reportez-vous aux [schémas de validation JSON](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md) pour vérifier les types de paramètre et déterminer s’ils sont obligatoires ou facultatifs.
