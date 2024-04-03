---
title: Service Elasticsearch instellen
description: Leer hoe u de service Elasticsearch voor Adobe Commerce kunt inschakelen voor cloudinfrastructuur.
feature: Cloud, Search, Services
exl-id: ac559cbb-342a-4756-ade5-49eba4827965
source-git-commit: 8147b43b26370d9305c3c7dc47865ddcbae1904d
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---

# Service Elasticsearch instellen

[Elasticsearch](https://www.elastic.co) is een opensource product dat u toelaat om gegevens van om het even welke bron, om het even welke formaat, en onderzoek en visualiseren het in echt te nemen - tijd.

{{elasticsearch-support}}

Voor Adobe Commerce versie 2.4.4 en hoger raadpleegt u [OpenSearch-service instellen](opensearch.md).

- Elasticsearch voeren snelle en geavanceerde zoekopdrachten uit op producten in de productcatalogus
- Elasticsearch Analyzers ondersteunen meerdere talen
- Ondersteunt stopwoorden en synoniemen
- Indexering heeft geen invloed op klanten totdat de herindexering is voltooid

>[!TIP]
>
>De Adobe raadt u aan altijd Elasticsearch voor uw Adobe Commerce op het project van de wolkeninfrastructuur te vestigen zelfs als u van plan bent om een derdezoekhulpmiddel voor uw toepassing van Adobe Commerce te vormen. De Elasticsearch van de vestiging verstrekt een reserveoptie in het geval dat het derdeonderzoekshulpmiddel ontbreekt.

{{service-instruction}}

**Elasticsearch inschakelen**:

1. Voor de projecten van de Aanzet, voeg toe `elasticsearch` aan de `.magento/services.yaml` bestand met de versie van de Elasticsearch en toegewezen schijfruimte in MB.

   ```yaml
   elasticsearch:
       type: elasticsearch:<version>
       disk: 1024
   ```

   Voor Pro projecten, moet u een kaartje van de Steun van Adobe Commerce voorleggen om de versie van de Elasticsearch in de het Staging en milieu&#39;s van de Productie te veranderen.

1. Stel de `relationships` eigenschap in de `.magento.app.yaml` bestand.

   ```yaml
   relationships:
       elasticsearch: "elasticsearch:elasticsearch"
   ```

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable Elasticsearch" && git push origin <branch-name>
   ```

   Voor informatie over hoe deze veranderingen uw milieu&#39;s beïnvloeden, zie [Services](services-yaml.md).

1. Nadat het plaatsingsproces voltooit, gebruik SSH aan login aan het verre milieu.

   ```bash
   magento-cloud ssh
   ```

1. Indexeer de zoekindex van de catalogus opnieuw.

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. Maak de cache leeg.

   ```bash
   bin/magento cache:clean
   ```

{{service-change-tip}}

## Compatibiliteit met Elasticsearch-software

Wanneer u uw Adobe Commerce installeert of verbetert op het project van de wolkeninfrastructuur, controleert altijd verenigbaarheid tussen de de dienstversie van de Elasticsearch en [Elasticsearch PHP](https://github.com/elastic/elasticsearch-php) client voor Adobe Commerce.

- **Eerste keer instellen**-Bevestig dat de versie van de Elasticsearch die in het dialoogvenster `services.yaml` bestand is compatibel met de Elasticsearch PHP client geconfigureerd voor Adobe Commerce.

- **Project upgraden**- Controleer of de Elasticsearch PHP client in de nieuwe toepassingsversie compatibel is met de Elasticsearch service versie die op de cloud-infrastructuur is geïnstalleerd.

Serviceversie en compatibiliteitsondersteuning voor Adobe Commerce op cloudinfrastructuur worden bepaald door versies die worden geïmplementeerd op de cloudinfrastructuur en verschillen soms van versies die worden ondersteund door Adobe Commerce-implementaties op locatie. Zie [Serviceversies](services-yaml.md#service-versions).

**De compatibiliteit van de software van de Elasticsearch controleren**:

1. Wijzig op uw lokale werkstation de projectmap.

1. De details van de Elasticsearch weergeven voor de actieve omgeving.

   ```bash
   magento-cloud relationships --property=elasticsearch
   ```

1. U kunt SSH ook gebruiken om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. De Composer-pakketversie controleren op `elasticsearch/elasticsearch`.

   ```bash
   composer show elasticsearch/elasticsearch
   ```

   Controleer in het antwoord de geïnstalleerde versie in het dialoogvenster `versions` eigenschap.

   ```terminal
   name     : elasticsearch/elasticsearch
   descrip. : PHP Client for Elasticsearch
   keywords : client, elasticsearch, search
   versions : * v7.17.1
   type     : library
   license  : Apache License 2.0 (Apache-2.0) (OSI approved) https://spdx.org/licenses/Apache-2.0.html#licenseText
   license  : GNU Lesser General Public License v2.1 only (LGPL-2.1-only) (OSI approved) https://spdx.org/licenses/LGPL-2.1-only.html#licenseText
   homepage :
   source   : [git] git@github.com:elastic/elasticsearch-php.git f1b8918f411b837ce5f6325e829a73518fd50367
   dist     : [zip] https://api.github.com/repos/elastic/elasticsearch-php/zipball/f1b8918f411b837ce5f6325e829a73518fd50367 f1b8918f411b837ce5f6325e829a73518fd50367
   path     : ~/vendor/elasticsearch/elasticsearch
   names    : elasticsearch/elasticsearch
   ```

   U kunt ook de Elasticsearch PHP client version vinden in de  `composer.lock` in de hoofdmap van de omgeving.

1. Haal de verbindingsgegevens van de Elasticsearch-service op vanaf de opdrachtregel.

   ```bash
   vendor/bin/ece-tools env:config:show services
   ```

   In de reactie, vind het IP adres voor het de diensteindpunt van de Elasticsearch:

   ```terminal
   | elasticsearch:                                                                                                  |
   +------------------------------------------+----------------------------------------------------------------------+
   | username                                 | null                                                                 |
   | scheme                                   | http                                                                 |
   | service                                  | elasticsearch                                                        |
   | fragment                                 | null                                                                 |
   | ip                                       | 169.254.220.11                                                       |
   | hostname                                 | dzggu33f75wi3sd24lgwtoupxm.elasticsearch.service._.magentosite.cloud |
   | public                                   | false                                                                |
   | cluster                                  | fo3qdoxtla4j4-master-7rqtwti                                         |
   | host                                     | elasticsearch.internal                                               |
   | rel                                      | elasticsearch                                                        |
   | query                                    |                                                                      |
   | path                                     | null                                                                 |
   | password                                 | null                                                                 |
   | type                                     | elasticsearch:6.5                                                    |
   | port                                     | 9200                                                                 |
   +------------------------------------------+----------------------------------------------------------------------+
   ```

1. De geïnstalleerde service voor Elasticsearch ophalen `version:number` van het de diensteindpunt.

   ```bash
   curl -XGET <elasticsearch-service-endpoint-ip-address>:9200/
   ```

   ```terminal
   {
      "name" : "-AqGi9D",
      "cluster_name" : "elasticsearch",
      "cluster_uuid" : "_yze6-ywSEW1MaAF8ZPWyQ",
      "version" : {
        "number" : "6.5.4",
        "build_flavor" : "default",
        "build_type" : "deb",
        "build_hash" : "82a8aa7",
        "build_date" : "2019-01-23T12:07:18.760675Z",
        "build_snapshot" : false,
        "lucene_version" : "7.5.0",
        "minimum_wire_compatibility_version" : "5.6.0",
        "minimum_index_compatibility_version" : "5.0.0"
   },
   "  tagline" : "You Know, for Search"
   }
   ```

1. Controleer de versiecompatibiliteit tussen de Elasticsearch service en de PHP client.

   Als de versies incompatibel zijn, voert u een van de volgende updates uit in uw omgevingsconfiguratie:

   - Verander de Elasticsearch PHP cliënt in een versie die met de de dienstversie van de Elasticsearch compatibel is.

     ```bash
     composer require "elasticsearch/elasticsearch:~<version>"
     ```

   - Wijzig de versie van de Elasticsearch-service in het dialoogvenster `services.yaml` naar een versie die compatibel is met de Elasticsearch PHP client.

     {{pro-update-service}}

## De service Elasticsearch opnieuw starten

Als u de [Elasticsearch](https://www.elastic.co) hebt, moet u contact opnemen met de ondersteuning van Adobe Commerce.

## Aanvullende zoekconfiguratie

- Standaard wordt de zoekconfiguratie voor Cloud-omgevingen telkens opnieuw gegenereerd wanneer u deze implementeert. U kunt de `SEARCH_CONFIGURATION` Implementeer variabele om aangepaste zoekinstellingen tussen implementaties te behouden. Zie [Variabelen implementeren](../environment/variables-deploy.md#search_configuration).

- Nadat u opstelling de dienst van de Elasticsearch voor uw project, gebruik Admin UI om de verbinding van de Elasticsearch te testen en Elasticsearch montages voor Adobe Commerce aan te passen.

### Plug-ins toevoegen voor Elasticsearch

U kunt desgewenst insteekmodules voor Elasticsearch toevoegen door de `configuration:plugins` van de Elasticsearch in de `.magento/services.yaml` bestand. Met de volgende code worden bijvoorbeeld de insteekmodules voor ICU-analyse en Fonetische analyse ingeschakeld.

```yaml
elasticsearch:
    type: elasticsearch:<service-version>
    disk: 1024
    configuration:
        plugins:
            - analysis-icu
            - analysis-phonetic
```

Als u de Elastic Suite-plug-in van derden gebruikt, moet u [de update `ece-tools` package](../dev-tools/update-package.md) naar versie 2002.0.19 of hoger.
Als u Elastic Suite instelt, voegt u de configuratie-instellingen toe aan de `ELASTICSUITE_CONFIGURATION` implementeert variabele. Deze configuratie bewaart de montages over plaatsingen.

### Plug-ins voor Elasticsearch verwijderen

De insteekmodules verwijderen uit `elasticsearch:` in `.magento/services.yaml` worden niet verwijderd of uitgeschakeld zoals u zou verwachten. U moet de gegevens van uw Elasticsearch opnieuw indexeren. Dit gedrag is opzettelijk bedoeld om mogelijk verlies of beschadiging van gegevens te voorkomen die afhankelijk zijn van deze plug-ins.

**Elasticsearch-plug-ins verwijderen**:

1. Verwijder de insteekmodules van de Elasticsearch uit uw `.magento/services.yaml` bestand.
1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add .magento/services.yaml
   ```

   ```bash
   git commit -m "Remove Elasticsearch plugin"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. De `.magento/services.yaml` wijzigingen in uw Cloud-repo.
1. Indexeer de zoekindex van de catalogus opnieuw.

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. Maak de cache leeg.

   ```bash
   bin/magento cache:clean
   ```

>[!TIP]
>
>Raadpleeg voor meer informatie over het gebruik van de Elastic Suite-plug-in of het oplossen van problemen met Adobe Commerce de [Elastic Suite-documentatie](https://github.com/Smile-SA/elasticsuite).

## Problemen oplossen

Raadpleeg de volgende Adobe Commerce Support-artikelen voor hulp bij het oplossen van problemen met de Elasticsearch:

- [Elasticsearch 5 is geconfigureerd, maar de zoekpagina wordt niet geladen met de fout &quot;Veldgegevens is uitgeschakeld...&quot;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/elasticsearch/elasticsearch-5-is-configured-but-search-page-does-not-load-with-fielddata-is-disabled...-error.html)
- [Cataloguspaginering werkt niet wanneer Elasticsearch 6.x wordt gebruikt](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/catalog-pagination-doesn-t-work-when-elasticsearch-6.x-is-used.html)
- [Elasticsearch in Adobe Commerce probleemoplosser](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/elasticsearch/elasticsearch-in-magento-troubleshooter.html)
- [Status Elasticsearch-index is `yellow` of `red`](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/elasticsearch/elasticsearch-index-status-is-yellow-or-red.html)
