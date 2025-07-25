---
title: Conditions préalables pour les implémentations Adobe Analytics uniquement
description: Découvrez les conditions préalables requises pour utiliser Streaming Media Collection avec les implémentations Adobe Analytics uniquement
feature: Streaming Media, Workspace Basics
role: User, Admin, Data Engineer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: 0b0b4a373b15191dcb37dc436413f68cdc70768e
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 44%

---

# Conditions préalables pour les implémentations Adobe Analytics uniquement

Les conditions préalables décrites dans cette section sont spécifiques à l’implémentation de la collecte de médias en flux continu avec des implémentations Adobe-Analytics uniquement (lorsque vous n’utilisez pas Edge).

1. **Remplir les conditions préalables générales**<br>
Que vous implémentiez Streaming Media Collection pour des implémentations Adobe Analytics uniquement ou pour des implémentations Edge, assurez-vous de respecter les [ conditions préalables générales ](/help/getting-started/prereqs.md).

1. **Confirmez que vous disposez d’une implémentation d’Adobe Analytics**<br>
Lors de l’implémentation de Streaming Media Collection avec une implémentation Analytics uniquement, une implémentation de base d’Adobe Analytics est également requise. Pour plus d’informations, voir [Implémentation d’Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=fr).

1. **Obtenir l’URL du serveur de suivi multimédia**<br>
Demandez à votre représentant Adobe Analytics de vous fournir l’URL du serveur de suivi multimédia. Il s’agit de l’URL `collection-api-server` pour Mobile SDK, le SDK JavaScript et le serveur de suivi non-collection-api pour Roku. Les noms de domaine pour l’implémentation de l’API sont les suivants : `[your_namespace].hb-api.omtrdc.net`.

1. **Télécharger le SDK Media actuel ou mettre en œuvre les extensions requises**<br>
Selon le chemin d’implémentation, [téléchargez le SDK actuel](/help/getting-started/download-sdks.md) pour les plateformes web, mobiles ou de type OTT. Les extensions requises doivent être mises en œuvre pour activer les chemins d’accès vers les extensions Streaming Media Collection.

1. **Activer les rapports Adobe Analytics**<br>
Pour activer les rapports dans Analytics et afficher le contenu et les données de publicité que vous collectez, vous devez activer les rapports dans Analytics. Voir [Activation des rapports multimédia](/help/reporting/media-reports-enable.md).
