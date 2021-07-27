---
title: Présentation des segments de streaming multimédia
description: « Découvrez les segments de création de rapports associés au type de streaming multimédia, y compris le segment, la description et la règle pour le type de diffusion de streaming multimédia. »
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: « Media Analytics, Segmentation »
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: ht
source-wordcount: '207'
ht-degree: 100%

---

# Segments{#segments}

Les segments vous permettent d’identifier des sous-ensembles de visiteurs selon des caractéristiques ou des interactions Web. La diffiusion de segments de streaming multimédia vous permet d’identifier le type de flux des visiteurs, par exemple les diffusions audio, en direct ou en podcast. Pour plus d’informations sur les segments Adobe Analytics, voir [À propos des segments et des conteneurs](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html?lang=fr) dans le guide des composants Adobe Analytics.

>[!NOTE]
>
>Ces segments de création de rapports associés au type de diffusion multimédia ont été introduits le 13/09/18 avec le paramètre `streamType`.

| Segment | Description | Composants de |
|---|---|---|
| Type de flux du média : tous | Segmenter toutes les données de diffusion de *média* | &quot;Le contenu (ID) existe&quot; |
| Type de flux de média : audio | Segmenter toutes les données de diffusion *audio* | &quot;Contenu (ID) présent&quot; ET &quot;Type de diffusion multimédia = `audio`&quot; |
| Type de flux de média : vidéo | Segmenter toutes les données de diffusion *vidéo* | &quot;Contenu (ID) présent&quot; ET &quot;Type de diffusion multimédia != `audio`&quot; |
| Type de contenu du média : VoD | Segmenter tout le contenu VoD | &quot;Type de contenu = `vod`&quot; |
| Type de contenu du média : actif | Segmenter tout le contenu en direct | &quot;Type de contenu = `live`&quot; |
| Type de contenu du média : linéaire | Segmenter tout le contenu linéaire | &quot;Type de contenu = `linear`&quot; |
| Type de contenu du média : podcast | Segmenter tout le contenu d’un podcast | &quot;Type de contenu = `podcast`&quot; |
| Type de contenu du média : livre audio | Segmenter tout le contenu d’un livre audio | &quot;Type de contenu = `audiobook`&quot; |
| Type de contenu du média : AoD | Segmenter tout le contenu AoD | &quot;Type de contenu = `aod`&quot; |
