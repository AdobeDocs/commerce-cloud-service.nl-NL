---
title: Aanbevolen procedures voor het upgraden van uw project
description: Zie een lijst met aanbevolen procedures voor het upgraden van uw projectbestanden.
feature: Cloud, Best Practices, Upgrade
exl-id: 7d0a2627-e4c5-46b4-9e6c-24d20fa4f92f
source-git-commit: c61d711b1041ecf76ec6468cd225a34fd77c24b1
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Aanbevolen procedures voor het upgraden van uw project

Volg de beste praktijken voor bouwstijlen en plaatsing, en gebruik [Upgrades en patches](../development/commerce-version.md) om uw toepassing te upgraden. Gebruik de volgende richtlijnen om uw upgrade en werk na de upgrade te plannen:

- **Back-up maken van uw project**- Voordat u de Adobe Commerce en eventuele externe of aangepaste extensies upgradet, moet u een back-up maken van de database in de omgevingen Integratie, Staging en Productie. Zie [Back-up maken van de database](../development/commerce-version.md#project-backup).

- **Controleren op compatibiliteitsproblemen**-

   - Zorg ervoor dat aangepaste thema&#39;s compatibel zijn met de nieuwe Adobe Commerce-versie

   - Nadat u een upgrade hebt uitgevoerd voor externe en aangepaste extensies, kunt u de opdracht `magento-cloud local:build` bevel om Composer gebiedsdelen te bevestigen alvorens op te stellen.

   - Bekijk de Adobe Commerce-releaseopmerkingen en de uitbreidingsdocumentatie om te controleren of u eventuele oplossingen of configuratiewijzigingen hebt geïmplementeerd die nodig zijn om bekende functionele problemen en fouten met betrekking tot de upgrade van de Adobe Commerce-versie en -extensies te verhelpen.

   - Zorg ervoor dat de geïnstalleerde serviceversies compatibel zijn met de nieuwe Adobe Commerce-versie en werk de services waar nodig bij. Zie [Services](../services/services-yaml.md).

   - Test uw database om problemen op te lossen die zijn ontstaan door de updates voor de Adobe Commerce-versie en -extensies.

   - Breng de vereiste updates van de specifieke omgevingen aan voordat u deze implementeert in de externe omgeving.

   - Zorg ervoor dat de versie van de zoekservice compatibel is met de PHP-clientversie. Zie [Elasticsearch instellen](../services/elasticsearch.md) of [OpenSearch instellen](../services/opensearch.md).

- **Controleer de databaseconnectiviteit en de beschikbare opslag in externe omgevingen**-

   - Gebruik SSH aan login aan de verre server en verifieer de verbinding aan het gegevensbestand MySQL. Zie [Verbinding maken met de database](../services/mysql.md#connect-to-the-database).

   - Beschikbare opslag controleren in de externe omgeving - Gebruik de optie `disk free` gebruiken om beschikbare schijfruimte in uw cloud-omgevingen weer te geven en te beheren. Zie [Schijfruimte beheren](../storage/manage-disk-space.md).

      - Controleer de grootte van het bijgewerkte gegevensbestand en verifieer dat `services.yaml` Er is voldoende schijfruimte toegewezen.

      - Maak schijfruimte vrij - ontruim het geheime voorgeheugen en schoonmaak `/log` en `/tmp` mappen voordat deze worden geïmplementeerd.

- **Plan en voer een succesvolle verbetering op lokale en integratiemilieu&#39;s uit, alvorens aan het Opvoeren**-Na de upgrade test u de implementatie en lost u eventuele problemen op.

- **Code samenvoegen met Staging en vervolgens met Productie**- Test en los eventuele problemen in de testomgeving op voordat u wijzigingen aanbrengt in de productieomgeving.

- **Voer upgradetaken uit**-

   - Gebruik SSH om u aan te melden bij de externe server en controleer het volgende:

      - Controleer de indexeerstatus en herdex naar wens. Zie [De indexen beheren](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/manage-indexers.html) in de _Configuratiegids_.

      - Controleer de `cron` de `cron_schedule` tabel in de Adobe Commerce-database om de status van uitsnijden te controleren en de taken opnieuw uit te voeren.
Zie [Logboekregistratie](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html#logging) in de _Configuratiegids_.

   - Voltooi het testen van gebruikersacceptatietests na de upgrade op de testomgeving voor het opslaan en produceren van bestanden en los eventuele problemen op die te maken hebben met upgrades van derden en aangepaste extensies.
