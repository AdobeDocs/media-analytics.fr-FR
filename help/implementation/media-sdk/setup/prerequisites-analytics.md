---
title: Conditions préalables pour les implémentations Adobe Analytics uniquement
description: En savoir plus sur les conditions préalables à l’utilisation des médias en flux continu avec les mises en oeuvre d’Adobe Analytics uniquement
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: c4d058ee82f4995f42bfe21c0442004f1f7ea4af
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 58%

---

# Conditions préalables pour les implémentations Adobe Analytics uniquement

Les conditions préalables décrites dans cette section sont spécifiques à la mise en oeuvre de médias en flux continu avec des mises en oeuvre Adobe-Analytics uniquement (si vous n’utilisez pas Edge).

1. **Remplir les conditions préalables générales**<br>
Que vous mettiez en oeuvre des médias en flux continu pour les mises en oeuvre d’Adobe Analytics uniquement ou pour les mises en oeuvre d’Edge, assurez-vous de respecter les conditions suivantes : [conditions préalables générales](/help/getting-started/prereqs.md).

1. **Confirmation que vous disposez d’une mise en oeuvre Adobe Analytics**<br>
Lors de la mise en oeuvre de médias en flux continu avec une mise en oeuvre Analytics uniquement, une mise en oeuvre de base Adobe Analytics est également requise. Pour plus d’informations, voir [Implémentation d’Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=fr).

1. **Obtenir l’URL du serveur de suivi multimédia**<br>
Demandez à votre représentant Adobe Analytics de vous fournir l’URL du serveur de suivi multimédia. Il s’agit de l’URL `collection-api-server` du SDK Mobile, du SDK JavaScript et du serveur de suivi non-collection-api pour Roku. Les noms de domaine pour l’implémentation de l’API sont les suivants : `[your_namespace].hb-api.omtrdc.net`.

1. **Télécharger le SDK Media actuel ou mettre en œuvre les extensions requises**<br>
Selon le chemin d’implémentation, [téléchargez le SDK actuel](/help/getting-started/download-sdks.md) pour les plateformes web, mobiles ou de type OTT. Les extensions requises doivent être implémentées pour activer les chemins d’accès vers les extensions Adobe Analytics for Streaming Media.

1. **Activer les rapports Adobe Analytics**<br>
Pour activer les rapports dans Analytics et afficher le contenu et les données de publicité que vous collectez, vous devez activer les rapports dans Analytics. Voir [Activation des rapports multimédia](/help/reporting/media-reports-enable.md).
