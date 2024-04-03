---
title: Cache instellen voor statische bestanden
description: Leer opslagopties voor cache in te stellen in het dialoogvenster [!DNL Commerce] toepassingsconfiguratiebestand.
feature: Cloud, Configuration, Cache, SCD
exl-id: ca6db004-47fc-45ea-b8db-c0ecc3c2136b
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Cache instellen voor statische bestanden

De cache-TTL (time-to-live) voor uw media en statische bestanden wordt ingesteld in het dialoogvenster `.magento.app.yaml` configuratiebestand gebruiken `expires` toets.

>[!NOTE]
>
>Voordat u de productieomgeving bijwerkt, is het belangrijk dat u de wijzigingen in de testomgeving test. [Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) voor hulp bij het bijwerken van de configuratie in deze omgevingen.

1. Geef de TTL-tijd (in seconden) op in het dialoogvenster [`web` eigenschap](web-property.md) van de `.magento.app.yaml` bestand. U kunt de `expires` key under `locations` of onder `"/media"` en `"/static"`.

   Als u wilt voorkomen dat de cache vervalt, gebruikt u de `expires: -1` sleutelwaardepaar. Zie het volgende voorbeeld:

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
