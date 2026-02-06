---
title: Présentation des segments de streaming multimédia
description: Découvrez les segments de création de rapports associés au type de diffusion multimédia, y compris le segment, la description et la règle pour le type de diffusion multimédia.
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: "Streaming Media, Segmentation"
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 89%

---

# Segments de médias{#segments}

Les segments vous permettent d’identifier des sous-ensembles de visiteurs selon des caractéristiques ou des interactions Web. La diffiusion de segments de streaming multimédia vous permet d’identifier le type de flux des visiteurs, par exemple les diffusions audio, en direct ou en podcast. Pour plus d’informations sur les segments Adobe Analytics, voir [À propos des segments et des conteneurs](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html?lang=fr) dans le guide des composants Adobe Analytics.

>[!NOTE]
>
>Ces segments de création de rapports associés au type de diffusion multimédia ont été introduits le 13/09/18 avec le paramètre `streamType`.

| Segment | Description | Composants de |
|---|---|---|
| Type de flux du média : tous | Segmenter toutes les données de diffusion de *média* | « Contenu (ID) présent » |
| Type de flux de média : audio | Segmenter toutes les données de diffusion *audio* | « Contenu (ID) présent » ET « Type de diffusion multimédia = `audio` » |
| Type de flux de média : vidéo | Segmenter toutes les données de diffusion *vidéo* | « Contenu (ID) présent » ET « Type de diffusion multimédia != `audio` » |
| Type de contenu du média : VoD | Segmenter tout le contenu VoD | « Type de contenu = `vod` » |
| Type de contenu du média : actif | Segmenter tout le contenu en direct | « Type de contenu = `live` » |
| Type de contenu du média : linéaire | Segmenter tout le contenu linéaire | « Type de contenu = `linear` » |
| Type de contenu du média : podcast | Segmenter tout le contenu d’un podcast | « Type de contenu = `podcast` » |
| Type de contenu du média : livre audio | Segmenter tout le contenu d’un livre audio | « Type de contenu = `audiobook` » |
| Type de contenu du média : AoD | Segmenter tout le contenu AoD | « Type de contenu = `aod` » |
