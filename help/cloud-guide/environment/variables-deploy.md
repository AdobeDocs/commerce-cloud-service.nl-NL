---
title: Variabelen implementeren
description: Zie de lijst met omgevingsvariabelen die acties in de Adobe Commerce op de implementatiefase van de cloudinfrastructuur besturen.
feature: Cloud, Configuration, Cache, Deploy, SCD, Storage, Search
recommendations: noDisplay, catalog
role: Developer
exl-id: 673880b5-830b-4837-ac0c-5fa5643ae34c
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '2185'
ht-degree: 0%

---

# Variabelen implementeren

Het volgende _inzetten_ variabelen controleren acties in de opstellen fase en kunnen waarden van erven en met voeten treden [Algemene variabelen](variables-global.md). Deze variabelen invoegen in het dialoogvenster `deploy` stadium van de `.magento.env.yaml` bestand:

```yaml
stage:
  deploy:
    DEPLOY_VARIABLE_NAME: value
```

Voor meer informatie over het aanpassen van het bouwstijl en opstellen proces:

- [Implementatieconfiguratie](configure-env-yaml.md)
- [Implementatieproces](../deploy/process.md)

## `CACHE_CONFIGURATION`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.1.4 en hoger

Configureer Redis-pagina en standaardcaching. Wanneer u het `cm_cache_backend_redis` parameter, moet u specificeren `server`, `port`, en `database` opties.

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      frontend:
        default:
          backend: file
        page_cache:
          backend: file
```

{{merge-options}}

In het volgende voorbeeld worden nieuwe waarden samengevoegd met een bestaande configuratie:

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      _merge: true
      frontend:
        default:
          backend_options:
            database: 10
        page_cache:
          backend_options:
            database: 11
```

