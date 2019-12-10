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

| Segment | Description | Règle |
|---|---|---|
| Type de diffusion multimédia : Tous | Segmente toutes les données de diffusion *multimédia* | « Contenu (ID) présent » |
| Type de diffusion multimédia : Audio | Segmente toutes les données de diffusion *audio* | " Contenu (ID) présent " ET " Type de diffusion multimédia = `audio` " |
| Type de diffusion multimédia : Vidéo | Segmente toutes les données de diffusion *vidéo* | « Contenu (ID) présent » ET « Type de diffusion multimédia= `audio` » |
| Type de contenu multimédia : VoD | Segmente tout le contenu VoD | "Type de contenu = `vod`" |
| Type de contenu multimédia : En direct | Segmente tout le contenu en direct | "Type de contenu = `live`" |
| Type de contenu multimédia : Linéaire | Segmente tout le contenu linéaire | "Type de contenu = `linear`" |
| Type de contenu multimédia : Podcast | Segmente tous les podcasts | "Type de contenu = `podcast`" |
| Type de contenu multimédia : Livre audio | Segmente tous les livres audio | "Type de contenu = `audiobook`" |
| Type de contenu multimédia : AoD | Segmente tout le contenu AoD | "Type de contenu = `aod`" |

