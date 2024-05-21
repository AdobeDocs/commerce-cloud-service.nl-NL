---
title: Opmerkingen bij de release ECE-Tools
description: Zie een lijst met de meest recente verbeteringen in het pakket ECE-Tools.
recommendations: noDisplay, catalog
last-substantial-update: 2024-05-21T00:00:00Z
exl-id: a464b940-c56e-4a7c-9948-559539e25361
source-git-commit: 923e2114270df22e134e0676ac97f84d770bb226
workflow-type: tm+mt
source-wordcount: '2929'
ht-degree: 0%

---

# Opmerkingen bij de release ECE-Tools

De [Gereedschappen](https://github.com/magento/ece-tools) Dit pakket is een set scripts en gereedschappen die zijn ontworpen voor het beheren en implementeren van Cloud-projecten. In deze releaseopmerkingen worden de meest recente verbeteringen van dit pakket beschreven, dat onderdeel is van het [Cloud Tools Suite voor Commerce](cloud-tools-suite.md).

>[!NOTE]
>
>Zie [ECE-gereedschappen upgraden](../dev-tools/update-package.md) voor informatie over de bijwerking van de meest recente versie van de `ece-tools` pakket.

De `ece-tools` Het pakket gebruikt de volgende versiesequentie: `200<major>.<minor>.<patch>`

De opmerkingen bij de release omvatten:

- ![nieuw pictogram](../../assets/new.svg) Nieuwe functies
- ![fixepictogram](../../assets/fix.svg) Oplossingen en verbeteringen

<!--Add release notes below-->

## v2002.1.19 {#latest}

Releasedatum: 21 mei 2024

- ![nieuw pictogram](../../assets/new.svg) **Lua**—Toegevoegde optie useLua voor CACHE_CONFIGURATION.
- ![fixepictogram](../../assets/fix.svg) **Validator**—Bijgewerkte validators voor nieuwe versies van Redis en RabbitMQ.

## v2002.1.18

Releasedatum: 8 april 2024

- ![nieuw pictogram](../../assets/new.svg) **PHP** — Toegevoegde ondersteuning voor PHP 8.3.
- ![fixepictogram](../../assets/fix.svg) Validator - Bijgewerkte EOL-validatie.

## v2002.1.17

Releasedatum: 16 januari 2024

- ![fixepictogram](../../assets/fix.svg) **Validator voor Elasticsearch &amp; OpenSearch**—Oplossing voor een probleem met de validator die een misleidend bericht heeft gegenereerd om een zoekservice te installeren wanneer LiveSearch is ingeschakeld.<!-- MCLOUD-10167 -->
- ![fixepictogram](../../assets/fix.svg) **Waarschuwing bij implementatie**—Probleem verholpen dat leidde tot implementatiewaarschuwingen over niet-lege mappen.<!-- MCLOUD-8958 -->

## v2002.1.16

Releasedatum: 16 oktober 2023

- ![nieuw pictogram](../../assets/new.svg) **ENABLE_WEBHOOKS globale omgevingsvariabele**—Toegevoegd de [ENABLE_WEBHOOKS](../environment/variables-global.md#enable_webhooks) globale variabele voor gebruik met de websites van Commerce om met een extern eindpunt, zoals runtime App Builder actie of een derdevoorraadbeheersysteem te verbinden.

## v2002.1.15

Releasedatum: 31 juli 2023

- ![fixepictogram](../../assets/fix.svg) **Foutcodes**—Bijgewerkt foutencodeschema en de generator van het foutencodedocument.
- ![fixepictogram](../../assets/fix.svg) **Validator voor aangepast Redis-model**-Updated the validator for custom Redis backend models. [Zie het voorbeeld voor geheim voorgeheugenconfiguratie](../environment/variables-deploy.md#cache_configuration).
- ![fixepictogram](../../assets/fix.svg) **Validator voor RabbitMQ**- Toegevoegde ondersteuning voor RabbitMQ 3.11
- ![fixepictogram](../../assets/fix.svg) **De onjuiste koppeling herstellen**- Oplossing voor de onjuiste koppeling naar de instapkaartdocumentatie in de welkomstsjabloon voor e-mail.

## v2002.1.14

Releasedatum: 10 maart 2023

- ![nieuw pictogram](../../assets/new.svg) **PHP**—Toegevoegde ondersteuning voor PHP 8.2.
- ![nieuw pictogram](../../assets/new.svg) **Validators voor services**—Bijgewerkte validators voor Commerce 2.4.6 vereiste services: MariaDB 10.6, Redis 7.0, PHP 8.2, OpenSearch 2.x en RabbitMQ 3.9.
- ![fixepictogram](../../assets/fix.svg) **ece-tools db-dump**—Oplossing voor een probleem dat de `db-dump` om voortijdig te stoppen.

## v2002.1.13

Releasedatum: 27 oktober 2022

- ![nieuw pictogram](../../assets/new.svg) **Toegevoegde ondersteuning voor Adobe I/O Events voor Adobe Commerce**. Extensieontwikkelaars kunnen nu de opdracht [Adobe I/O Events](https://developer.adobe.com/events/docs/) framework om Commerce-gebeurtenisinformatie van Cloud-instanties te verzenden naar hun toepassingen die zijn geschreven voor [Adobe App Builder](https://developer.adobe.com/app-builder/docs/overview/). Adobe I/O Gebeurtenissen voor Adobe Commerce bevinden zich in Voorvertoning voor partners.<!-- CEXT-932 -->
- ![nieuw pictogram](../../assets/new.svg) **Validator voor OPcache-configuratie**—Een validator toegevoegd om de OPcache-configuratie te controleren op uitgesloten paden.<!-- MCLOUD-9485 -->
- ![fixepictogram](../../assets/fix.svg) **Probleem verholpen met GraphQL-cacheconfiguratie**—Nu houdt ECE-Tools de GraphQL `id_salt` waarde in `cache` in de `app/etc/env.php` bestand.<!-- MCLOUD-9486 -->

## v2002.1.12

Releasedatum: 13 september 2022

- ![nieuw pictogram](../../assets/new.svg) **Inschakelen`synchronous_replication`**—ECE-gereedschapssets `synchronous_replication=>true` in de `app/etc/env.php` bestand wanneer `MYSQL_USE_SLAVE_CONNECTION` is ingeschakeld. Deze configuratie heeft alleen invloed op Commerce 2.4.6+. Zie de `MYSQL_USE_SLAVE_CONNECTION` variabele beschrijving in de [Variabelen implementeren](../environment/variables-deploy.md#mysql_use_slave_connection).<!-- MCLOUD-9142 -->
- ![nieuw pictogram](../../assets/new.svg) **OpenSearch**—Toegevoegde functionaliteit om het `opensearch` motor voor de volgende Adobe Commerce-release 2.4.6. Zie [OpenSearch-service instellen](../services/opensearch.md).<!-- MCLOUD-9236 -->

## v2002.1.11

Releasedatum: 4 augustus 2022

- ![fixepictogram](../../assets/fix.svg) **ElasticSuite-validatie en OpenSearch**—Fixed ElasticSuite integriteitscontrole validator issue when OpenSearch is installed.<!-- MCLOUD-8767 -->
- ![fixepictogram](../../assets/fix.svg) **Terugkeertypen voor implementatieopdrachten**—Vaste terugkeertypes voor opstellen bevelen.<!-- AC-3208 -->
- ![fixepictogram](../../assets/fix.svg) **[!DNL RabbitMQ]probleem met nieuwe Commerce 2.4.5-installatie**—Vast [!DNL RabbitMQ] crash probleem bij nieuwe Commerce 2.4.5. installatie.<!-- MCLOUD-9059 -->

## v2002.1.10

Releasedatum: 31 maart 2022

- ![fixepictogram](../../assets/fix.svg) **Elasticsearch 7.10**—Bijgewerkte validators ter ondersteuning van de versie 7.10 van Elasticsearch.<!-- MCLOUD-8548 -->

## v2002.1.9

Releasedatum: 10 maart 2022

- ![nieuw pictogram](../../assets/new.svg) **OpenSearch**—Toegevoegde ondersteuning voor OpenSearch voor Adobe Commerce versies 2.4.4, 2.4.3-p2 en 2.3.7-p3.<!-- MCLOUD-8296 -->
- ![nieuw pictogram](../../assets/new.svg) **PHP**—Toegevoegde ondersteuning voor PHP 8.1.
- ![fixepictogram](../../assets/fix.svg) **symfonie/proces**—De compatibiliteit met symfony/proces ^5.3 is toegevoegd.<!-- MCLOUD-8283 -->

- ![nieuw pictogram](../../assets/new.svg) **Meerdere processen voor consumenten**—Toegevoegd a `multiple_processes` zodat u het aantal processen kunt specificeren om voor elke consument te kweken. Zie de `CRON_CONSUMERS_RUNNER` variabele beschrijving in de [Variabelen implementeren](../environment/variables-deploy.md#cron_consumers_runner).<!-- MCLOUD-8295 -->
- ![nieuw pictogram](../../assets/new.svg) **OpenSearch-schema en volledig hostpad**—Toegevoegd de capaciteit om een regeling van de Elasticsearch en volledige gastheerweg te vormen.
- ![fixepictogram](../../assets/fix.svg) **AWS S3**—Veranderde methode van AWS S3 enablement.
- ![fixepictogram](../../assets/fix.svg) **Reader voor stuurprogramma_opties herstellen**—Toegevoegde het lezen driver_options configuratie voor de verbinding van DB van `env.php` bestand op `ece-tools` voor validators.<!-- MCLOUD-8420 -->

## v2002.1.8

Releasedatum: 25 oktober 2021

- ![nieuw pictogram](../../assets/new.svg) **Alternatieve stortplaats**—Toegevoegd de `--dump-directory` zodat u een doelmap voor een DB-dump kunt kiezen. Nu `/app/var/dump-main` is de standaarddoeldirectory voor een DB-dump. Zie [Back-upbeheer: de database dumpen](../storage/database-dump.md)<!-- MCLOUD-8063 -->
- ![fixepictogram](../../assets/fix.svg) **Monolog bijwerken**—De minimale versie die vereist is voor de `monolog` verpakken naar `^2.3`.<!-- ACMP-1263 -->
- ![fixepictogram](../../assets/fix.svg) **Symfony bijwerken**—De Symfony-afhankelijkheden zijn bijgewerkt om compatibel te zijn met Adobe Commerce 2.4.4.<!-- ACMP-1533 -->
- ![fixepictogram](../../assets/fix.svg) **Functie/oplossing automatisch laden**—Oplossing voor een probleem bij de implementatie naar een integratieomgeving en het bekijken van de `CRITICAL: [9] Required configuration is missed in autoload section of composer.json file.` fout.<!-- https://github.com/magento/ece-tools/pull/799 -->

## v2002.1.7

Releasedatum: 29 juli 2021

**Configuratie-updates**—

- ![nieuw pictogram](../../assets/new.svg) Toegevoegde ondersteuning voor Composer 2.0.<!--MCLOUD-8003-->

- ![fixepictogram](../../assets/fix.svg) **Bijgewerkte componentenvereisten voor`symphony/console`**—Bijgewerkt ECE-tools `composer.json` versievereisten voor de `symphony/console` pakket maken om een probleem te verhelpen dat de `di:compile` opdrachten die mislukken met de volgende fout: `Incompatible argument type: Required type: int. Actual type: string`<!--MC-42919-->

- ![fixepictogram](../../assets/fix.svg) Bijgewerkte softwarecontroles aan het einde van de levensduur (`eol.yaml`) om Elasticsearch 7.9.x op te nemen.<!--MCLOUD-7938-->

## v2002.1.6

Releasedatum: 20 april 2021

- ![nieuw pictogram](../../assets/new.svg) **Verificatiegegevens opnieuw verzenden**—De mogelijkheid om Redis-autorisatiegegevens te lezen is toegevoegd door de `relationships` bezit tijdens de opstellen fase.<!--MCLOUD-7694-->

- ![nieuw pictogram](../../assets/new.svg) **Autorisatiegegevens Elasticsearch**—De mogelijkheid toegevoegd om de autorisatiegegevens van de Elasticsearch te lezen van de `relationships` bezit tijdens de opstellen fase.<!--MCLOUD-7695-->

- ![nieuw pictogram](../../assets/new.svg) **Speciale service voor sessieopslag**—Toegevoegd `redis-session` als tweede optie voor sessieopslag. U kunt de `redis-session` service voor het opslaan van sessiegegevens en het gebruik van de `redis` service voor cache om betere prestaties te bieden.<!--MCLOUD-7698-->

- ![nieuw pictogram](../../assets/new.svg) **Vervangen SPLIT_DB-berichten**—Waarschuwing voor validatie toegevoegd en kritieke berichten voor de vervangen validator `SPLIT_DB` voor Adobe Commerce 2.4.2 en de verwijdering ervan in Adobe Commerce 2.5.0.<!--MCLOUD-7806-->

- ![fixepictogram](../../assets/fix.svg) **Versie van Elasticsearch van relaties**—Fixed Service validator om de juiste versie van Elasticsearch op te halen van de `relationships` eigenschappen in Cloud Docker- en integratieomgevingen.<!--MCLOUD-7572-->

- ![fixepictogram](../../assets/fix.svg) **Flexibele poortvalidatie van Redis**—Redis kan de poort nu valideren via een aangepaste cacheverbinding via de `server` URL. U kunt bijvoorbeeld als volgt uw poortnummer aan de URL van de server toevoegen: `server: 'tcp://rfs-store-simple-page-cache:26379'`. Hierdoor voorkomt u validatiefouten waarbij de `port` deze optie ontbreekt of is onjuist.<!--MCLOUD-7722-->

- ![fixepictogram](../../assets/fix.svg) **Upgrade uitvoeren naar Adobe Commerce 2.4.2**—Oplossing voor het probleem dat vereiste dat gebruikers handmatig moesten uitvoeren `bin/magento setup:upgrade` hun sites operationeel te maken na de upgrade naar Adobe Commerce 2.4.2.<!--MCLOUD-7776-->

## v2002.1.5

Releasedatum: 1 februari 2021

- ![nieuw pictogram](../../assets/new.svg) **Externe opslag**—Toegevoegd de `REMOTE_STORAGE` omgevingsvariabele om Cloud Projecten voor externe opslag van mediabestanden in te schakelen met behulp van een opslagservice, zoals AWS S3. Deze configuratieoptie maakt deel uit van het pakket ECE-Tools, maar wordt niet ondersteund door Adobe Commerce op cloudinfrastructuur.<!--MCLOUD-7153-->

- ![nieuw pictogram](../../assets/new.svg) **Nieuw `cloud:config:validate` command**—Toegevoegd, opdracht `php vendor/bin/ece-tools cloud:config:validate` om de `.magento.env.yaml` voordat u wijzigingen aanbrengt in de externe cloud-omgeving.<!--MCLOUD-7120-->

- ![nieuw pictogram](../../assets/new.svg) **Het opcache spoelen**—Toegevoegde ondersteuning voor de `opcache.enable_cli` PHP optie om OPcache te spoelen alvorens de op-implementatiehaak uit te voeren. Deze configuratie stelt de geheim voorgeheugenconfiguratie terug om ervoor te zorgen dat de huidige configuratiemontages op elke plaatsing worden toegepast.<!--MCLOUD-7015-->

- ![nieuw pictogram](../../assets/new.svg) **Validatie van Aurora DB**—De validatie van de databaseservice is bijgewerkt zodat deze compatibel is met de Aurora-database.<!--MCLOUD-7269-->

- ![nieuw pictogram](../../assets/new.svg) **Nieuwe SCD_NO_PARENT-omgevingsvariabele**—Toegevoegd de `SCD_NO_PARENT` omgevingsvariabele (voor Adobe Commerce >=2.4.2) voor het beheren van het genereren van statische inhoud voor bovenliggende thema&#39;s.<!--MCLOUD-7284-->

- ![fixepictogram](../../assets/fix.svg) **Geheugenbeperkingen en opdrachten**—Oplossing voor een probleem waarbij `php vendor/bin/ece-tools` werken niet als de grootte van de `cloud.log` bestand overschrijdt de PHP memory_limit. In plaats van het gehele document te lezen `cloud.log` in het geheugen, lezen wij nu slechts een kleinere ondergroep gegevens van het logboekdossier.<!--MCLOUD-7275--><!--MCLOUD-7400-->

- ![fixepictogram](../../assets/fix.svg) **Aangepaste databaseverbindingen**—Vast a `.magento.env.yaml` configuratieprobleem waarbij aangepaste databaseverbindingen zijn gedefinieerd voor `DATABASE_CONFIGURATION` zijn niet gebruikt. De verbindingsinstellingen zijn niet toegevoegd aan `app/etc/env.php`.<!--MCLOUD-7426-->

- ![fixepictogram](../../assets/fix.svg) **Lege foutlogboeken**—Oplossing van een probleem dat ertoe leidde dat implementaties mislukten als de `cloud.error.log` was leeg.<!--MCLOUD-7296-->

- ![fixepictogram](../../assets/fix.svg) **MariaDB 10.3-validatie**—Vaste validatie van MariaDB 10.3 voor Adobe Commerce 2.3.6-p1.<!--MCLOUD-7416-->

- ![fixepictogram](../../assets/fix.svg) **Cache:leegmaken**—Verbeterde logbestandvermeldingen om het begin en het einde van de `cache:flush` stap.<!--MCLOUD-7503-->

## v2002.1.4

Releasedatum: 19 november 2020

- ![fixepictogram](../../assets/fix.svg) Probleem opgelost waarbij de implementatie mislukte als het zoekprogramma dat in het dialoogvenster `SEARCH_CONFIGURATION` omgevingsvariabele is een andere waarde dan `elasticsearch`.<!--MCLOUD-7283-->

## v2002.1.3

Releasedatum: 9 november 2020

**Infrastructuurupdates**—

- ![nieuw pictogram](../../assets/new.svg) Toegevoegde ECE-Tools steun voor read-only `pub/static` directory wanneer de statische inhoud wordt geplaatst om in het bouwstijlstadium op te stellen.<!--MC-37699-->

- ![nieuw pictogram](../../assets/new.svg) Extra ondersteuning voor Elasticsearch 7.9 en Redis 6 voor compatibiliteit met komende Adobe Commerce-releases.<!--MCLOUD-7191-->

- ![fixepictogram](../../assets/fix.svg) De ECE-tools zijn bijgewerkt `composer.json` om een vereiste afhankelijkheid voor het Hulpmiddel van de Patches van de Kwaliteit toe te voegen. Hiermee verhelpt u een cirkelafhankelijkheid tussen de pakketten ECE-Tools en magento-cloud-patches.<!--MCLOUD-6910-->

**Verbeteringen voor validatie en logbestand**—

- ![nieuw pictogram](../../assets/new.svg) Toegevoegde onderzoek-motor bevestiging om ervoor te zorgen dat `elasticsearch` is ingesteld voor Adobe Commerce op cloudinfrastructuur 2.4 en hoger. Als de bevestiging ontbreekt, wordt de plaatsing tegengehouden met een kritiek foutenbericht dat oplossingen voor de kwestie voorstelt. Zie [Kritieke fouten, werkgebied implementeren](../dev-tools/error-reference.md#deploy-stage).<!--MCLOUD-6937-->

- ![nieuw pictogram](../../assets/new.svg) Toegevoegde Elasticsearch bevestiging om de verenigbaarheid tussen de de dienstversie van de Elasticsearch en de versie van Adobe Commerce te controleren.<!--MCLOUD-7193-->

- ![nieuw pictogram](../../assets/new.svg) Het foutbericht voor de compatibiliteit van de Elasticsearch is bijgewerkt om de versies van Elasticsearch weer te geven die compatibel zijn met de module Adobe Commerce Elasticsearch. Het foutbericht bevat nu de specifieke versies voor Elasticsearch die in uw Cloud-infrastructuur moeten worden geïnstalleerd, zodat deze compatibel zijn met de module Elasticsearch die door uw versie van Adobe Commerce wordt gebruikt. Zie [Waarschuwingsfouten, werkgebied implementeren](../dev-tools/error-reference.md#deploy-stage-1).<!--MCLOUD-6698-->

- ![nieuw pictogram](../../assets/new.svg) Toegevoegde waarschuwingsfouten `2026` en `2027` for invalid `MAGE_MODE` instelling omgevingsvariabele. De enige geldige waarde is `production`. Voor deze correctie `MAGE_MODE` kan worden ingesteld op `developer` zonder implementatiefouten, alleen om later fouten te veroorzaken bij het schrijven naar alleen-lezen bestanden. Zie [Waarschuwingsfouten](../dev-tools/error-reference.md#warning-errors).<!--MCLOUD-6708-->

- ![fixepictogram](../../assets/fix.svg) Correctie van validatie voor Redis-, RabbitMQ- en MySQL-services om ervoor te zorgen dat deze versies compatibel zijn met de Adobe Commerce-versie. De geldige versies van deze diensten worden nu geschreven aan `cloud.log`.<!--MCLOUD-7098-->

- ![fixepictogram](../../assets/fix.svg) De `cloud.log` om de gezamenlijke verzoekgrens voor het verzenden van verzoeken tijdens geheim voorgeheugenwarmte op te nemen. Deze waarde is geconfigureerd in het dialoogvenster [WARM_UP_CONCURRENCY](../environment/variables-post-deploy.md#warm_up_concurrency) variabele voor na implementatie.<!--MCLOUD-5563-->

**CLI-opdrachtupdates**—

- ![nieuw pictogram](../../assets/new.svg) Toegevoegde CLI-opdrachten (`cloud:config:create` en `cloud:config:update`) om de `.magento.env.yaml` dossier met een configuratie die één of meerdere bouwstijl kan omvatten, stelt, en post-opstelt variabelen op. Zie [Configuratiebestand maken van CLI](../environment/configure-env-yaml.md#create-configuration-file-from-cli).<!--MCLOUD-7072-->

**Updates van omgevingsvariabelen**—

- ![nieuw pictogram](../../assets/new.svg) De [SKIP_COMPOSER_DUMP_AUTOLOAD](../environment/variables-build.md#skip_composer_dump_autoload) bouwstijlvariabele. De variabele instellen op `true` voorkomt dat de toepassing het `composer dump-autoload` gebruiken tijdens een installatie van Cloud Docker voor Commerce. De variabele is alleen relevant voor Cloud Docker voor Commerce-containers met schrijfbare bestandssystemen (gemaakt voor testen en ontwikkelen met `./vendor/bin/ece-docker build:compose --with-test`). Met dergelijke installaties slaat u de `composer dump-autoload` voorkomt fouten bij het uitvoeren van andere opdrachten die bestanden proberen te openen vanuit een verwijderde `generated` directory.<!--MCLOUD-6939-->

## v2002.1.2

Releasedatum: 5 augustus 2020

**Verbeteringen voor validatie en logbestand**—

- ![nieuw pictogram](../../assets/new.svg) De `schema.error.yaml` een bestand dat alle fout- en waarschuwingsmeldingen bevat die tijdens het proces voor het maken, implementeren en na de implementatie kunnen optreden, samen met suggesties voor het oplossen van de fouten. De informatie in dit bestand is ook beschikbaar in het dialoogvenster _Cloud Guide voor Commerce_. Zie [Referentie van foutbericht voor Griekenland-tools](../dev-tools/error-reference.md).<!--MCLOUD-5878-->

- ![nieuw pictogram](../../assets/new.svg) Het foutenlogboek voor de cloud is gewijzigd (`/var/log/cloud.error.log`) worden ingevoerd in de indeling JSON, zodat het logboek beter programmatisch kan worden geparseerd.<!--MCLOUD-5879-->

- ![nieuw pictogram](../../assets/new.svg) Extra foutcontroles toegevoegd voor het samenstellen, implementeren en achteraf implementeren van verwerking en verbeterde bestaande controles:

   - Foutcode 2026—Kan sommige gegevens die tijdens de constructiefase zijn gegenereerd, niet herstellen naar de gekoppelde mappen

   - Foutcode 3004—Kan geen back-upbestanden maken

   - Foutcode 102: extra controles toegevoegd voor problemen die optreden wanneer de opdracht `env.php` bestand is niet beschrijfbaar <!--MCLOUD-6221-->

- ![nieuw pictogram](../../assets/new.svg) De **QUALITY_PATCH** omgevingsvariabele om een of meer kwaliteitspatches op te geven die tijdens het implementatieproces moeten worden toegepast. Zie [Variabelen samenstellen](../environment/variables-build.md#quality_patches).<!--MCLOUD-6375-->

## v2002.1.1

Releasedatum: 25 juni 2020

- ![nieuw pictogram](../../assets/new.svg) **Infrastructuurupdates**—

   - ![nieuw pictogram](../../assets/new.svg) **Verbeteringen voor logboekregistratie**—Verbeterde logtraceringscapaciteit door afsluitcodes toe te wijzen aan kritieke implementatiefouten en de afsluitcodes weer te geven in foutmeldingen en loggebeurtenissen. Zie [Referentie van foutbericht voor Griekenland-tools](../dev-tools/error-reference.md).<!-- MCLOUD-5637, 5531-->

   - ![nieuw pictogram](../../assets/new.svg) Verbeterd proces voor database-dumps (`vendor/bin/ece-tools db-dump`) en bijgewerkte logboekberichten om te verduidelijken dat de verrichting van de gegevensbestandstortplaats de toepassing aan onderhoudswijze schakelt, de processen van de consumentenrij tegenhoudt, en bouwstijlbanen onbruikbaar maakt alvorens de stortplaats begint.<!--MCLOUD-5324, MCLOUD-2062-->

   - ![fixepictogram](../../assets/fix.svg) Probleem verholpen om ervoor te zorgen dat de project-URL correct wordt bijgewerkt wanneer het opstellen aan het Opvoeren en milieu&#39;s van de Productie. Nu, `ece-tools` gebruikt URL voor de route met `primary:true` attributen in de configuratie van de projectroute worden geplaatst die. Zie [Variabelen implementeren](../environment/variables-deploy.md#update_urls).<!--MCLOUD-5883-->

   - ![fixepictogram](../../assets/fix.svg) De `generate.xml` workflows voor het samenstellen van scenario&#39;s voor het toepassen van patches. Patches moeten eerder worden toegepast om Adobe Commerce bij te werken en eventuele problemen op te lossen die de `di:compile` en `module:refresh` stappen die moeten mislukken.<!--MCLOUD-5941-->

   - ![fixepictogram](../../assets/fix.svg) Probleem verholpen tijdens het installatieproces waarbij de fout onjuist wordt geretourneerd. `Crypt key missing` fout. De `crypt/key` Deze waarde wordt automatisch tijdens de installatie gegenereerd.<!--MCLOUD-6120-->

- ![nieuw pictogram](../../assets/new.svg) **Service-updates**—

   - ![nieuw pictogram](../../assets/new.svg) Extra ondersteuning voor PHP 7.4 en MariaDB 10.4.<!--MAGECLOUD-2957, MCLOUD-4144-->

- ![nieuw pictogram](../../assets/new.svg) **Updates van omgevingsvariabelen**—

   - ![nieuw pictogram](../../assets/new.svg) De **SCD_USE_BALER** variabele om de Baler-module in te schakelen voor JavaScript-bundeling tijdens het Adobe Commerce-proces voor het bouwen van cloudinfrastructuur. Zie de beschrijving van de variabele in het dialoogvenster [build-variabelen](../environment/variables-build.md#scd_use_baler).<!-- MCLOUD-3456, MCLOUD-3457-->

   - ![nieuw pictogram](../../assets/new.svg) De **REDIS_BACKEND** omgevingsvariabele om het Redis-back-endmodel voor Redis-cache voor Adobe Commerce 2.3.5 of hoger te configureren. Zie de beschrijving van de variabele in het dialoogvenster [variabelen implementeren](../environment/variables-deploy.md#redis_backend).<!--MCLOUD-5721, MCLOUD-5865-->

- ![nieuw pictogram](../../assets/new.svg) **CLI-opdrachtupdates**—

   - ![nieuw pictogram](../../assets/new.svg) Bijgewerkt de volgende CLI bevelen met een optie voor meer gedetailleerd registreren:

      - `app:config:dump`
      - `app:config:import`
      - `module:enable`

     Het registrerenniveau voor elke vraag wordt bepaald door de configuratie van [`VERBOSE_COMMANDS`](../environment/variables-build.md#verbose_commands) in de `.magento.env.yaml` bestand.<!--MCLOUD-3503-->

- ![nieuw pictogram](../../assets/new.svg) **Verbeteringen voor validatie**—

   - ![nieuw pictogram](../../assets/new.svg) **Elasticsearch 7.x-compatibiliteitscontroles**—Bijgewerkte validatie van Elasticsearch voor Elasticsearch 7.x software compatibiliteitscontroles.<!--MCLOUD-5542-->

   - ![nieuw pictogram](../../assets/new.svg) **Updated service version and EOL validation checks**—Bijgewerkte validatie om geïnstalleerde serviceversies te controleren aan de hand van Adobe Commerce 2.4.-vereisten.<!--MCLOUD-6144-->

   - ![fixepictogram](../../assets/fix.svg) Probleem met validatie verholpen zodat het volgende post-implementatiewaarschuwingsbericht alleen wordt weergegeven als de `post-deploy` haakconfiguratie ontbreekt in de `.magento.app.yaml` bestand:

     ```text
     Your application does not have the "post_deploy" hook enabled.
     ```

     <!--MCLOUD-4077-->

   - ![nieuw pictogram](../../assets/new.svg) **Toegevoegde validatie voor Zend Framework-afhankelijkheden**—Toegevoegde componentenafhankelijkheidsvalidering voor het Zend Framework dat naar het Laminas-project is gemigreerd. Als de vereiste gebiedsdelen ontbreken, toont het volgende foutenbericht tijdens het bouwstijlproces.

     ```text
     Required configuration is missing from the autoload section of the composer.json file.
     Add ("Laminas\Mvc\Controller\Zend\": "setupsrc/ Zend/Mvc/Controller/") to
     the `autoload -> psr-4` section. Then, re-run the "composer update" command locally, and
     commit the updated composer.json and composer.lock files.
     ```

     Zie [Afhankelijkheden van Zend Framework verifiëren](../development/commerce-version.md#verify-zend-framework-composer-dependencies).<!--MCLOUD-4094-->

   - ![nieuw pictogram](../../assets/new.svg) **Toegevoegde validatie voor `env.php` bestand en gegevens**—Toegevoegde controles voor de `env.php` en gegevens tijdens het installatie- en upgradeproces.<!--MCLOUD-5991-->

      - Als de `env.php` het bestand ontbreekt in de installatie en de `crypt/key` waarde wordt niet opgegeven in het dialoogvenster `.magento.app.yaml` , mislukt de implementatie met de volgende melding:

        ```text
        The crypt/key key value does not exist in the ./app/etc/env.php file or the CRYPT_KEY cloud environment variable``Missing crypt key for upgrading Magento`.
        ```

      - Als de installatie geen `env.php` of de configuratie slechts één cachetype bevat, `cron:enable` de opdracht wordt uitgevoerd tijdens het upgradeproces om het bestand te herstellen met alle `cache_types`. Het volgende bericht wordt toegevoegd aan het logboek:

        ```text
        Magento state indicated as installed but configuration file app/etc/env.php was empty or did not exist.
        Required data will be restored from environment configurations and from the .magento.env.yaml file.
        ```

## v2002.1.0

Releasedatum: 6 februari 2020

- ![nieuw pictogram](../../assets/new.svg) **Infrastructuurupdates**—

   - ![nieuw pictogram](../../assets/new.svg) **Afzonderlijk pakket toegevoegd voor Cloud Docker voor Commerce**—Het Docker-pakket losgekoppeld van het `ece-tools` pakket om de codekwaliteit te behouden en onafhankelijke releases te bieden. Updates en correcties voor `ece-tools` worden beheerd vanuit de [magento-cloud-docker](https://github.com/magento/magento-cloud-docker) GitHub-opslagplaats.<!--MAGECLOUD-2927-->

   - ![nieuw pictogram](../../assets/new.svg) **Bijgewerkte patchmogelijkheden**—De patchfunctionaliteit is verplaatst van het pakket ECE-tools naar een aparte [magento-cloud-patches](https://github.com/magento/magento-cloud-patches) pakket. Tijdens de implementatie `ece-tools` gebruikt het nieuwe pakket om patches toe te passen. Zie [Opmerkingen bij de release Cloud Patches](cloud-patches.md).<!--MAGECLOUD-4567-->

   - ![nieuw pictogram](../../assets/new.svg) **Bijgewerkte componentenafhankelijkheden**—De `composer.json` bestand voor Adobe Commerce op cloudinfrastructuur met een afhankelijkheid voor de `magento/magento-cloud-docker` pakket. Nu, `ece-tools` omvat gebiedsdelen voor alle pakketten in [`Cloud Tools Suite for Commerce`](cloud-tools-suite.md). Deze pakketten worden automatisch geïnstalleerd en bijgewerkt wanneer u ze installeert of bijwerkt `ece-tools`.

- ![nieuw pictogram](../../assets/new.svg) **Ondersteuning voor op scenario&#39;s gebaseerde implementaties**—<!--MAGECLOUD-4101-->

   - ![nieuw pictogram](../../assets/new.svg) Nu kunt u de bouw aanpassen, processen opstellen en post-opstellen gebruikend de configuratiedossiers van XML om de standaardconfiguratie met voeten te treden of aan te passen.

   - ![nieuw pictogram](../../assets/new.svg) **De `hooks` configuratie in`.magento.app.yaml`**—We hebben de `hooks` configuratieformaat om op scenario-gebaseerde plaatsingen te steunen. De oudere indeling van de eerdere release ECE-Tools 2002.0.x wordt nog steeds ondersteund. Nochtans, moet u aan het nieuwe formaat bijwerken om de op scenario-gebaseerde plaatsingseigenschap te gebruiken. Zie [Scenario-gebaseerde plaatsingen](../deploy/scenario-based.md#add-scenarios-using-build-and-deploy-hooks).

>[!NOTE]
>
>Voordat u versie 2002.1.0 van ECE-Tools gaat bijwerken, moet u eerst de [incompatibele wijzigingen terugdraaien](backward-incompatible-changes.md) voor meer informatie over wijzigingen die u mogelijk nodig hebt om Adobe Commerce bij te werken bij de configuratie of processen van projecten in de cloud-infrastructuur.

- ![nieuw pictogram](../../assets/new.svg) **Service-updates**—

   - ![nieuw pictogram](../../assets/new.svg) Toegevoegde ondersteuning voor PHP 7.3.<!--MAGECLOUD-4022-->

   - ![nieuw pictogram](../../assets/new.svg) Extra ondersteuning voor RabbitMQ 3.8.<!--MAGECLOUD-4674-->

   - ![nieuw pictogram](../../assets/new.svg) Toegevoegde bevestiging om geïnstalleerde de dienstversies tegen de EOL datum voor elke dienst te controleren. Nu ontvangen klanten een melding als een serviceversie zich binnen drie maanden na de EOL-datum bevindt en een waarschuwing als de EOL-datum in het verleden ligt.<!--MAGECLOUD-4076-->

   - ![fixepictogram](../../assets/fix.svg) Probleem verholpen met de configuratie van een Elasticsearch om ervoor te zorgen dat de juiste Elasticsearch-instellingen in alle omgevingen zijn geconfigureerd.<!--MAGECLOUD-4474-->

>[!NOTE]
>
>Zie [Serviceversies](../services/services-yaml.md#service-versions) voor een lijst met services die in Adobe Commerce worden gebruikt voor cloudinfrastructuur en de versiecompatibiliteit ervan met de Cloud-sjabloon.

- ![nieuw pictogram](../../assets/new.svg) **Updates van omgevingsvariabelen**—

   - ![nieuw pictogram](../../assets/new.svg) Uitgebreide functionaliteit van de `WARM_UP_PAGES` omgevingsvariabele ter ondersteuning van het vooraf laden van cache voor specifieke productpagina&#39;s. Zie de uitgebreide definitie in het dialoogvenster [variabelen na implementatie](../environment/variables-post-deploy.md#warm_up_pages) onderwerp.<!--MAGECLOUD-4444-->

   - ![nieuw pictogram](../../assets/new.svg) De `ERROR_REPORT_DIR_NESTING_LEVEL` omgevingsvariabele om het beheer van foutrapportgegevens in de `<magento_root>/var/report/` directory. Zie de beschrijving van de variabele in het dialoogvenster [build-variabelen](../environment/variables-build.md#error_report_dir_nesting_level) onderwerp.

   - ![fixepictogram](../../assets/fix.svg) De `SCD_EXCLUDE_THEMES`, `STATIC_CONTENT_THREADS`,`DO_DEPLOY_STATIC_CONTENT`, en `STATIC_CONTENT_SYMLINK` omgevingsvariabelen. Zie [Achterwaartse incompatibele wijzigingen](backward-incompatible-changes.md#environment-configuration-changes).<!--MAGECLOUD-4407, MAGECLOUD-3873-->

   - ![fixepictogram](../../assets/fix.svg) Probleem verholpen in het configuratieproces van de Elastic Suite, zodat de standaardconfiguratie zoals verwacht wordt overschreven wanneer u het `ELASTICSUITE_CONFIGURATION` Variabele implementeren zonder `_merge` -optie.<!--MAGECLOUD-4388-->

- ![nieuw pictogram](../../assets/new.svg) **CLI-opdrachtupdates**—

   - ![nieuw pictogram](../../assets/new.svg) **Nieuwe uitsnede, opdracht**—U kunt de verwerking van snijbewerkingen in uw Adobe Commerce-omgeving nu handmatig beheren met behulp van de `cron:disable` en `cron:enable` opdrachten. Gebruik de opdracht Uitschakelen om alle actieve snijprocessen te stoppen en alle snijtaken uit te schakelen. Gebruik de opdracht Inschakelen om de taken voor uitsnijden weer in te schakelen wanneer u klaar bent. Zie [Snijtaken uitschakelen](../application/crons-property.md#disable-cron-jobs).

   - ![nieuw pictogram](../../assets/new.svg) **Verbeterde foutrapportage**—Toegevoegd betere registreren voor CLI bevelmislukkingen die tijdens ECE-Hulpmiddelen verwerking voorkomen.<!--MAGECLOUD-4849-->

   - ![nieuw pictogram](../../assets/new.svg) **Verouderde bouwstijlbevelen verwijderen**— De volgende constructieopdrachten zijn verwijderd: `m2-ece-build`, `m2-ece-deploy`, `m2-ece-scd-dump`en hernoemd `ece-tools docker` opdrachten aan `ece-docker`. Zie [Achterwaartse incompatibele wijzigingen](backward-incompatible-changes.md)<!--MAGECLOUD-4392-->

- ![nieuw pictogram](../../assets/new.svg) De vervangen `build_options.ini` bestand en toegevoegde validatie om het samenstellen van het bestand te mislukken. Gebruik de [.magento.env.yaml](../environment/configure-env-yaml.md) bestand om constructieopties te configureren.

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen waarbij het constructieproces mislukte als de `config.php` bestand is leeg.<!--MAGECLOUD-4127-->

## 2002,0,23

Releasedatum: 27 februari 2020

- ![fixepictogram](../../assets/fix.svg) Probleem met compatibiliteit verholpen `ece-tools` 2002.0.x-releases die het genereren van statische inhoud op aanvraag in de productiemodus niet hebben kunnen voltooien.

## Oudere releases

Zie de [archief met opmerkingen vrijgeven](cloud-release-archive.md) voor versie 2002.0.22 en eerder.
