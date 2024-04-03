---
title: Cloudarchitectuur voor handel
description: Leer hoe de architecturen van Starter en Pro van het Project tegenover de Handel op de infrastructuur van de Wolk contrasteren.
feature: Cloud, Iaas, Paas
topic: Architecture
recommendations: noDisplay
exl-id: 37cd6733-c10a-4d06-b784-171da576f9fc
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---

# Cloudarchitectuur voor handel

Adobe Commerce on cloud Infrastructure heeft een Starter- en een Pro-plan. Elk plan heeft een unieke architectuur om uw ontwikkeling en plaatsingsproces van Adobe Commerce te drijven. Zowel het plan van de Aanzet als de Pro planarchitectuur stellen gegevensbestanden, Webservers, en caching servers over veelvoudige milieu&#39;s voor het testen van begin tot eind op terwijl het steunen van ononderbroken integratie.

Ter vergelijking, omvat elk plan de volgende infrastructuureigenschappen en gesteunde producten.

|          | Starter | Pro |
| -------- | --------------------| ------------------ |
| Kernfuncties | <ul><li>[Alle Adobe Commerce-functies](https://experienceleague.adobe.com/docs/commerce-operations/release/features.html)</li><li>PayPal on boarding Tool</li><li>[Koophandel](https://business.adobe.com/products/magento/business-intelligence.html?_ga=2.85288604.442698376.1665067470-1322106587.1655147209)</li></ul> | <ul><li>[Alle Adobe Commerce-functies](https://experienceleague.adobe.com/docs/commerce-operations/release/features.html)</li><li>PayPal on boarding Tool</li><li>[Koophandel](https://business.adobe.com/products/magento/business-intelligence.html?_ga=2.85288604.442698376.1665067470-1322106587.1655147209)</li><li>[B2B-module](https://business.adobe.com/products/magento/b2b-ecommerce.html?_ga=2.105948422.442698376.1665067470-1322106587.1655147209)</li></ul> |
| Infrastructuur en implementatie | <ul><li>Doorlopende tools voor cloudintegratie met onbeperkte gebruikers</li><li>Het netwerk van de Levering van de Inhoud (CDN), de Optimalisering van het Beeld (IO), en toegevoegde veiligheid met genereuze bandbreedteemissierechten. De dienst van de Firewall van de Toepassing van het Web (WAF) is beschikbaar op productiemilieu&#39;s slechts.</li><li>[New Relic](../monitor/new-relic-service.md) APM (Performance Monitoring) op 3 takken: `master` en 2 van uw keuze<br>Platform als een dienst (PaS) productie, het opvoeren, en ontwikkelmilieu&#39;s (4 totaal actieve milieu&#39;s) die voor Adobe Commerce worden geoptimaliseerd</li><li>Egress-filtering (uitgaande firewall)</li></ul> | <ul><li>Doorlopende tools voor cloudintegratie met onbeperkte gebruikers</li><li>Het netwerk van de Levering van de Inhoud (CDN), de Optimalisering van het Beeld (IO), en toegevoegde veiligheid met genereuze bandbreedteemissierechten. De dienst van de Firewall van de Toepassing van het Web (WAF) is beschikbaar op productiemilieu&#39;s slechts.</li><li>[New Relic](../monitor/new-relic-service.md) Infrastructuur voor productie + APM (prestatiebewaking) voor afbouw en productie. De [Beleid voor beheerde waarschuwingen](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts) voor het beleid van Adobe Commerce voert controle beste praktijken uit om u over toepassing en infrastructuurkwesties proactief mee te delen die plaatsprestaties beïnvloeden.</li><li>Platform als dienst (PaaS) gebaseerd [Integratieontwikkeling](pro-architecture.md#integration-environment) omgevingen (2 totaal actieve omgevingen) die zijn geoptimaliseerd voor Adobe Commerce</li><li>Infrastructuur als dienst (IaaS) - specifieke virtuele infrastructuur voor het Opvoeren en van de Productie milieu&#39;s</li></ul> |
| Infrastructuur voor hoge beschikbaarheid | | [Architectuur met hoge beschikbaarheid](pro-architecture.md#redundant-hardware) met een installatie van drie servers in de onderliggende infrastructuur als een service (IaaS) om betrouwbaarheid en beschikbaarheid op bedrijfsniveau te bieden |
| Speciale hardware | | Geïsoleerde en toegewijde hardware in de onderliggende infrastructuur als een dienst (IaaS) om nog hogere niveaus van betrouwbaarheid en beschikbaarheid te verstrekken |
| 24x7 e-mailondersteuning | 24x7 controle en e-mailondersteuning voor de kerntoepassing en de cloudinfrastructuur | 24x7 controle en e-mailondersteuning voor de kerntoepassing en de cloudinfrastructuur |
| Een toegewijde Technische Adviseur van de Klant (CTA) | | Specifiek technisch accountbeheer voor de eerste startperiode, vanaf uw abonnement tot uw eerste site wordt gestart |
| Invoegtoepassingen\* | <ul><li>[B2B-module](https://business.adobe.com/products/magento/b2b-ecommerce.html)</li></ul> |

\* _Beschikbaar voor extra kosten_

## Startersprojecten

De [Startplanarchitectuur](starter-architecture.md) heeft vier omgevingen:

- **Integratie**—De integratieomgeving biedt twee testbare omgevingen. Elke omgeving bevat een actieve Git-vertakking, database, webserver, caching, sommige services, omgevingsvariabelen en configuraties.

- **Staging**—Als de code en de uitbreidingen uw tests overgaan, kunt u uw samenvoegen `integration` vertakken naar de testomgeving voor de productie. Dit wordt de testomgeving voor de productie. Het omvat de `staging` actieve vertakking, database, webserver, caching, services van derden, omgevingsvariabelen, configuraties en services, zoals Fastly en New Relic.

- **Productie**—Wanneer code gereed en getest is, wordt alle code samengevoegd tot `master` voor uitrol naar de productielocatie live. Deze omgeving omvat uw actieve `master` vertakking, database, webserver, caching, services van derden, omgevingsvariabelen en configuraties.

- **Inactief**—U hebt een onbeperkt aantal inactieve vertakkingen.

## Pro-projecten

De [Pro-planarchitectuur](pro-architecture.md) heeft een globale `master` met drie omgevingen:

- **Integratie**—De integratieomgeving biedt een testbare omgeving die een database, webserver, caching, sommige services, omgevingsvariabelen en configuraties bevat. U kunt uw code ontwikkelen, opstellen en testen alvorens aan het Opvoeren milieu samen te voegen.

   - _Inactief_—U kunt een onbeperkt aantal inactieve vertakkingen hebben die op `integration` milieu, maar slechts één actieve tak (niet inbegrepen `integration` ).

- **Staging**—De testomgeving is bedoeld voor preproductietests en bevat een database, webserver, caching, services van derden, omgevingsvariabelen, configuraties en services, zoals Fastly.

- **Productie**—De productieomgeving bevat een architectuur met drie knooppunten en hoge beschikbaarheid voor uw gegevens, services, caching en opslag. De productie is uw levende, openbare opslagmilieu met milieuvariabelen, configuraties, en derdediensten.

## Ondersteunde software en services

Adobe Commerce op cloudinfrastructuur gebruikt:

- Besturingssysteem: Debian GNU/Linux
- Webserver: Nginx
- Database: MySQL (MariaDB)
- Content Delivery Network (CDN): Fastly CDN

U kunt de volgende services configureren:

- [PHP](../application/php-settings.md)
- [MySQL](../services/mysql.md)
- [Redis](../services/redis.md)
- [RabbitMQ](../services/rabbitmq.md)
- [Elasticsearch](../services/elasticsearch.md)
- [OpenSearch](../services/opensearch.md)

{{elasticsearch-support}}

>[!NOTE]
>
>Zie [Systeemvereisten](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) in de _Installatiehandleiding_ voor aanbevolen versies.

De snelste CDN-module wordt gebruikt voor CDN- en caching-services op staging- en productieomgevingen. Zie [Services voor snel configureren](../cdn/fastly.md).

Raadpleeg de volgende Adobe Commerce over configuratiebestanden voor de cloud-infrastructuur voor informatie over het configureren van de softwareversies die u in uw implementatie wilt gebruiken:

- [Toepassingsconfiguratie (.magento.app.yaml)](../application/configure-app-yaml.md)
- [Omgevingsconfiguratie (.magento.env.yaml)](../environment/configure-env-yaml.md)
- [Configuratie van routes (routes.yaml)](../routes/routes-yaml.md)
- [Configuratie van services (services.yaml)](../services/services-yaml.md)
