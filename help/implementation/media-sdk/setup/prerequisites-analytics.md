---
title: Conditions préalables pour les implémentations Adobe Analytics uniquement
description: Découvrez les conditions préalables requises pour utiliser le module complémentaire Adobe Analytics for Streaming Media pour les implémentations Adobe Analytics uniquement
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
TQID: https://experienceleague.adobe.com/falbDtUtqAMtmtQs2jLpEvUKmwvATotVu8njuTNZ09k
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c77ba355-6681-41fe-b719-563d3f507fdb
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: 243
ht-degree: 14%

---

# Conditions préalables pour les implémentations Adobe Analytics uniquement

Les conditions préalables décrites dans cette section sont spécifiques à l’implémentation du module complémentaire Adobe Analytics for Streaming Media pour les implémentations Adobe-Analytics uniquement (lorsque vous n’utilisez pas Edge).

1. **Remplir les conditions préalables générales**<br>
Que vous implémentiez des services de médias en flux continu pour des implémentations Adobe Analytics uniquement ou pour des implémentations Edge, assurez-vous de respecter les [ conditions préalables générales ](/help/getting-started/prereqs.md).

1. **Confirmez que vous disposez d’une implémentation d’Adobe Analytics**<br>
Lors de l’implémentation du module complémentaire Adobe Analytics for Streaming Media pour une implémentation Analytics uniquement, une implémentation de base d’Adobe Analytics est également requise. Pour plus d’informations, voir [Implémentation d’Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=fr).

1. **Obtenir l’URL du serveur de suivi multimédia**<br>
Demandez à votre représentant Adobe Analytics l’URL du serveur de suivi multimédia. Il s’agit de l’URL `collection-api-server` pour Mobile SDK, le SDK JavaScript et le serveur de suivi non-collection-api pour Roku. Les noms de domaine pour l’implémentation de l’API sont les suivants : `[your_namespace].hb-api.omtrdc.net`.

1. **Télécharger le SDK Media actuel ou implémenter les extensions requises**<br>
Selon le chemin d’implémentation, [téléchargez le SDK actuel](/help/getting-started/download-sdks.md) pour les plateformes web, mobiles ou de type OTT. Les extensions requises doivent être mises en œuvre pour activer le module complémentaire Adobe Analytics for Streaming Media.

1. **Activer les rapports Adobe Analytics**<br>
Pour activer les rapports dans Analytics et afficher le contenu et les données de publicité que vous collectez, vous devez activer les rapports dans Analytics. Voir [Activation des rapports multimédia](/help/implementation/media-sdk/setup/media-reports-enable.md).
