---
title: OpenSearch-service instellen
description: Leer hoe u de OpenSearch-service voor Adobe Commerce kunt inschakelen voor cloudinfrastructuur.
feature: Cloud, Search, Services
exl-id: 10dc6367-3f90-4ab6-a84e-15e8c3b32a38
source-git-commit: d4c36b084094846cfad69adc2bffd567a58fab26
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# OpenSearch-service instellen

De [OpenSearch](https://www.opensearch.org) de dienst is een open-bronvork van Elasticsearch 7.10.2, na de vergunningsveranderingen voor Elasticsearch. Zie de [OpenSource-project](https://github.com/opensearch-project) in GitHub.

{{elasticsearch-support}}

Met OpenSearch kunt u gegevens van elke bron, elke indeling en in real-time zoeken en visualiseren.

- Snel en geavanceerd zoeken naar producten in de productcatalogus
- OpenSearch Analyzers ondersteunen meerdere talen
- Ondersteunt stopwoorden en synoniemen
- Indexering heeft geen invloed op klanten totdat de herindexering is voltooid

{{service-instruction}}

>[!TIP]
>
>De Adobe raadt u aan altijd OpenSearch voor uw Adobe Commerce op het project van de wolkeninfrastructuur te vestigen zelfs als u van plan bent om een derdezoekhulpmiddel voor uw toepassing van Adobe Commerce te vormen. Het instellen van OpenSearch biedt een fallback-optie als het zoekgereedschap van derden mislukt.

**OpenSearch inschakelen**:

1. Voor Starter- en Pro-integratieomgevingen voegt u de opdracht `opensearch` aan de `.magento/services.yaml` bestand met de juiste versie en toegewezen schijfruimte in MB. In dit geval is versie 2 geschikt. De secundaire versie is niet vereist omdat de cloudinfrastructuur de nieuwste versie van OpenSearch gebruikt.

   ```yaml
   opensearch:
       type: opensearch:2
       disk: 1024
   ```

   Voor Pro-projecten moet u [Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om de OpenSearch-versie te wijzigen in de omgeving voor Staging en productie.

1. Stel de `relationships` eigenschap in de `.magento.app.yaml` bestand.

   ```yaml
   relationships:
       opensearch: "opensearch:opensearch"
   ```

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add .magento/services.yaml .magento.app.yaml
   ```

   ```bash
   git commit -m "Enable OpenSearch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   Voor informatie over hoe deze veranderingen uw milieu&#39;s beïnvloeden, zie [Services configureren](services-yaml.md).

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

## Compatibiliteit met OpenSearch-software

Wanneer u Adobe Commerce installeert of upgradet voor een infrastructuurproject voor de cloud, moet u altijd controleren op compatibiliteit tussen de OpenSearch-serviceversie en de [OpenSearch PHP](https://github.com/opensearch-project/opensearch-php) client voor Adobe Commerce.

- **Eerste keer instellen**-Bevestig dat de OpenSearch-versie die is opgegeven in het dialoogvenster `services.yaml` bestand is compatibel met de OpenSearch PHP client geconfigureerd voor Adobe Commerce.

- **Project upgraden**-Controleer of de OpenSearch PHP-client in de nieuwe toepassingsversie compatibel is met de OpenSearch-serviceversie die op de cloud-infrastructuur is geïnstalleerd.

De versie van de dienst en verenigbaarheidssteun wordt bepaald door versies die op de infrastructuur van de Wolk worden getest en worden opgesteld, en verschillen soms van versies die door Adobe Commerce op-gebouw plaatsingen worden gesteund. Zie [Systeemvereisten](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) in de _Installatiehandleiding_ voor een lijst met ondersteunde versies.

**Compatibiliteit met OpenSearch-software controleren**:

1. Wijzig op uw lokale werkstation de projectmap.

1. De OpenSearch-details voor de actieve omgeving weergeven.

   ```bash
   magento-cloud relationships --property=opensearch
   ```

1. U kunt SSH ook gebruiken om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Haal de verbindingsgegevens van de OpenSearch-service op.

   ```bash
   vendor/bin/ece-tools env:config:show services
   ```

   In de reactie, vind het IP adres en de haven voor het de diensteindpunt van OpenSearch:

   ```terminal
   +------------------------------------------+--------------------------------------------------------+
   | opensearch:                                                                                       |
   +------------------------------------------+--------------------------------------------------------+
   | username                                 | null                                                   |
   | scheme                                   | http                                                   |
   | service                                  | opensearch                                             |
   | fragment                                 | null                                                   |
   | ip                                       | 169.254.220.11                                         |
   | hostname                                 | hostf75wi3sd24l.opensearch.service._.magentosite.cloud |
   | port                                     | 9200                                                   |
   | cluster                                  | projectID-develop-4ranwui                              |
   | host                                     | opensearch.internal                                    |
   | rel                                      | opensearch                                             |
   | path                                     | null                                                   |
   | query                                    |                                                        |
   | password                                 | null                                                   |
   | type                                     | opensearch:2                                           |
   | public                                   | false                                                  |
   | host_mapped                              | false                                                  |
   ```

1. De geïnstalleerde OpenSearch-service ophalen `version:number` van het de diensteindpunt.

   ```bash
   curl -XGET <opensearch-service-endpoint-ip-address>:9200
   ```

   ```terminal
   {
      "name" : "opensearch.0",
      "cluster_name" : "opensearch",
      "cluster_uuid" : "_yzaae6-ywSEW1MaAF8ZPWyQ",
      "version" : {
        "distribution" : "opensearch",
        "number" : "2.5.0",
        "build_type" : "deb",
        "build_hash" : "aaaaaaa",
        "build_date" : "2023-01-23T12:07:18.760675Z",
        "build_snapshot" : false,
        "lucene_version" : "9.4.2",
        "minimum_wire_compatibility_version" : "7.10.0",
        "minimum_index_compatibility_version" : "7.0.0"
   },
   "tagline" : "The OpenSearch Project: https://opensearch.org/"
   }
   ```

{{pro-update-service}}

## De OpenSearch-service opnieuw starten

Als u de OpenSearch-service opnieuw wilt starten, moet u contact opnemen met de ondersteuning van Adobe Commerce.

## Aanvullende zoekconfiguratie

- Standaard wordt de zoekconfiguratie voor Cloud-omgevingen telkens opnieuw gegenereerd wanneer u deze implementeert. U kunt de `SEARCH_CONFIGURATION` Implementeer variabele om aangepaste zoekinstellingen tussen implementaties te behouden. Zie [Variabelen implementeren](../environment/variables-deploy.md#search_configuration).

- Nadat u de OpenSearch-service voor uw project hebt ingesteld, gebruikt u de beheerinterface om de OpenSearch-verbinding te testen en de OpenSearch-instellingen voor Adobe Commerce aan te passen.

### Plug-ins toevoegen voor OpenSearch

U kunt desgewenst insteekmodules voor OpenSearch toevoegen door de opdracht `configuration:plugins` aan de OpenSearch-service in het gedeelte `.magento/services.yaml` bestand. Met de volgende code worden bijvoorbeeld de insteekmodules voor ICU-analyse en Fonetische analyse ingeschakeld.

```yaml
opensearch:
    type: opensearch:2
    disk: 1024
    configuration:
        plugins:
            - analysis-icu
            - analysis-phonetic
```

Zie de [OpenSearch-project](https://github.com/opensearch-project) voor meer informatie over plug-ins.

### Insteekmodules voor OpenSearch verwijderen

De invoegtoepassingen verwijderen uit het dialoogvenster `opensearch:` van de `.magento/services.yaml` bestand doet dit **niet** Verwijder of maak de dienst onbruikbaar. Als u de service volledig wilt uitschakelen, moet u de OpenSearch-gegevens opnieuw indexeren nadat u de plug-ins uit uw `.magento/services.yaml` bestand. Dit ontwerp voorkomt mogelijk gegevensverlies of -beschadiging die afhankelijk is van deze plug-ins.

**OpenSearch-plug-ins verwijderen**:

1. De OpenSearch-insteekmodules verwijderen uit uw `.magento/services.yaml` bestand.
1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add .magento/services.yaml
   ```

   ```bash
   git commit -m "Remove OpenSearch plugin"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. De `.magento/services.yaml` wijzigingen in uw cloudopslagplaats.
1. Indexeer de zoekindex van de catalogus opnieuw.

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. Maak de cache leeg.

   ```bash
   bin/magento cache:clean
   ```
