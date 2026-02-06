---
title: Création d’un nouveau rapport de débogage
description: Découvrez comment créer un nouveau rapport de débogage.
uuid: 438fde3d-98f9-46d1-9672-75d204361568
exl-id: 047acf35-8c1c-4493-9ee7-e2bad47c351e
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 44%

---

# Création d’un nouveau rapport de débogage{#create-a-new-debug-report}

Pour créer un nouveau rapport de débogage :

1. Dans [!UICONTROL Création d’un nouveau rapport de débogage] sélectionnez les options suivantes :

   ![](assets/create-new-debug-report.png)

1. Renseignez les champs avec les informations suivantes :

   * **Nommer le rapport** - Saisissez le nom et la date du lecteur afin de pouvoir facilement suivre le lecteur pendant la certification et séparer les marques et les plateformes.
   * **Adobe Analytics**

      * [!UICONTROL Nom d’utilisateur] et [!UICONTROL Secret partagé] : ces champs sont facultatifs, mais vous pouvez ajouter vos informations d’identification d’API de services web à Adobe Debug pour afficher les noms des variables et les paramètres des variables pour la suite de rapports.

        Vous pouvez y accéder de l’une des manières suivantes :

         * [!UICONTROL Analytics > Admin > Paramètres De La Société > Services Web]
         * [!UICONTROL Analytics > Admin > Gestion des utilisateurs > Utilisateurs > Paramètres d’utilisateur individuels] Pour créer des informations d’identification d’API de services web pour un nouvel utilisateur, dans [!UICONTROL Gestion des utilisateurs], ajoutez l’utilisateur au groupe d’utilisateurs **Accès au service web**.

      * [!UICONTROL Point d’entrée par défaut] - Les données de ce champ sont fournies par Adobe et ne peuvent pas être modifiées.
      * [!UICONTROL Point d’entrée supplémentaire] - Ajoutez `CNAMES`, si vous les utilisez, pour le suivi de serveur comme `metrics.companyname.com`

   * **Vidéo Heartbeat (Media Analytics)**

      * [!UICONTROL Point d’entrée par défaut] - Les données de ce champ sont fournies par Adobe et ne peuvent pas être modifiées.
      * [!UICONTROL Point d’entrée supplémentaire] - Ajoutez `CNAMES`, si vous les utilisez, pour le suivi de serveur comme, par exemple, `metrics.companyname.com`.
