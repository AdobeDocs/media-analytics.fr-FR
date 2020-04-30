---
title: Segments
description: null
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Segments {#segments}

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

