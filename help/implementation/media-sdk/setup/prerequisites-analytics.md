---
title: Conditions préalables pour les implémentations Adobe Analytics uniquement
description: En savoir plus sur les conditions préalables à l’utilisation du module complémentaire Collection de médias en flux continu avec les mises en oeuvre d’Adobe Analytics uniquement
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 43%

---

# Conditions préalables pour les implémentations Adobe Analytics uniquement

Les conditions préalables décrites dans cette section sont spécifiques à la mise en oeuvre du module complémentaire Collection de médias en flux continu avec les mises en oeuvre d’Adobe uniquement Analytics (si vous n’utilisez pas Edge).

1. **Remplir les conditions préalables générales**<br>
Que vous mettiez en oeuvre le module complémentaire de collecte de médias en flux continu pour les implémentations d’Adobe Analytics uniquement ou pour les implémentations d’Edge, assurez-vous que vous répondez aux [conditions préalables générales](/help/getting-started/prereqs.md).

1. **Confirmation que vous disposez d’une mise en oeuvre Adobe Analytics**<br>
Lors de la mise en oeuvre du module complémentaire Collection de médias en flux continu avec une mise en oeuvre Analytics uniquement, une mise en oeuvre de base Adobe Analytics est également requise. Pour plus d’informations, voir [Implémentation d’Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=fr).

1. **Obtenir l’URL du serveur de suivi multimédia**<br>
Demandez à votre représentant Adobe Analytics de vous fournir l’URL du serveur de suivi multimédia. Il s’agit de la variable `collection-api-server` URL du SDK Mobile, du SDK JavaScript et du serveur de suivi non-collection-api pour Roku. Les noms de domaine pour l’implémentation de l’API sont les suivants : `[your_namespace].hb-api.omtrdc.net`.

1. **Télécharger le SDK Media actuel ou mettre en œuvre les extensions requises**<br>
Selon le chemin d’implémentation, [téléchargez le SDK actuel](/help/getting-started/download-sdks.md) pour les plateformes web, mobiles ou de type OTT. Les extensions requises doivent être mises en oeuvre pour activer les chemins d’accès des extensions du module complémentaire Collection de médias en flux continu.

1. **Activer les rapports Adobe Analytics**<br>
Pour activer les rapports dans Analytics et afficher le contenu et les données de publicité que vous collectez, vous devez activer les rapports dans Analytics. Voir [Activation des rapports multimédia](/help/reporting/media-reports-enable.md).
