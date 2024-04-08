---
title: Cloud Components for Commerce
description: Zie een lijst met de meest recente verbeteringen in het pakket met Cloud Components.
recommendations: noDisplay, catalog
exl-id: b4e2508a-3558-4fa8-bae0-3eb76c7b2775
source-git-commit: c02dfd2709cdc63ac1630edaa8c89cad5f737ea1
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# Cloud Components for Commerce

De [Cloud-componenten](https://github.com/magento/magento-cloud-components) biedt uitgebreide Adobe Commerce-kernfunctionaliteit voor sites die worden geïmplementeerd in de Cloud-infrastructuur. Dit pakket is afhankelijk van het pakket ECE-Tools. In deze releaseopmerkingen worden de meest recente verbeteringen van dit pakket beschreven. Dit pakket maakt deel uit van [Cloud Tools Suite voor handel](cloud-tools-suite.md).

De `magento/magento-cloud-components` het pakket gebruikt de volgende versiereeks: `<major>.<minor>.<patch>`

De opmerkingen bij de release omvatten:

- ![nieuw pictogram](../../assets/new.svg) Nieuwe functies
- ![fixepictogram](../../assets/fix.svg) Oplossingen en verbeteringen

<!--Add release notes below-->

## v1.0.14 {#latest}

Releasedatum: 8 april 2024

- ![nieuw pictogram](../../assets/new.svg) **PHP** — Toegevoegde ondersteuning voor PHP 8.3.

## v1.0.13

Releasedatum: 10 maart 2023

- ![nieuw pictogram](../../assets/new.svg) **Verbeterde ondersteuning voor PHP 8.2**—Oplossingen voor compatibiliteitsproblemen met bepaalde PHP 8.2.x-versies ter ondersteuning van Commerce 2.4.6.

## v1.0.12

Releasedatum: 13 september 2022

- ![fixepictogram](../../assets/fix.svg) **Fouten bij warmtekrachtkoppeling**—Oplossing voor een probleem dat probeerde op te lossen [opwarmen](../environment/variables-post-deploy.md#warm_up_pages) wanneer de zichtbaarheid van de pagina is ingesteld op [**Niet afzonderlijk zichtbaar**](https://docs.magento.com/user-guide/system/data-attributes-product.html#simple-product-csv-file-structure) in de Admin, resulterend in `ERROR: Warming up failed: <link to page>` fouten in het plaatsingslogboek.<!-- MCLOUD-9134 -->

## v1.0.11

Releasedatum: 4 augustus 2022

- ![fixepictogram](../../assets/fix.svg) **Toegevoegde ondersteuning voor compatibiliteit met Symfony 5.4**—Oplossingen voor compatibiliteit met Symfony 5.4.<!-- AC-3550 -->

## v1.0.10

Releasedatum: 10 maart 2022

- ![nieuw pictogram](../../assets/new.svg) **Ondersteuning voor PHP 8.1**—Toegevoegde ondersteuning voor PHP 8.1 en verwijderde ondersteuning voor PHP 7.1.

## v1.0.9

Releasedatum: 25 oktober 2021

- ![fixepictogram](../../assets/fix.svg) **Monolog bijwerken**—De minimale versie die vereist is voor de `monolog` verpakken naar `^2.3`.<!-- ACMP-1263 -->

## v1.0.8

Releasedatum: 29 juli 2021

- ![fixepictogram](../../assets/fix.svg) **Verwijderde slashes van automatisch gegenereerde URL&#39;s**—Verwijderd de slashes aan het einde van de pagina-URL&#39;s van de categorie die tijdens het opwarmen van de cache zijn gegenereerd.<!--MCLOUD-7192-->

## v1.0.7

Releasedatum: 9 september 2020

- ![nieuw pictogram](../../assets/new.svg) **Verbeteringen voor logboekregistratie**—Verklein de grootte van `cache.log` om de prestaties te verbeteren.<!--MCLOUD-6859-->

- ![fixepictogram](../../assets/fix.svg) Oplossing voor een typefout in de cacheconfiguratiewaarden die de oorzaak waren van de fout `php bin/magento cache:evict` CLI bevel om te ontbreken.

## v1.0.6

Releasedatum: 5 augustus 2020

- ![nieuw pictogram](../../assets/new.svg) **Prestaties van Redis verbeteren**—Toegevoegd de `./bin/magento cache:evict` gebruiken om verlopen Redis-toetsen te verwijderen, waardoor het geheugengebruik van Redis wordt verminderd om de prestaties te verbeteren.<!--MCLOUD-6023-->

- ![fixepictogram](../../assets/fix.svg) Verwijderde ondersteuning voor *New Relic-aanmeldingen in context* om een prestatieprobleem op te lossen.<!--MCLOUD-6422-->

## v1.0.5

Releasedatum: 25 juni 2020

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen dat werd geïntroduceerd in magento/magento-cloud-components versie 1.0.4 en dat ertoe leidde dat de uitlijningscache-bewerking tijdens de implementatiefase mislukte, waardoor het implementatieproces werd onderbroken.

## v1.0.4

Releasedatum: 25 juni 2020

- ![nieuw pictogram](../../assets/new.svg) **Geïmplementeerde New Relic-logbestanden in context**—Toepassingslogboeken die door Adobe Commerce worden gegenereerd, worden nu weergegeven in sporen binnen New Relic om de mogelijkheden voor probleemoplossing te verbeteren.<!--MCLOUD-6029-->

- ![nieuw pictogram](../../assets/new.svg) **Verbeterde logboekregistratie**—Toegevoegde logboekregistratie om de ongeldigverklaring van het geheime voorgeheugen en volledige herindexgebeurtenissen te volgen.<!--MCLOUD-6157-->

## v1.0.3

Releasedatum: 27 februari 2020

- ![fixepictogram](../../assets/fix.svg) Oplossing voor een compatibiliteitsprobleem dat moest worden ondersteund `ece-tools` 2002.0.x-releases die oudere PHP-versies gebruiken.

## v1.0.2

Releasedatum: 6 februari 2020

- ![nieuw pictogram](../../assets/new.svg) Uitgebreide functionaliteit van de `WARM_UP_PAGES` omgevingsvariabele ter ondersteuning van het vooraf laden van cache voor specifieke productpagina&#39;s. Zie de [variabelen na implementatie](../environment/variables-post-deploy.md#warm_up_pages) voor een gedetailleerde eigenschapbeschrijving.<!--MAGECLOUD-4444-->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen waarbij een ongeldige opslag-URL ertoe leidde dat de naimplementatiehaak mislukte bij gebruik van de `WARM_UP_PAGES` om de cache te vullen. Dit probleem is alleen opgetreden toen URL-herschrijvingen waren uitgeschakeld.<!-- MAGECLOUD-4094 -->

## v1.0.1

Releasedatum: 23 juli 2019

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen dat invloed had op [**WARM_UP_PAGES**](../environment/variables-post-deploy.md#warm_up_pages) functionaliteit die een standaard opslag URL gebruikt. Als de `config:show:default-url` opdracht kan geen basis-URL ophalen, wordt de URL van de variabele MAGENTO_CLOUD_ROUTES gebruikt.<!-- MAGECLOUD-3866 -->

## v1.0.0

Releasedatum: 12 juni 2019

Dit is de eerste release van het [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components) pakket is een nieuwe afhankelijkheid van `ece-tools` pakketversie 2002.0.20 en hoger.

- ![nieuw pictogram](../../assets/new.svg) De mogelijkheid toegevoegd om regex-patronen te gebruiken om de **WARM_UP_PAGES** omgevingsvariabele om één pagina, meerdere domeinen en meerdere pagina&#39;s in cache te plaatsen. Zie [Variabelen na implementatie](../environment/variables-post-deploy.md#warm_up_pages).<!--MAGECLOUD-3258-->
