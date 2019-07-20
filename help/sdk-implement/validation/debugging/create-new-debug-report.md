---
seo-title: Création d’un nouveau rapport de débogage
title: Création d’un nouveau rapport de débogage
uuid: 438 fde 3 d -98 f 9-46 d 1-9672-75 d 204361568
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Création d’un nouveau rapport de débogage{#create-a-new-debug-report}

Pour créer un nouveau rapport de débogage :

1. In [!UICONTROL Create New Debug Report] select the following:

   ![](assets/create-new-debug-report.png)

1. Renseignez les champs avec les informations suivantes :

   * **Nommer le rapport** : Entrez le nom et la date du lecteur afin de pouvoir facilement suivre le lecteur pendant la certification et conserver les marques et les plates-formes distinctes.
   * **Adobe Analytics**

      * [!UICONTROL Nom d’utilisateur] et [!UICONTROL Secret partagé] : Ces champs sont facultatifs, mais vous pouvez ajouter vos informations d’identification de l’API de services Web à Adobe Debug pour afficher les noms de variable et les paramètres de variable pour la suite de rapports.

         L’accès peut s’effectuer de l’une des manières suivantes :

         * [!UICONTROL Analytics &gt; Admin &gt; Paramètres de la société &gt; Services Web]
         * [!UICONTROL Analytics &gt; Administration &gt; Gestion des utilisateurs &gt; Utilisateurs &gt; Paramètres d’utilisateur individuels] Pour créer des informations d’identification d’API de services Web pour un nouvel utilisateur, dans [!UICONTROL Gestion des utilisateurs], ajoutez l’utilisateur au groupe d’utilisateurs **Accès au service Web**.
      * [!UICONTROL Point de terminaison] par défaut : les données de ce champ sont fournies par Adobe et ne peuvent pas être modifiées.
      * [!UICONTROL Point de terminaison] supplémentaire - Ajoutez `CNAMES`, si vous les utilisez, pour le serveur de suivi comme `metrics.companyname.com`
   * **Media Heartbeats**

      * [!UICONTROL Point de terminaison] par défaut : les données de ce champ sont fournies par Adobe et ne peuvent pas être modifiées.
      * [!UICONTROL Point de terminaison] supplémentaire : ajoutez `CNAMES`-les, si vous les utilisez, pour votre serveur de suivi, `metrics.companyname.com`par exemple.