In het volgende voorbeeld wordt het [Redis, functie voor vooraf laden](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/redis/redis-pg-cache.html#redis-preload-feature) zoals gedefinieerd in het _Configuratiegids_:

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      _merge: true
      frontend:
        default:
          id_prefix: '061_'
          backend_options:
            preload_keys:
              - '061_EAV_ENTITY_TYPES:hash'
              - '061_GLOBAL_PLUGIN_LIST:hash'
              - '061_DB_IS_UP_TO_DATE:hash'
              - '061_SYSTEM_DEFAULT:hash'
```

Een aangepaste [REDIS_BACKEND](#redis_backend) model (niet alleen vanuit de lijst van gewenste personen), stelt u de `_custom_redis_backend` optie voor `true` om de juiste validatie in te schakelen, zoals in het volgende voorbeeld:

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      frontend:
        default:
          _custom_redis_backend: true
          backend: '\CustomRedisModel'
```

## `CLEAN_STATIC_FILES`

- **Standaard**—`true`
- **Versie**—Adobe Commerce 2.1.4 en hoger

Schakelt reiniging in of uit [statische inhoudsbestanden](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html) geproduceerd tijdens de bouwstijl of opstellen fase. De standaardwaarde gebruiken _true_ in ontwikkeling als beste praktijk.

- **`true`**—Verwijdert alle bestaande statische inhoud alvorens de bijgewerkte statische inhoud op te stellen.
- **`false`**—De implementatie overschrijft alleen bestaande statische inhoudsbestanden als de gegenereerde inhoud een nieuwere versie bevat.

Als u statische inhoud wijzigt via een afzonderlijk proces, stelt u de waarde in op _false_.

```yaml
stage:
  deploy:
    CLEAN_STATIC_FILES: false
```

Het niet opschonen van statische weergavebestanden vóór de implementatie kan problemen veroorzaken als u updates voor bestaande bestanden implementeert zonder de vorige versies te verwijderen. Vanwege [fallback van statische bestanden](https://developer.adobe.com/commerce/frontend-core/guide/caching/#clean-static-files-cache) regels, kunnen fallback-bewerkingen het verkeerde bestand weergeven als de map meerdere versies van hetzelfde bestand bevat.

## `CRON_CONSUMERS_RUNNER`

- **Standaard**—`cron_run = false`, `max_messages = 1000`
- **Versie**—Adobe Commerce 2.2.0 en hoger

Gebruik deze omgevingsvariabele om te bevestigen dat de berichtenrijen na een implementatie worden uitgevoerd.

- `cron_run`—Een booleaanse waarde die de `consumers_runner` uitsnijdtaak (standaard = `false`).
- `max_messages`—Een getal dat het maximum aantal berichten opgeeft dat elke consument moet verwerken voordat hij/zij afsluit (standaardwaarde = `1000`). U kunt instellen op `0` om te voorkomen dat de consument wordt beëindigd.
- `consumers`—Een array van tekenreeksen die aangeven welke consumenten moeten worden uitgevoerd. Een lege array wordt uitgevoerd _alles_ consumenten.

- `multiple_processes`-Een getal dat het aantal processen opgeeft dat voor elke consument moet worden gekaapt. Ondersteund in de handel **2.4.4.** of hoger.

>[!NOTE]
>
>Om een lijst van berichtrij terug te keren `consumers`, voert u de `./bin/magento queue:consumers:list` in de externe omgeving.

Voorbeeld van een array die specifiek wordt uitgevoerd `consumers` en de `multiple_processes` voor elke consument:

```yaml
stage:
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 1000
      consumers:
        - example_consumer_1
        - example_consumer_2
-     multiple_processes:
        example_consumer_1: 4
        example_consumer_2: 3
```

Voorbeeld van een lege array die alles uitvoert `consumers`:

```yaml
stage:
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 1000
      consumers: []
```

Standaard overschrijft het implementatieproces alle instellingen in de `env.php` bestand. Zie [Berichtenrijen beheren](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/manage-message-queues.html) in de _Handleiding voor configuratie_ voor Adobe Commerce ter plaatse.

## `CONSUMERS_WAIT_FOR_MAX_MESSAGES`

- **Standaard**—`false`
- **Versie**—Adobe Commerce 2.2.0 en hoger

Configureren hoe `consumers` verwerkt berichten van de berichtrij door één van de volgende opties te kiezen:

- `false`—`Consumers` proces beschikbare berichten in de rij, sluit de verbinding van TCP, en beëindigt. `Consumers` wacht niet op extra berichten om de rij in te gaan, zelfs als het aantal verwerkte berichten minder dan is `max_messages` waarde opgegeven in het dialoogvenster `CRON_CONSUMERS_RUNNER` implementeert variabele.

- `true`—`Consumers` blijven berichten van de berichtrij verwerken tot het maximumaantal berichten (`max_messages`) opgegeven in de `CRON_CONSUMERS_RUNNER` Implementeer variabele voordat u de TCP-verbinding sluit en het consumentenproces beëindigt. Als de wachtrij wordt leeggemaakt voordat de wachtrij wordt bereikt `max_messages`, wacht de consument op meer berichten.

>[!WARNING]
>
>Als u workers gebruikt om te starten `consumers` in plaats van een uitsnijdtaak te gebruiken, stelt u deze variabele in op true.

```yaml
stage:
  deploy:
    CONSUMERS_WAIT_FOR_MAX_MESSAGES: false
```

## `CRYPT_KEY`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.1.4 en hoger

>[!WARNING]
>
>Stel de `CRYPT_KEY` waarde door de [!DNL Cloud Console] in plaats van de `.magento.env.yaml` om te voorkomen dat de sleutel in de broncodeopslagplaats voor uw omgeving beschikbaar wordt gemaakt. Zie [Omgeving en projectvariabelen instellen](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html#configure-environment).

Wanneer u het gegevensbestand van één milieu aan een andere zonder installatieproces verplaatst, hebt u de overeenkomstige cryptografische informatie nodig. Adobe Commerce gebruikt de coderingssleutelwaarde die is ingesteld in het dialoogvenster [!DNL Cloud Console] als de `crypt/key` waarde in de `env.php` bestand.

## `DATABASE_CONFIGURATION`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.1.4 en hoger

Als u een database in het dialoogvenster [relaties, eigenschap](../application/properties.md#relationships) van de `.magento.app.yaml` kunt u uw databaseverbindingen aanpassen voor implementatie.

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      some_config: 'some_value'
```

{{merge-options}}

In het volgende voorbeeld worden nieuwe waarden samengevoegd met een bestaande configuratie:

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      some_config: 'some_new_value'
      _merge: true
```

U kunt ook een tabelvoorvoegsel configureren.

>[!WARNING]
>
>Als u de samenvoegoptie niet gebruikt met het tabelvoorvoegsel, moet u standaardverbindingsinstellingen opgeven of kan de implementatie niet worden gevalideerd.

In het volgende voorbeeld wordt het `ece_` tabelvoorvoegsel met standaardverbindingsinstellingen in plaats van de `_merge` optie:

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      connection:
        default:
          username: user
          host: host
          dbname: magento
          password: password
      table_prefix: 'ece_'
```

Voorbeelduitvoer:

```terminal
MariaDB [main]> SHOW TABLES;
+-------------------------------------+
| Tables_in_main                      |
+-------------------------------------+
| ece_admin_passwords                 |
| ece_admin_system_messages           |
| ece_admin_user                      |
| ece_admin_user_session              |
| ece_adminnotification_inbox         |
| ece_amazon_customer                 |
| ece_authorization_rule              |
| ece_cache                           |
| ece_cache_tag                       |
| ece_captcha_log                     |
...
```

## `ELASTICSUITE_CONFIGURATION`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.2.0 en hoger

Blijft aangepast [!DNL Elastic Suite] de dienstmontages tussen plaatsingen en gebruikt het in de &quot;systeem/gebrek/glimlach_elasticsuite_core_base_settings&quot;sectie van de belangrijkste [!DNL Elastic Suite] configuratie. Als de [!DNL Elastic Suite] samenstellingspakket is geïnstalleerd, automatisch geconfigureerd.

```yaml
stage:
  deploy:
    ELASTICSUITE_CONFIGURATION:
      es_client:
        servers: 'remote-host:9200'
      indices_settings:
        number_of_shards: 1
        number_of_replicas: 0
```

{{merge-options}}

In het volgende voorbeeld wordt een nieuwe waarde samengevoegd met de bestaande configuratie:

```yaml
stage:
  deploy:
    ELASTICSUITE_CONFIGURATION:
      indices_settings:
        number_of_shards: 3
        number_of_replicas: 2
      _merge: true
```

**Bekende beperkingen**:

- De zoekmachine wijzigen in een ander type dan `elasticsuite` veroorzaakt een implementatiefout vergezeld van een geschikte validatiefout
- Het verwijderen van de dienst van de Elasticsearch veroorzaakt een implementatiefout vergezeld van een aangewezen bevestigingsfout

>[!NOTE]
>
>Voor meer informatie over het gebruik of het oplossen van problemen [!DNL Elastic Suite] met Adobe Commerce, raadpleegt u de [[!DNL Elastic Suite] documentatie](https://github.com/Smile-SA/elasticsuite).

## `ENABLE_GOOGLE_ANALYTICS`

- **Standaard**—`false`
- **Versie**—Adobe Commerce 2.1.4 en hoger

Laat en maakt Googles Analytics toe onbruikbaar wanneer het opstellen aan het Opvoeren en de milieu&#39;s van de Integratie. Googles Analytics gelden standaard alleen voor de productieomgeving. Deze waarde instellen op `true` om Googles Analytics in de milieu&#39;s van het Staging en van de Integratie toe te laten.

- **`true`**—Laat Googles Analytics op het Opvoeren en de milieu&#39;s van de Integratie toe.
- **`false`**—Maakt Googles Analytics op het Opvoeren en de milieu&#39;s van de Integratie onbruikbaar.

Voeg de `ENABLE_GOOGLE_ANALYTICS` omgevingsvariabele voor de `deploy` in de `.magento.env.yaml` bestand:

```yaml
stage:
  deploy:
    ENABLE_GOOGLE_ANALYTICS: true
```

>[!NOTE]
>
>Het implementatieproces maakt altijd Googles Analytics in productieomgevingen mogelijk.

## `FORCE_UPDATE_URLS`

- **Standaard**—`true`
- **Versie**—Adobe Commerce 2.1.4 en hoger

Bij implementatie in een Pro- of Starter-testomgeving vervangt deze variabele Adobe Commerce-basis-URL&#39;s in de database door de project-URL&#39;s die zijn opgegeven door de [`MAGENTO_CLOUD_ROUTES`](variables-cloud.md) variabele. Gebruik deze instelling om het standaardgedrag van de [UPDATE_URLS](#update_urls) Implementeer variabele, die wordt genegeerd bij de implementatie in een testomgeving of productieomgeving.

```yaml
stage:
  deploy:
    FORCE_UPDATE_URLS: true
```

## `LOCK_PROVIDER`

- **Standaard**—`file`
- **Versie**—Adobe Commerce 2.2.5 en hoger

De vergrendelingsprovider voorkomt het starten van dubbele snijtaken en afdekgroepen. Gebruik de `file` sluisprovider in de productieomgeving. Starter-omgevingen en de Pro-integratieomgeving maken geen gebruik van de [MAGENTO_CLOUD_LOCKS_DIR](variables-cloud.md) variabele, so `ece-tools` past de `db` automatisch vergrendelen.

```yaml
stage:
  deploy:
    LOCK_PROVIDER: "db"
```

Zie [De vergrendeling configureren](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/lock-provider.html) in de _Hulplijn installeren_.

## `MYSQL_USE_SLAVE_CONNECTION`

- **Standaard**—`false`
- **Versie**—Adobe Commerce 2.1.4 en hoger

>[!TIP]
>
>De `MYSQL_USE_SLAVE_CONNECTION` Variabele wordt alleen ondersteund in Adobe Commerce op staging- en Production Pro-clusteromgevingen met cloudinfrastructuur en wordt niet ondersteund in Starter-projecten.

Adobe Commerce kan meerdere databases asynchroon lezen. Instellen op `true` om automatisch een _alleen-lezen_ verbinding met het gegevensbestand om read-only verkeer op een niet hoofdknoop te ontvangen. Deze verbinding verbetert prestaties door lading het in evenwicht brengen, omdat slechts één knoop lees-schrijf verkeer behandelt. Instellen op `false` om een bestaande alleen-lezen-verbindingsarray te verwijderen uit de `env.php` bestand.

```yaml
stage:
  deploy:
    MYSQL_USE_SLAVE_CONNECTION: true
```

Wanneer de `MYSQL_USE_SLAVE_CONNECTION` variable is ingesteld op `true`de `synchronous_replication` parameter is ingesteld op `true` standaard in de `env.php` bestand op Pro Staging- en Productomgevingen. Wanneer de `MYSQL_USE_SLAVE_CONNECTION` is ingesteld op `false`de `synchronous_replication` parameter wordt niet gevormd.

## `QUEUE_CONFIGURATION`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.1.4 en hoger

Gebruik deze omgevingsvariabele om aangepaste AMQP-service-instellingen tussen implementaties te behouden. Als u bijvoorbeeld liever een bestaande berichtwachtrij gebruikt in plaats van dat u de cloudinfrastructuur gebruikt om deze voor u te maken, gebruikt u de `QUEUE_CONFIGURATION` omgevingsvariabele om deze aan te sluiten op uw site:

```yaml
stage:
  deploy:
    QUEUE_CONFIGURATION:
      amqp:
        host: test.host
        port: 1234
      amqp2:
        host: test.host2
        port: 12345
      mq:
        host: mq.host
        port: 1234
```

{{merge-options}}

In het volgende voorbeeld worden nieuwe waarden samengevoegd met een bestaande configuratie:

```yaml
stage:
  deploy:
    QUEUE_CONFIGURATION:
      _merge: true
      amqp:
        host: changed1.host
        port: 5672
      amqp2:
        host: changed2.host2
        port: 12345
      mq:
        host: changedmq.host
        port: 1234
```

## `REDIS_BACKEND`

- **Standaard**—`Cm_Cache_Backend_Redis`
- **Versie**—Adobe Commerce 2.3.0 en hoger

Specificeert de achtergrondmodelconfiguratie voor het geheime voorgeheugen van Redis.

Adobe Commerce versie 2.3.0 en hoger bevat de volgende back-endmodellen:

- `Cm_Cache_Backend_Redis`
- `\Magento\Framework\Cache\Backend\Redis`
- `\Magento\Framework\Cache\Backend\RemoteSynchronizedCache`

Het voorbeeld hoe u instelt `REDIS_BACKEND`

```yaml
stage:
  deploy:
    REDIS_BACKEND: '\Magento\Framework\Cache\Backend\RemoteSynchronizedCache'
```

>[!NOTE]
>
>Als u `\Magento\Framework\Cache\Backend\RemoteSynchronizedCache` als het Redis-back-endmodel [L2-cache](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/level-two-cache.html), `ece-tools` genereert automatisch de cachemonfiguratie. Zie een voorbeeld [configuratiebestand](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/level-two-cache.html#configuration-example) in de _Adobe Commerce-configuratiegids_. Om de geproduceerde geheim voorgeheugenconfiguratie met voeten te treden, gebruik [CACHE_CONFIGURATION](#cache_configuration) implementeert variabele.

## `REDIS_USE_SLAVE_CONNECTION`

- **Standaard**—`false`
- **Versie**—Adobe Commerce 2.1.16 en hoger

>[!WARNING]
>
>Do _niet_ deze variabele inschakelen op een [geschaalde architectuur](../architecture/scaled-architecture.md) project. Dit veroorzaakt verbindingsfouten van Redis. Redis-slaven zijn nog steeds actief, maar worden niet gebruikt voor Redis-lezen. Als alternatief raadt de Adobe aan Adobe Commerce 2.3.5 of hoger te gebruiken, een nieuwe Redis-back-endconfiguratie te implementeren en L2-caching voor Redis te implementeren.

>[!TIP]
>
>De `REDIS_USE_SLAVE_CONNECTION` Variabele wordt alleen ondersteund in Adobe Commerce op staging- en Production Pro-clusteromgevingen met cloudinfrastructuur en wordt niet ondersteund in Starter-projecten.

Adobe Commerce kan meerdere Redis-instanties asynchroon lezen. Instellen op `true` om automatisch een _alleen-lezen_ verbinding met een instantie Redis om alleen-lezen verkeer op een niet-hoofdknooppunt te ontvangen. Deze verbinding verbetert prestaties door lading het in evenwicht brengen, omdat slechts één knoop lees-schrijf verkeer behandelt. Instellen op `false` om een bestaande alleen-lezen-verbindingsarray te verwijderen uit de `env.php` bestand.

```yaml
stage:
  deploy:
    REDIS_USE_SLAVE_CONNECTION: true
```

U moet een Redis-service hebben geconfigureerd in het dialoogvenster `.magento.app.yaml` en in het `services.yaml` bestand.

[ECE-Tools versie 2002.0.18](../release-notes/cloud-release-archive.md#v2002018) en gebruikt later meer fouttolerantie. Als Adobe Commerce geen gegevens van Redis kan lezen _slaven_ -instantie, leest het vervolgens gegevens van Redis _meester_ -instantie.

De alleen-lezen verbinding is niet beschikbaar voor gebruik in de integratieomgeving of als u de [`CACHE_CONFIGURATION` variabel](#cache_configuration).

## `RESOURCE_CONFIGURATION`

- **Standaard**—Niet ingesteld
- **Versie**—Adobe Commerce 2.1.4 en hoger

Wijst een middelnaam aan een gegevensbestandverbinding toe. Deze configuratie komt overeen met de `resource` van de `env.php` bestand.

{{merge-options}}

In het volgende voorbeeld worden nieuwe waarden samengevoegd met een bestaande configuratie:

```yaml
stage:
  deploy:
    RESOURCE_CONFIGURATION:
      _merge: true
      default_setup:
        connection: default
```

## `SCD_COMPRESSION_LEVEL`

- **Standaard**—`4`
- **Versie**—Adobe Commerce 2.1.4 en hoger

Hiermee wordt opgegeven welke [gzip](https://www.gnu.org/software/gzip) compressieniveau (`0` tot `9`) te gebruiken bij het comprimeren van statische inhoud; `0` Schakelt compressie uit.

```yaml
stage:
  deploy:
    SCD_COMPRESSION_LEVEL: 5
```

## `SCD_COMPRESSION_TIMEOUT`

- **Standaard**—`600`
- **Versie**—Adobe Commerce 2.1.4 en hoger

Wanneer de tijd die nodig is om de statische elementen te comprimeren, de time-outlimiet voor compressie overschrijdt, wordt het implementatieproces onderbroken. Stel de maximale uitvoeringstijd, in seconden, in voor de opdracht voor het comprimeren van statische inhoud.

```yaml
stage:
  deploy:
    SCD_COMPRESSION_TIMEOUT: 800
```

## `SCD_MATRIX`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.1.4 en hoger

U kunt meerdere landinstellingen per thema configureren. Deze aanpassing versnelt het implementatieproces door het aantal onnodige themabestanden te verminderen. U kunt bijvoorbeeld de _magento/backend_ thema in het Engels en een aangepast thema in andere talen.

In het volgende voorbeeld wordt het `Magento/backend` thema met drie landinstellingen:

```yaml
stage:
  deploy:
    SCD_MATRIX:
      "magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

U kunt ook _niet_ Stel een thema op:

```yaml
stage:
  deploy:
    SCD_MATRIX:
      "magento/backend": [ ]
```

## `SCD_MAX_EXECUTION_TIME`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.2.0 en hoger

Staat u toe om de maximale verwachte uitvoeringstijd voor statische inhoudsplaatsing te verhogen.

Door gebrek, plaatst Adobe Commerce de maximum verwachte uitvoering aan 900 seconden, maar in sommige scenario&#39;s zou u meer tijd kunnen nodig hebben om de statische inhoudsplaatsing voor een project van de Wolk te voltooien.

```yaml
stage:
  deploy:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_NO_PARENT`

- **Standaard**—`false`
- **Versie**—Adobe Commerce 2.4.2 en hoger

Voor de opstellen fase, reeks `SCD_NO_PARENT: true` zodat het genereren van statische inhoud voor bovenliggende thema&#39;s niet plaatsvindt tijdens de implementatiefase. Dit het plaatsen minimaliseert plaatsingstijd en verhindert plaatsonderbreking die kan voorkomen als de statische inhoud tijdens de plaatsing bouwt ontbreekt. Zie [Statische implementatie van inhoud](../deploy/static-content.md).

```yaml
stage:
  deploy:
    SCD_NO_PARENT: true
```

## `SCD_STRATEGY`

- **Standaard**—`quick`
- **Versie**—Adobe Commerce 2.2.0 en hoger

Hiermee kunt u de [implementatiestrategie](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-strategy.html) voor statische inhoud. Zie [Statische weergavebestanden gebruiken](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html).

Deze opties gebruiken _alleen_ als u meerdere landinstellingen hebt:

- `standard`—implementeert alle statische weergavebestanden voor alle pakketten.
- `quick`—(_default_) minimaliseert de implementatietijd.
- `compact`—bespaart schijfruimte op de server. In Adobe Commerce versie 2.2.4 en eerder overschrijft deze instelling de waarde voor `scd_threads` met een waarde van `1`.

```yaml
stage:
  deploy:
    SCD_STRATEGY: "compact"
```

## `SCD_THREADS`

- **Standaard**—Automatisch
- **Versie**—Adobe Commerce 2.1.4 en hoger

Plaatst het aantal draden voor statische inhoudsplaatsing. De standaardwaarde wordt geplaatst gebaseerd op de ontdekte de draadtelling van cpu en overschrijdt geen waarde van 4. Verhoog het aantal draden versnelt de statische plaatsing van inhoud; het verminderen van het aantal draden vertraagt het. U kunt bijvoorbeeld de waarde van de thread instellen:

```yaml
stage:
  deploy:
    SCD_THREADS: 2
```

Gebruik [Configuratiebeheer](../store/store-settings.md) met de `scd-dump` bevel om statische plaatsing in de bouwstijlfase te bewegen.

## `SEARCH_CONFIGURATION`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.1.4 en hoger

Gebruik deze omgevingsvariabele om aangepaste instellingen voor zoekservices tussen implementaties te behouden. Bijvoorbeeld:

Configuratie Elasticsearch:

```yaml
stage:
  deploy:
   SEARCH_CONFIGURATION:
     engine: elasticsearch
     elasticsearch_server_hostname: http://elasticsearch.internal
     elasticsearch_server_port: '9200'
     elasticsearch_index_prefix: magento2
     elasticsearch_server_timeout: '15'
```

OpenSearch configuratie (voor Handel 2.4.6 en later):

```yaml
stage:
  deploy:
   SEARCH_CONFIGURATION:
     engine: opensearch
     opensearch_server_hostname: 'http://opensearch.internal'
     opensearch_server_port: '9200'
     opensearch_index_prefix: 'magento2'
     opensearch_server_timeout: '15'
```

{{merge-options}}

In het volgende voorbeeld wordt een nieuwe waarde samengevoegd met de bestaande configuratie:

```yaml
stage:
  deploy:
    SEARCH_CONFIGURATION:
      engine: elasticsearch
      elasticsearch_server_port: '9200'
      _merge: true
```

## `SESSION_CONFIGURATION`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.1.4 en hoger

Configureer de Redis-sessieopslag. Vereist de `save`, `redis`, `host`, `port`, en `database` opties voor de sessieopslagvariabele. Bijvoorbeeld:

```yaml
stage:
  deploy:
    SESSION_CONFIGURATION:
      redis:
        bot_first_lifetime: 100
        bot_lifetime: 10001
        database: 0
        disable_locking: 1
        host: redis.internal
        max_concurrency: 10
        max_lifetime: 10001
        min_lifetime: 100
        port: 6379
      save: redis
```

{{merge-options}}

In het volgende voorbeeld wordt een nieuwe waarde samengevoegd met de bestaande configuratie:

```yaml
stage:
  deploy:
    SESSION_CONFIGURATION:
      _merge: true
      redis:
        max_concurrency: 10
```

## `SKIP_SCD`

- **Standaard**— _Niet ingesteld_
- **Versie**—Adobe Commerce 2.1.4 en hoger

Instellen op `true` om statische inhoudsplaatsing tijdens de opstellen fase over te slaan.

Voor de opstellen fase, reeks `SKIP_SCD: true` zodat de statische inhoud bouwt niet tijdens de opstellen fase gebeurt. Dit het plaatsen minimaliseert plaatsingstijd en verhindert plaatsonderbreking die kan voorkomen als de statische inhoud tijdens de plaatsing bouwt ontbreekt. Zie [Statische implementatie van inhoud](../deploy/static-content.md).

```yaml
stage:
  deploy:
    SKIP_SCD: true
```

## `UPDATE_URLS`

- **Standaard**—`true`
- **Versie**—Adobe Commerce 2.1.4 en hoger

Vervang bij implementatie Adobe Commerce basis-URL&#39;s in de database door de project-URL&#39;s die zijn opgegeven door de [`MAGENTO_CLOUD_ROUTES`](variables-cloud.md) variabele. Deze configuratie is handig voor lokale ontwikkeling, waarbij basis-URL&#39;s zijn ingesteld voor uw lokale omgeving. Wanneer u implementeert in een Cloud-omgeving, worden de URL&#39;s bijgewerkt zodat u toegang hebt tot uw winkel en beheerder met de project-URL&#39;s.

Als u URL&#39;s moet bijwerken wanneer u deze implementeert in een Pro- of Starter-staging- en productieomgeving, gebruikt u de opdracht [`FORCE_UPDATE_URLS`](#force_update_urls) variabele.

```yaml
stage:
  deploy:
    UPDATE_URLS: false
```

## `VERBOSE_COMMANDS`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.1.4 en hoger

Schakel de [Symfony](https://symfony.com/doc/current/console/verbosity.html) debug-breedbeeldniveau voor `bin/magento` CLI bevelen die tijdens de plaatsingsfase worden uitgevoerd.

>[!NOTE]
>
>De instelling VERBOSE_COMMANDS gebruiken om de details in de opdrachtuitvoer voor zowel geslaagd als mislukt te beheren `bin/magento` CLI-opdrachten, moet u instellen [MIN_LOGGING_LEVEL](variables-global.md#minlogginglevel) `debug`.

Kies het detailniveau in de logboeken:

- `-v`= normale uitvoer
- `-vv`= uitgebreidere uitvoer
- `-vvv` = uitgebreide uitvoer, ideaal voor foutopsporing

```yaml
stage:
  deploy:
    VERBOSE_COMMANDS: "-vv"
```
