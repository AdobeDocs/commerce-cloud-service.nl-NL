---
title: Cache instellen voor statische bestanden
description: Leer om de opties van de geheim voorgeheugenopslag in het  [!DNL Commerce]  dossier van de toepassingsconfiguratie te plaatsen.
feature: Cloud, Configuration, Cache, SCD
exl-id: ca6db004-47fc-45ea-b8db-c0ecc3c2136b
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Cache instellen voor statische bestanden

De cache-TTL (time-to-live) voor uw media en statische bestanden wordt in het configuratiebestand van `.magento.app.yaml` ingesteld met behulp van de `expires` -toets.

>[!NOTE]
>
>Voordat u de productieomgeving bijwerkt, is het belangrijk dat u de wijzigingen in de testomgeving test. [ leg een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) voor hulp met het bijwerken van de configuratie op deze milieu&#39;s voor.

1. Geef de TTL-tijd (in seconden) op in de eigenschap [`web` ](web-property.md) van het `.magento.app.yaml` -bestand. U kunt de `expires` -toets toevoegen onder `locations` of onder `"/media"` en `"/static"` .

   Als u wilt voorkomen dat de cache vervalt, gebruikt u het sleutelwaardepaar `expires: -1` . Zie het volgende voorbeeld:

   ```yaml
   # The configuration of app when it is exposed to the web.
   web:
     locations:
       "/media":
         ...
         expires: -1
   
       "/static":
         ...
         expires: -1
   ```

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add -A && git commit -m "Set cache TTL for static files" && git push origin <branch-name>
   ```
