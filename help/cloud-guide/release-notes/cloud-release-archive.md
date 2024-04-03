---
title: Archief met releaseopmerkingen voor ece-tools
description: Meer informatie over gearchiveerde verbeteringen voor ece-tools.
hide: true
hidefromtoc: true
recommendations: noDisplay, noCatalog
exl-id: 96663d2f-ef00-4490-ad2e-06e8041b228e
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '7147'
ht-degree: 0%

---

# Archief met releaseopmerkingen voor ece-tools

>[!NOTE]
>
>Deze releaseopmerkingen bevatten informatie en updates voor `ece-tools` v2002.0.22 en hoger. Zie [Opmerkingen bij de release Cloud Tools Suite](cloud-tools-suite.md) voor de nieuwste updates voor `ece-tools` en andere Cloud-pakketten.

## v2002.0.22

De `ece-tools` De release 2002.0.22 wijzigt de structuur van de `ece-tools` pakket om de release van `Adobe Commerce on cloud infrastructure` patches uit de release ECE-Tools. Vanaf deze release worden patches en kritieke oplossingen geleverd met de [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) een nieuwe afhankelijkheid van de `ece-tools` pakket. We hebben deze wijzigingen aangebracht om de complexiteit te verminderen bij het plannen van releaseupdates en het werken met bijdragen van de gemeenschap.

- ![nieuw pictogram](../../assets/new.svg) **Wijzigingen in het pakket ECE-tools**

   - ![nieuw pictogram](../../assets/new.svg) De Adobe Commerce-patches verplaatst van de `ece-tools` verpakken naar een nieuw [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) samenstellingspakket.

   - ![nieuw pictogram](../../assets/new.svg) De `composer.json` bestand voor de `ece-tools` pakket om een afhankelijkheid voor toe te voegen `magento/magento-cloud-patches` pakket v1.0.0.

   - ![fixepictogram](../../assets/fix.svg) Het probleem dat de oorzaak was van de `ece-tools` patchproces dat moet worden afgebroken wanneer u patchsets toepast boven op alleen-beveiligingsreleases, te beginnen met versie 2.3.2-p2 en hoger. Deze kwestie werd geïntroduceerd door de nieuwe versieregeling die voor [beveiligingspatches](https://devdocs.magento.com/guides/v2.3/release-notes/bk-release-notes.html#security-only-patches).<!--MAGECLOUD-4661-->

- ![fixepictogram](../../assets/fix.svg) **Patches en kritieke oplossingen**-Werk uw Cloud-omgevingen bij met `ece-tools` versie 2002.0.22 om de volgende patches en kritieke oplossingen toe te passen. Deze patches worden opgenomen in de `magento/magento-cloud-patches` pakket v1.0.0.

   - ![fixepictogram](../../assets/fix.svg) **Beveiligingspatches voor 2.3.1.x en 2.3.2.x van Page Builder**- Oplossingen een kwestie in de voorproef van de Bouwer van de Pagina die unauthenticated gebruikers toestaat om tot sommige malplaatjesmethodes toegang te hebben die kunnen worden gebruikt om willekeurige codeuitvoering over het netwerk (RCE) te teweegbrengen resulterend in globale informatielekken. Dit probleem kan optreden wanneer niet-ondersteunde versies van Page Builder worden gebruikt met Adobe Commerce versie 2.3.1 en 2.3.2.<!--MAGECLOUD-4649-->

   - ![fixepictogram](../../assets/fix.svg) **MSI-patches**-Hiermee worden problemen verholpen die indexatiefouten en prestatieproblemen hebben veroorzaakt bij het gebruik van standaardinstellingen voor inventarisatie voor het beheer van voorraden.<!--MAGECLOUD-4428-->

   - ![fixepictogram](../../assets/fix.svg) **Achterwaartse Verenigbaarheid van nieuwe Interfaces van de Post**-Oplossing voor een probleem met achterwaartse incompatibiliteit dat wordt veroorzaakt door de `Magento\Framework\Mail\EmailMessageInterface` PHP interface created in Adobe Commerce v2.3.3. In het bereik van deze patch worden de nieuwe `EmailMessageInterface` erft van de oude `MessageInterface`en Adobe Commerce-kernmodules zijn weer afhankelijk van `MessageInterface`.<!--MAGECLOUD-4422-->

   - ![fixepictogram](../../assets/fix.svg) **Paginering van catalogi werkt niet op Elasticsearch 6.x**-Hiermee verhelpt u een kritiek probleem met de paginering van zoekresultaten dat van invloed is op klanten die Elasticsearch 6.x als zoekprogramma voor catalogi gebruiken.<!--MAGECLOUD-4448-->

## v2002.0.21

- ![nieuw pictogram](../../assets/new.svg) **Dockingupdates**—

   - ![nieuw pictogram](../../assets/new.svg) **Nieuwe Docker-afbeeldingen**—Ondersteund door versies 2.3.3 en hoger<!-- MAGECLOUD-3345 -->

      - PHP versie 7.3.<!-- MAGECLOUD-4017 -->

      - Varnish Cache 6.2.0<!-- MAGECLOUD-4017 -->

   - ![nieuw pictogram](../../assets/new.svg) Toegevoegde steun om de configuratie van de douaneschaak toe te passen in `.magento.app.yaml` in de Docker-omgeving. Eerder, steunde de milieu van de Dokker slechts de standaardhakenconfiguratie.<!-- MAGECLOUD-3505-->

   - ![nieuw pictogram](../../assets/new.svg) Docker ENV-bestanden worden niet meer gegenereerd tijdens de Docker-build en `docker:config:convert` is vervangen. De bijbehorende gegevens worden nu opgeslagen in het dialoogvenster `docker-compose.yml` bestand.<!-- MAGECLOUD-3816-->

   - ![nieuw pictogram](../../assets/new.svg) **Bijgewerkte PHP-afbeelding**-Added Node.js to the PHP Docker image to support node, npm, and grunt-cli capabilities.<!-- MAGECLOUD-3953 -->

- ![nieuw pictogram](../../assets/new.svg) **Updates van omgevingsvariabelen**-

   - ![nieuw pictogram](../../assets/new.svg) De **LOCK_PROVIDER** Hiermee implementeert u variabele om de vergrendelingsprovider te configureren die het starten van dubbele snijtaken en snijgroepen voorkomt. Zie de beschrijving van de variabele in het dialoogvenster [variabelen implementeren](../environment/variables-deploy.md#lock_provider) onderwerp.<!-- MAGECLOUD-4052 -->

   - ![nieuw pictogram](../../assets/new.svg) De **CONSUMERS_WAIT_FOR_MAX_MESSAGES** omgevingsvariabele om te configureren hoe consumenten berichten uit de wachtrij verwerken wanneer ze de functie `CRON_CONSUMERS_RUNNER` omgevingsvariabele voor het beheer van cron-taken. Zie de beschrijving van de variabele in het dialoogvenster [variabelen implementeren](../environment/variables-deploy.md#consumers_wait_for_max_messages) onderwerp.<!-- MAGECLOUD-4071 -->

   - ![fixepictogram](../../assets/fix.svg) Probleem verholpen waarbij databasestortingsfouten kunnen optreden als de `consumers_runner` met de snijtaak worden meerdere exemplaren van dezelfde consument op verschillende knooppunten gestart. Als u nu de optie [**CRON_CONSUMERS_RUNNER**](../environment/variables-deploy.md#cron_consumers_runner) in uw omgeving variabele implementeren, `consumers_runner` taak gebruikt de `single-thread` optie om één instantie van elke consument op slechts één knoop te beginnen.<!-- MAGECLOUD-3913 -->

   - ![fixepictogram](../../assets/fix.svg) Probleem verholpen dat invloed had op [**WARM_UP_PAGES**](../environment/variables-post-deploy.md#warm_up_pages) functionaliteit die een standaard opslag URL gebruikt. Als de `config:show:default-url` opdracht kan geen basis-URL ophalen, wordt de URL van de variabele MAGENTO_CLOUD_ROUTES gebruikt.<!-- MAGECLOUD-3866 -->

- ![nieuw pictogram](../../assets/new.svg) Bijgewerkt de registrereninformatie die door wordt teruggekeerd `module:refresh` gebruiken. Nu, kunt u een gedetailleerde lijst van toegelaten modules in zien `cloud.log` bestand.<!-- MAGECLOUD-2514 -->

- ![nieuw pictogram](../../assets/new.svg) Verbeterde validatie- en waarschuwingsmeldingen voor versiecompatibiliteit tussen Adobe Commerce-versies en geïnstalleerde services, zoals Elasticsearch, [!DNL RabbitMQ], Redis en DB.<!-- MAGECLOUD-3535 -->

- ![nieuw pictogram](../../assets/new.svg) Toegevoegde ondersteuning voor RabitMQ versie 3.8.<!-- MAGECLOUD-4674-->

- ![nieuw pictogram](../../assets/new.svg) Bijgewerkte interactieve validaties voor de dienstverenigbaarheid om op gesteunde versies voor de nieuwe versies van Adobe Commerce 2.3.3 en 2.2.10 te wijzen. Zie [Systeemvereisten](https://devdocs.magento.com/guides/v2.4/install-gde/system-requirements.html) in de _Installatiehandleiding_ voor aanbevolen versies.<!-- MAGECLOUD-4018 -->

- ![fixepictogram](../../assets/fix.svg) Verbeterd het logboekbericht dat wordt geretourneerd wanneer het proces voor het beheer van de snijtaak in de implementatiefase probeert een snijtaak te stoppen die al is voltooid om te verduidelijken dat dit probleem geen fout is. Het logniveau is gewijzigd van `INFO` tot `DEBUG`.<!-- MAGECLOUD-3653-->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen bij het uitvoeren van het `setup:upgrade` bevel dat niet het plaatsingsproces onderbreek toen een mislukking tijdens voorkwam `app:config:import` taak.<!-- MAGECLOUD-3806 -->

- ![nieuw pictogram](../../assets/new.svg) Het standaardlogniveau voor de bestandshandler is gewijzigd in `debug` om de hoeveelheid details in het logboek te verminderen dat in [!DNL Cloud Console], terwijl het verstrekken van gedetailleerde informatie voor het zuiveren.<!-- MAGECLOUD-3871 -->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen die een fout veroorzaakte met de implementatie van statische inhoud tijdens het maken van een build. Na een installatie en `ece-tools` config-stortplaats, kwam een fout voor als er geen scène voor de admin gebruiker in werd gespecificeerd `config.php` bestand. Er is nu een standaardlandinstelling voor de beheerder in het dialoogvenster `config.php` bestand.<!-- MAGECLOUD-3957 -->

- ![fixepictogram](../../assets/fix.svg) Vast een `Undefined index error` dat zich voordoet wanneer een `magento-cloud` CLI het bevel ontbreekt in een milieu dat niet met een veilige URL (https) wordt gevormd. Het pakket ECE-Tools gebruikt nu de basis-URL (http) als de beveiligde URL niet beschikbaar is.<!-- MAGECLOUD-4009 -->

## v2002.0.20

- ![nieuw pictogram](../../assets/new.svg) **Docker-updates**—

   - ![nieuw pictogram](../../assets/new.svg) U kunt nu functionele tests uitvoeren met de `ece-tools` in de Docker-omgeving. Zie [toepassing testen](https://devdocs.magento.com/cloud/docker/docker-test-magecloud-pkg-code.html).<!-- MAGECLOUD-3129/3684 -->

   - ![nieuw pictogram](../../assets/new.svg) Extra ondersteuning voor het configureren van PHP-modules met behulp van de `.magento.app.yaml` bestand. Alle [PHP-extensies opgegeven in de `.magento.app.yaml` file](https://devdocs.magento.com/cloud/project/magento-app-php-application.html#php-extensions) zijn beschikbaar in de Docker PHP containers.<!-- MAGECLOUD-3357 -->

   - ![nieuw pictogram](../../assets/new.svg) Er zijn nieuwe bevelen beschikbaar om de het bevellijnervaring van de Docker te verbeteren. Zie de [`bin/magento-docker` sectie van de verwijzing van de Dokker](https://devdocs.magento.com/cloud/docker/docker-quick-reference.html#magento-cloud-docker-cli).<!-- MAGECLOUD-3569 -->

   - ![nieuw pictogram](../../assets/new.svg) De mogelijkheid om Mutagen.io te gebruiken voor het synchroniseren van bestanden tijdens de ontwikkeling tussen de lokale host en Docker is toegevoegd.<!-- MAGECLOUD-3559 -->

   - ![fixepictogram](../../assets/fix.svg) Correctie van het standaardpad bij gebruik van de Docker-omgeving. Nu, wanneer u SSH aan login aan de container van de Dokker gebruikt, bent u bij de projectwortel in `/app` directory, zoals verwacht.<!-- MAGECLOUD-3582 -->

   - ![fixepictogram](../../assets/fix.svg) De natriumbibliotheek is bijgewerkt van versie 1.0.11 naar versie 1.0.18 en de extensie Natrium PHP is bijgewerkt.<!-- MAGECLOUD-3832 -->

     >[!WARNING]
     >
     >Adobe Commerce op cloudinfrastructuur moet [Een Adobe Commerce-ondersteuningsticket verzenden](https://support.magento.com/hc/en-us/articles/360000913794#submit-ticket) het libnatrium-pakket bijwerken op Pro Production and Staging-omgevingen voordat het wordt bijgewerkt naar Adobe Commerce 2.3.2. U kunt momenteel geen upgrade uitvoeren van Starter-omgevingen naar Adobe Commerce 2.3.2.

   - ![fixepictogram](../../assets/fix.svg) De `analysis-icu` en de `analysis-phonetic` Elasticsearch sluit aan op alle beelden van de Dokker.<!-- MAGECLOUD-3446 -->

   - ![fixepictogram](../../assets/fix.svg) Verbeterde validaties: bij het gebruik van opties voor de `docker:build` moet u een waarde opgeven wanneer u een optie gebruikt. Voeg ook validatie toe voor de Node-versie bij het gebruik van de `docker:build run` gebruiken.<!-- MAGECLOUD-3486 & MAGECLOUD-3678 -->

- ![nieuw pictogram](../../assets/new.svg) **Updates van omgevingsvariabelen**—

   - ![nieuw pictogram](../../assets/new.svg) Extra ondersteuning voor voorvoegsels van databasetabellen met de opdracht [Omgevingsvariabele DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration).<!-- MAGECLOUD-2901 -->

   - ![nieuw pictogram](../../assets/new.svg) De **FORCE_UPDATE_URLS** Variabele implementeren om basis-URL&#39;s bij te werken bij de implementatie naar Pro- en Starter-productie- en staging-omgevingen. Zie de definitie in de [variabelen implementeren](../environment/variables-deploy.md#force_update_urls) inhoud.<!-- MAGECLOUD-3602 -->

   - ![nieuw pictogram](../../assets/new.svg) De **TTFB_TESTED_PAGES** post-opstellen variabele om te vormen _Tijd naar eerste byte_ pagina-tests om de prestaties van de toepassing te controleren op sites die zijn geïmplementeerd in de cloud. Zie de beschrijving van de variabele in [variabelen na implementatie](../environment/variables-post-deploy.md).<!-- MAGECLOUD-3643 -->

   - ![fixepictogram](../../assets/fix.svg) Probleem verholpen met multi-threaded SCD, dat willekeurige mislukkingen in statische inhoudsplaatsing veroorzaakte. De oplossing die u nodig hebt, is **SCD_THREADS** variabele tot `1`. U kunt nu het aantal verhogen wanneer dat nodig is. Zie de definities in de [variabelen implementeren](../environment/variables-deploy.md#scd_threads) en de [build-variabelen](../environment/variables-build.md#scd_threads).<!-- MAGECLOUD-3611 -->

   - ![fixepictogram](../../assets/fix.svg) U kunt de **WARM_UP_PAGES** omgevingsvariabele om één pagina, meerdere domeinen en meerdere pagina&#39;s in cache te plaatsen. Zie de uitgebreide definitie in het dialoogvenster [variabelen na implementatie](../environment/variables-post-deploy.md#warm_up_pages) inhoud.<!-- MAGECLOUD-3258 -->

- ![fixepictogram](../../assets/fix.svg) De `pub/static/.htaccess` aan de uitsluitingslijst. [Fix ingediend door Björn Kraus of PHOENIX MEDIA GmbH](https://github.com/magento/ece-tools/pull/455).<!-- MAGECLOUD-3545/Github#455 -->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen waarbij alle validatieberichten werden weergegeven als `Critical` als ten minste één validator van het kritieke niveau een fout heeft geretourneerd.<!-- MAGECLOUD-3178 -->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen die een implementatiefout veroorzaakte als de basis-URL niet bestond in de database.<!-- MAGECLOUD-3075 -->

- ![nieuw pictogram](../../assets/new.svg) Een nieuwe **`env:config:show`command** aan de `ece-tools` pakket dat de omgevingsdiensten, routes, of variabelen toont. Zie [Services, routes en variabelen](https://devdocs.magento.com/cloud/reference/ece-tools-reference.html#services-routes-and-variables). [Functie ingediend door Vladimir Kerkhoff](https://github.com/magento/ece-tools/pull/486).<!-- MAGECLOUD-3451 -->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen waarbij een kritieke fout optrad tijdens een poging om Adobe Commerce 2.2.6 of eerder te installeren met `ece-tools` ontwikkelen na shell refactoring.<!-- MAGECLOUD-3665 -->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen waarbij Adobe Commerce 2.1.x- en 2.2.x-installaties mislukten met een waarschuwing over het gebruik van een verouderde versie van Carbon.<!-- MAGECLOUD-3704 -->

- ![fixepictogram](../../assets/fix.svg) Verminderde `cloud.log` logniveau voor shell-uitvoer van `info` tot `debug`.<!-- MAGECLOUD-3277 -->

- ![fixepictogram](../../assets/fix.svg) De `--remove-definers (-d)` aan de `ece-tools db-dump` om definities uit het dumpbestand te verwijderen.<!-- MAGECLOUD-3510 -->

## v2002.0.19

- ![fixepictogram](../../assets/fix.svg) Het probleem waarbij de `env.php` bestand tijdens een implementatie, met als gevolg dat aangepaste configuraties verloren gaan. Deze update zorgt ervoor dat Adobe Commerce op de cloudinfrastructuur de `env.php` bestand met elke implementatie, terwijl aangepaste configuraties behouden blijven.<!-- MAGECLOUD-3668 -->

## v2002.0.18

- ![nieuw pictogram](../../assets/new.svg) **Docker-updates**—

   - ![nieuw pictogram](../../assets/new.svg) Nu, steunt het milieu van de Dokker de kanonconfiguratie die in [crons, eigenschap van het bestand .magento.app.yaml](https://devdocs.magento.com/cloud/project/magento-app-properties.html#crons).<!-- MAGECLOUD-3150 -->

   - ![nieuw pictogram](../../assets/new.svg) **Nieuwe Docker-container**—Toegevoegd a [TLS-proxy-container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container) om de Varnish SSL beëindiging over HTTPS te vergemakkelijken.<!-- MAGECLOUD-2890 -->

   - ![nieuw pictogram](../../assets/new.svg) **Nieuwe Docker-afbeelding**—Er is een afbeelding Node.js toegevoegd ter ondersteuning van Gulp en andere mogelijkheden, zoals JS Unit Testing.<!-- MAGECLOUD-3345 -->

   - ![nieuw pictogram](../../assets/new.svg) **Samenstellingsmodi voor dockers**—Nu kunt u ervoor kiezen de Docker-omgeving te starten in [Productiemodus of Developer-modus](https://devdocs.magento.com/cloud/docker/docker-launch.html#set-the-launch-mode). De modus Ontwikkelaar ondersteunt actieve ontwikkeling met volledige, schrijfbare bestandssysteemmachtigingen.<!-- MAGECLOUD-3152/3511 -->

   - ![fixepictogram](../../assets/fix.svg) Probleem verholpen waardoor de implementatie van Docker mislukte met een `Name or service not known` fout als het geheime voorgeheugen voor de dienst wordt gevormd die niet beschikbaar is. U kunt nu een service verwijderen uit de [`.magento/services.yaml` file](https://devdocs.magento.com/cloud/project/services.html). De de configuratiegenerator van de Docker werkt de dienst in de `docker/config.php.dist` bestand automatisch.<!-- MAGECLOUD-3369 -->

   - ![nieuw pictogram](../../assets/new.svg) Toegevoegde interactieve validaties voor service-compatibiliteit. Als een aangevraagde service niet compatibel is met de Adobe Commerce-versie of andere services, wordt de _interactieve modus_ de gebruiker een bericht en een keuze geeft om door te gaan. Zie de [Serviceversies](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-containers) beschikbaar voor Docker. Gebruik de `-n` om de interactiviteit voor CICD-doeleinden over te slaan.<!-- MAGECLOUD-3251 -->

   - ![fixepictogram](../../assets/fix.svg) Probleem verholpen met Docker-compositie `db-dump` die bestaande dumps wist.<!-- MAGECLOUD-3366 -->

   - ![fixepictogram](../../assets/fix.svg) Probleem verholpen waarbij Redis werd toegewezen `session`, `default`, en `page_cache` cacheopslag naar dezelfde database-id.<!-- MAGECLOUD-3172 -->

- ![nieuw pictogram](../../assets/new.svg) **Updates van omgevingsvariabelen**—

   - ![nieuw pictogram](../../assets/new.svg) De nieuwe **ELASTICSUITE\_CONFIGURATION** de omgevingsvariabele behoudt uw aangepaste de dienstmontages tussen plaatsingen. Zie de definitie in de [variabelen implementeren](../environment/variables-deploy.md#elasticsuite_configuration) inhoud.<!-- MAGECLOUD-3205 -->

   - ![nieuw pictogram](../../assets/new.svg) De **SCD_MAX_EXECUTION_TIMEOUT** omgevingsvariabele zodat u meer tijd nodig hebt om de statische implementatie van inhoud uit te voeren via de `.magento.env.yaml` bestand. Zie de definitie in de [variabelen implementeren](../environment/variables-deploy.md#scd_max_execution_time)de [build-variabelen](../environment/variables-build.md#scd_max_execution_time)en de [algemene variabelen](../environment/variables-global.md#scd_max_execution_time).<!-- MAGECLOUD-2822 -->

      - ![nieuw pictogram](../../assets/new.svg) De **MAGENTO_CLOUD_LOCKS_DIR** omgevingsvariabele om het pad naar het koppelpunt voor de vergrendelingsprovider op de cloudinfrastructuur te configureren. De vergrendelingsprovider voorkomt het starten van dubbele snijtaken en afdekgroepen. Deze variabele wordt ondersteund op Adobe Commerce versie 2.2.5 en hoger en automatisch geconfigureerd. Zie de definitie in [Cloud-variabelen](../environment/variables-cloud.md).<!-- MAGECLOUD-3135 -->

      - ![fixepictogram](../../assets/fix.svg) De **SCD_THREADS** omgevingsvariabele standaardwaarden om automatisch de optimale waarde te bepalen op basis van de gedetecteerde CPU-thread. Zie de bijgewerkte definities in het dialoogvenster [variabelen implementeren](../environment/variables-deploy.md#scd_threads) en de [build-variabelen](../environment/variables-build.md#scd_threads).<!-- MAGECLOUD-3382 -->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen met een patch voor het DB-isolatiemechanisme dat een fout veroorzaakte bij de upgrade naar Adobe Commerce op cloudinframeconversie 2002.0.16.<!-- MAGECLOUD-3383 -->

- ![fixepictogram](../../assets/fix.svg) Een patch toegevoegd ter vervanging van _Google-afbeeldingen_ with _Afbeeldingsgrafieken_. Zie het DevBlog-artikel [Veroudering en update van Google Image Charts voor M1](https://community.magento.com/t5/Magento-DevBlog/Google-Image-Charts-deprecation-and-update-for-M1/ba-p/125006).<!-- MAGECLOUD-3456 -->

- ![fixepictogram](../../assets/fix.svg) Toegevoegde validatie voor de [variabele SEARCH_CONFIGURATION](../environment/variables-deploy.md#search_configuration). Implementatie mislukt als de optie &#39;engine&#39; niet is ingesteld en `_merge` is niet vereist.<!-- MAGECLOUD-3470 -->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen waarbij gevoelige gegevens werden vrijgegeven nadat een uitzondering is opgetreden. De gevoelige informatie wordt nu op de juiste wijze gemaskeerd.<!-- MAGECLOUD-3525 -->

- ![fixepictogram](../../assets/fix.svg) Verbeterde fouttolerante instellingen van het Magento Open Source-pakket. Als Adobe Commerce geen gegevens van Redis kan lezen `slave` De Redis leest `master` -instantie. Zie [REDIS_USE_SLAVE_CONNECTION](../environment/variables-deploy.md#redis_use_slave_connection).<!-- MAGECLOUD-2899 -->

## v2002.0.17

>[!NOTE]
>
>De `ece-tools` versie 2002.0.17 bevat een belangrijke beveiligingspatch. Zie [Technische bronnen: Magento Open Source patches](https://magento.com/tech-resources/download#download2288).

- ![nieuw pictogram](../../assets/new.svg) **Service-updates**—Ondersteund door de volgende Adobe Commerce-versies: 2.2.8 en hoger 2.2.x, 2.3.1 en hoger 2.3.x

   - Extra ondersteuning voor Elasticsearch versie 6.x.<!-- MAGECLOUD-3196 -->

   - Toegevoegde ondersteuning voor Redis versie 5.0.

- ![nieuw pictogram](../../assets/new.svg) **Nieuwe Docker-afbeeldingen**—Voegt de volgende diensten aan de Docker toe bouwt:

   - Elasticsearch 6.5<!-- MAGECLOUD-3196 -->

   - Redis 5.0<!-- MAGECLOUD-3223 -->

- ![nieuw pictogram](../../assets/new.svg) **Nieuwe omgevingsvariabele**—Eerder was er een hard-gecodeerde onderbreking voor compressie SCD. Nu kunt u de compressieonderbreking vormen SCD gebruikend **SCD_COMPRESSION_TIMEOUT** omgevingsvariabele. Zie de definities in de [build-variabelen](../environment/variables-build.md#scd_compression_timeout) en de [variabelen implementeren](../environment/variables-deploy.md#scd_compression_timeout) inhoud.<!-- MAGECLOUD-2870 -->

- ![fixepictogram](../../assets/fix.svg) De `--use-rewrites` voor de installatieopdracht, zodat de webserver herschrijft voor gegenereerde koppelingen in de winkel- en beheerdersrechten gebruikt om de beveiliging en de gebruikerservaring te verbeteren.<!-- MAGECLOUD-3246 -->

- ![fixepictogram](../../assets/fix.svg) Tijdstempels toegevoegd aan de `var/log/install_upgrade.log` bestand, zodat de datums voor installatie- en upgradegebeurtenissen worden weergegeven.<!-- MAGECLOUD-2895 -->

## v2002.0.16

- ![nieuw pictogram](../../assets/new.svg) **Dockingupdates**—

   - Nu, is de standaarddienstconfiguratie die in het milieu van de Dokker wordt geproduceerd het zelfde als de standaardconfiguratie in het malplaatje van de Wolk.<!-- MAGECLOUD-3025 -->

   - U kunt post van uw milieu van de Dokker verzenden gebruikend `sendmail` service.<!-- MAGECLOUD-2907 -->

   - De mogelijkheid toegevoegd om [Xdebug configureren](https://devdocs.magento.com/cloud/docker/docker-development-debug.html) om fouten op te sporen in de Cloud Docker-omgeving.<!-- MAGECLOUD-2891 -->

   - Probleem verholpen met webservicerechten tijdens het genereren van het dialoogvenster `docker-compose.yml` bestand.<!-- MAGECLOUD-2883 -->

- ![nieuw pictogram](../../assets/new.svg) **Verbetering van upgrade**—Toegevoegde bevestiging om te bevestigen dat `autoload` eigenschap in de `composer.json` bevat vereiste configuratiewijzigingen voordat u gaat upgraden naar Adobe Commerce v2.3. Zie [Upgradeversie](https://devdocs.magento.com/cloud/project/project-upgrade.html).<!-- MAGECLOUD-2392 -->

- ![nieuw pictogram](../../assets/new.svg) Het compressieproces in het opstellen van statische inhoud omvat nu alle activa-native geproduceerd of aangepast-en komt tijdens de bouwstijlfase aan het begin van voor [`build:transfer` sectie](https://devdocs.magento.com/cloud/project/magento-app-properties.html#hooks). Eerder was het compressieproces vóór het toepassen van aangepaste minificatie en bundeling van statische elementen. [Fix, ingediend door Rafael Garcia Lepper door Tryzens Limited](https://github.com/magento/ece-tools/pull/413).<!-- MAGECLOUD-3104 -->

- ![fixepictogram](../../assets/fix.svg) Oplossing voor een fout met betrekking tot de databaseverbinding die optrad tijdens de implementatie direct na het configureren van een extra database- en servicerelatie. Ook, behandelt deze moeilijke situatie een kwestie die tijdens het configuratieproces van Handel die voor Starter meldt voorkwam. Voor Starter, is deze verbetering &quot;moet&quot;voor het gebruiken van de Rapportering van de Handel hebben.<!-- MAGECLOUD-3035 -->

- ![fixepictogram](../../assets/fix.svg) Oplossing voor een validatieprobleem met de databaseconfiguratie die ertoe heeft geleid dat het implementatieproces is mislukt.<!-- MAGECLOUD-3003 -->

- ![fixepictogram](../../assets/fix.svg) De restrictie is bijgewerkt met de juiste versie van het dialoogvenster `symfony/yaml` pakket gebruiken met [PHP-constanten](https://devdocs.magento.com/cloud/project/magento-env-yaml.html#php-constants). Constante parsering werkt niet wanneer u een `symfony/yaml` pakketversie ouder dan 3.2. [Fix ingediend door Vladimir Kerkhoff](https://github.com/magento/ece-tools/pull/404).<!-- MAGECLOUD-2956 -->

- ![nieuw pictogram](../../assets/new.svg) **Omgevingsconfiguratiecontrole**—Toegevoegde validatie om de PHP-versie te controleren en gebruikers te waarschuwen als ze de meest recente aanbevolen versie niet gebruiken.<!--MAGECLOUD-2903-->

- ![fixepictogram](../../assets/fix.svg) Probleem opgelost met het verwerken van onjuist gevormde JSON-variabelen. Als een JSON-variabele nu een syntaxisfout veroorzaakt, verschijnt er een waarschuwing in het dialoogvenster `cloud.log` Het bestand en de implementatie worden voortgezet met de standaardvariabele.<!-- MAGECLOUD-2851 -->

- ![fixepictogram](../../assets/fix.svg) Oplossing voor een verbindingsfout die optrad tijdens de implementatie direct nadat de service Redis was uitgeschakeld.<!-- MAGECLOUD-2747 -->

- ![nieuw pictogram](../../assets/new.svg) **Wijzigingen in logboekbestand**—De [logniveau](../environment/log-handlers.md#log-levels) van `Info` tot `Notice` voor de volgende bouwstijl en stel procesgebeurtenissen op:<!--MAGECLOUD-2925-->

   - Begin en eind van het proces om geïnstalleerde modules in overeenstemming te brengen `composer.json` met gedeelde configuratie-instellingen in het dialoogvenster `app/etc/config.php` file

   - Begin en eind van het configuratiebevestigingsproces

   - Begin en einde van het dialoogvenster `setup:di:compile` proces voor het genereren van klassen

- ![nieuw pictogram](../../assets/new.svg) **Nieuwe omgevingsvariabelen**—

   - **[Distributievariabele voor RESOURCE_CONFIGURATION](../environment/variables-deploy.md#resource_configuration)**—Gebruik deze variabele om een middelnaam aan een gegevensbestandverbinding in kaart te brengen.<!-- MAGECLOUD-3026 & MAGECLOUD-2963-->

   - **[Globale variabele X_FRAME_CONFIGURATION](../environment/variables-global.md#x_frame_configuration)**—Gebruik deze variabele om het `X-Frame-Options` koptekstconfiguratie voor het weergeven van een Adobe Commerce-pagina in een `<frame>`, `<iframe>`, of `<object>`.<!-- MAGECLOUD-3048 -->

- ![fixepictogram](../../assets/fix.svg) **Updates van omgevingsvariabelen**—Gewijzigd de volgende omgevingsvariabelen:

   - **[WARM_UP_PAGES](../environment/variables-post-deploy.md)**—De mogelijkheid toegevoegd om de cache voor opgegeven pagina&#39;s vooraf te laden op alle domeinen die zijn gedefinieerd voor een Adobe Commerce-winkel. Eerder, als uw plaats met veelvoudige domeinen werd gevormd, kon het post-opstellen proces niet het geheime voorgeheugen voor de gespecificeerde pagina&#39;s op niet standaarddomeinen vooraf laden en de volgende fout in het post-opstellen logboek terugkeren: `ERROR: Warming up failed: <uri>`<!-- MAGECLOUD-2466 -->

   - **SCD_COMPRESSION_LEVEL**—De documentatie en de steekproef zijn bijgewerkt `.magento.env.yaml` bestand met de juiste standaardwaarden voor SCD-compressieniveau. Zie de definities in de [build-variabelen](../environment/variables-build.md#scd_compression_level) en de [variabelen implementeren](../environment/variables-deploy.md#scd_compression_level) inhoud.<!-- MAGECLOUD-2823 -->

   - **SCD_EXCLUDE_THEMES**—Deze omgevingsvariabele is vervangen. Gebruik de [SCD_MATRIX](../environment/variables-build.md#scd_matrix) om themaconfiguratie te beheren.<!--MAGECLOUD-2882-->

   - **SCD\_MATRIX**—Oplossing voor het validatieproces om een probleem te voorkomen dat optrad wanneer SCD_MATRIX een themawaarde negeerde die verschillende tekengevallen bevatte. Zie de definities in de [build-variabelen](../environment/variables-build.md#scd_matrix) en de [variabelen implementeren](../environment/variables-deploy.md#scd_matrix) inhoud.<!-- MAGECLOUD-2904 -->

   - **ADMIN-variabelen**—<!-- MAGECLOUD-2573/MAGECLOUD-2848 -->

      - Verbeterde beveiliging bij het beheren van referenties voor de Admin-gebruiker met omgevingsvariabelen. U kunt de ADMIN_EMAIL, ADMIN_USERNAME, en ADMIN_PASSWORD milieuvariabelen niet meer gebruiken om admin geloofsbrieven tijdens verbeteringen met voeten te treden. Als u geen toegang hebt tot het deelvenster Beheer, gebruikt u de opdracht _Wachtwoord vergeten_ van de `admin:user:create` CLI bevel om een nieuwe admin gebruiker te creëren. Zie [Open het deelvenster Beheer](https://devdocs.magento.com/cloud/onboarding/onboarding-tasks.html#admin).

      - ADMIN_EMAIL is niet meer vereist wanneer u patches upgradet of toepast.

## v2002.0.15

- ![nieuw pictogram](../../assets/new.svg) **Dockingupdates**—

   - Nu gebruikt de generator van de Dokker de diensten die in `.magento.app.yaml` en `.magento/services.yaml` configuratiebestanden wanneer [de Docker-omgeving bouwen](https://devdocs.magento.com/cloud/docker/docker-config.html). U kunt een verschillende de dienstversie kiezen gebruikend bouwstijlparameters.<!-- MAGECLOUD-2888 -->

   - Afbeelding met PHP 7.2 toegevoegd—Ondersteuning voor PHP 7.2 toegevoegd in Cloud Docker; bijgewerkt met [Docker-configuratie starten](https://devdocs.magento.com/cloud/docker/docker-config.html) om de `docker:build --php` om de versie van PHP te specificeren compatibel met uw versie van Adobe Commerce.<!-- MAGECLOUD-2799 -->

   - Toegevoegde [Container voor uitsnijden](https://devdocs.magento.com/cloud/docker/docker-containers-cli.html#cron-container) gebaseerd op de PHP-CLI afbeelding.<!-- MAGECLOUD-2565 -->

   - De volgende services zijn toegevoegd aan de Docker-build:

      - [!DNL RabbitMQ] 3.5 en 3.7<!-- MAGECLOUD-2567 & 2889-->

      - Elasticsearch 1.7, 2.4 en 5.2<!-- MAGECLOUD-2569 & 2887 -->

      - Redis 3.2 en 4.0<!-- MAGECLOUD-2886 -->

- ![nieuw pictogram](../../assets/new.svg) **Configureren met PHP-constanten**—Extra ondersteuning voor [PHP-constanten](https://devdocs.magento.com/cloud/project/magento-env-yaml.html#php-constants) in de `.magento.env.yaml` configuratiebestand.<!-- MAGECLOUD- 2575 -->

- ![nieuw pictogram](../../assets/new.svg) **Nieuwe omgevingsvariabele**—Door gebrek, slechts heeft het milieu van de Productie toegelaten Googles Analytics. U kunt Googles Analytics op de milieu&#39;s van het Staging en van de Integratie toelaten gebruikend  [ENABLE_GOOGLE_ANALYTICS omgevingsvariabele](../environment/variables-deploy.md#enable_google_analytics).<!--MAGECLOUD-2879-->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen waarbij aangepaste uitsnijdconfiguraties uit de `env.php` bestand na een herschikking. Nu blijven aangepaste uitsnijdconfiguraties veilig in de `env.php` bestand.<!-- MAGECLOUD-2923 -->

- ![fixepictogram](../../assets/fix.svg) Vaste inconsistenties in de berichten en [logniveaus](../environment/log-handlers.md#log-levels) voor bouw, opstellen, en post-opstellen fasen. Grotere begin- en eindniveaus van logberichten vanaf **info** tot **bericht** voor alle fasen en subfasen. Toegevoegde begin- en eindlogberichten, indien van toepassing.<!-- MAGECLOUD-2919 -->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen met betrekking tot snijprocessen die het begin van de fase na implementatie, indien geconfigureerd, verhinderden. Nu, als u de post-opstellen toegelaten haak hebt, worden de kroonprocessen opnieuw toegelaten aan het begin van de post-opstellen fase.<!-- MAGECLOUD-2862 -->

- ![fixepictogram](../../assets/fix.svg) Oplossing voor een probleem dat een geslaagde installatie van Adobe Commerce verhinderde bij het opgeven van een aangepaste databaseconfiguratie. Eerder gebruikte het installatieproces de gegevensbestandconfiguratie van [Variabele Magento_CLOUD_RELATIONSHIP](../environment/variables-cloud.md) zelfs als u aangepaste verbindingsgegevens hebt opgegeven in het dialoogvenster [Omgevingsvariabele DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration).<!--MAGECLOUD-2736-->

- ![fixepictogram](../../assets/fix.svg) De `config:dump` zodat elke website in de `system` van de `config.php` bestand.<!--MAGECLOUD-2740-->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen dat tot _opwarmen_ fouten tijdens de post-opstellen fase door de bron basisURL verwijzing te verbeteren.<!--MAGECLOUD-2797-->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen waarbij bestanden onjuist werden gegenereerd tijdens het dialoogvenster `setup:di:compile` -procedure, die van invloed was op de Amazon Pay-module.<!--MAGECLOUD-2850-->

## v2002.0.14

- ![nieuw pictogram](../../assets/new.svg) **Ideale status verifiëren**—De `ideal-state` De tovenaar verifieert nu de huidige configuratie tijdens elke plaatsing en verstrekt duidelijke instructies voor het bijwerken van de configuratie om een snellere, nul-onderbreking plaatsing te bereiken.<!--MAGECLOUD-2372-->

- ![fixepictogram](../../assets/fix.svg) **PCI-compatibiliteit**—Bijgewerkt de overseinenprotocollen voor Adobe Commerce op wolkeninfrastructuur om versie 1.2 van de Veiligheid van de Laag van het Vervoer (TLS) te vereisen wanneer het verbinden met de diensten van het derdenoverseinen. Als u een berichtservice gebruikt die geen ondersteuning biedt voor TLS versie 1.2, moet u een upgrade uitvoeren op uw service. Anders wordt het volgende foutbericht weergegeven wanneer uw Adobe Commerce-toepassing verbinding probeert te maken met de berichtserver om een e-mail te verzenden: `Unable to connect via TLS`.<!--MAGECLOUD-2521-->

- ![nieuw pictogram](../../assets/new.svg) **Implementatieverbetering**—Toegevoegde bevestiging om klanten te waarschuwen als het het Staging of milieu van de Productie heeft `dev`, `debug`, of `debug_logging` opties die worden ingeschakeld om prestatieproblemen te voorkomen die worden veroorzaakt door excessieve logboekactiviteit.<!--MAGECLOUD-2517-->

- ![fixepictogram](../../assets/fix.svg) **Implementatieoplossingen**—

   - Nu wordt de onderhoudswijze toegelaten bij het begin van de opstellen fase en gehandicapt aan het eind. Als de plaatsing ontbreekt, blijft de plaats op onderhoudswijze tot de plaatsingskwesties worden opgelost. Eerder werd de productiemodus van de site hersteld, zelfs als de implementatie mislukte.<!--MAGECLOUD-2603-->

      - Herwerkte de controles van de plaatsingsfasbevestiging om het foutenniveau voor de volgende plaatsingskwesties van te verlagen `CRITICAL` tot `WARNING` zodat de implementatie is voltooid. Deze problemen hebben er eerder toe geleid dat de implementatie is mislukt.

      - De configuratie van het milieu bevat onjuiste waarden voor opstelling of wolkenvariabelen.

   - De versie van de Elasticsearch op de cloudinfrastructuur is niet compatibel met de versie van de elasticsearch/elasticsearch module die door Adobe Commerce wordt ondersteund op de cloudinfrastructuur. Zie de [Probleemoplossing voor Elasticsearch, artikel](https://support.magento.com/hc/en-us/articles/360015758471-Deployment-fails-or-interrupts-with-cloud-log-error-Elasticsearch-version-is-not-compatible-with-current-version-of-magento) in de knowledgebase voor Adobe Commerce-ondersteuning.<!--MAGECLOUD-2600-->

   - Probleem verholpen met de gedeelde configuratie-instellingen in het dialoogvenster `app/etc/config.php` bestand dat heeft veroorzaakt `recursion detected` fouten tijdens de implementatie.<!--MAGECLOUD-2173-->

- ![fixepictogram](../../assets/fix.svg) **Cron-gerelateerde correcties**—

   - Probleem verholpen met snijplanning waardoor taken niet konden worden uitgevoerd als u een andere snijfrequentie dan de standaardfrequentie (1 minuut) opgeeft.<!--MAGECLOUD-2602-->

   - Probleem verholpen in de implementatiefase die ervoor zorgde dat cron-taken tijdens de implementatie konden worden uitgevoerd, wat databasestlokken en andere kritieke problemen kan veroorzaken. Nu, worden alle kroonbanen tegengehouden alvorens de opstellen fase begint en opnieuw begonnen nadat de plaatsing voltooit.&lt;!—MAGECLOUD—2537—>

   - Oplossing voor de werkstroom voor uitsnijden in versie 2.2.x om bevroren uitsnijdtaken te ontgrendelen zodat deze kunnen worden gestopt voordat de implementatie wordt gestart. Eerder, veroorzaakte een bevroren kroonbaan de plaatsing aan stagnatie.<!--MAGECLOUD-2501-->

- ![fixepictogram](../../assets/fix.svg) De indeling van het dialoogvenster `config.php` bestand gegenereerd door de `vendor/bin/ece-tools config:dump` gebruiken om korte array syntaxis en 4-spaties inspringing te gebruiken om te voldoen aan Adobe Commerce-coderingsstandaarden.<!--MAGECLOUD-2527-->

- ![fixepictogram](../../assets/fix.svg) Oplossing voor een implementatiefout die optreedt wanneer de `.magento.env.yaml` contains `{{ base_url }}` en `{{ unsecure_base_url }}` tijdelijke aanduidingen voor webconfiguraties in plaats van de standaard-URL-configuratie voor een Adobe Commerce-infrastructuurproject in de cloud./<!--MAGECLOUD-2607-->

## v2002.0.13

- ![nieuw pictogram](../../assets/new.svg) **Implementatie zonder downtime inschakelen**—Adobe Commerce op cloudinfrasinfrastructuurwachtrijen stelt tijdens de implementatie aanvragen voor vereiste databasewijzigingen in en past de wijzigingen toe zodra de implementatie is voltooid. Verzoeken kunnen maximaal 5 minuten worden bewaard om ervoor te zorgen dat geen sessies verloren gaan. Zie [Statische implementatieopties voor inhoud om downtime bij implementatie op Cloud te reduceren](https://support.magento.com/hc/en-us/articles/360004861194-Static-content-deployment-options-to-reduce-deployment-downtime-on-Cloud).<!--MAGECLOUD-2169-->

- ![nieuw pictogram](../../assets/new.svg) **Docker-compositie voor cloud**—Breng de volgende verbeteringen aan in de [Installatie en configuratie van Docker](https://devdocs.magento.com/cloud/docker/docker-config.html) proces:

   - Een opdracht toegevoegd—`docker:config:convert` om PHP-configuratiebestanden om te zetten in Docker ENV-indeling om de configuratie van de omgeving te vereenvoudigen. Nu kopieert u de PHP-configuratiebestanden naar de Docker-map en zet u ze om in Docker ENV-bestanden. Zie [Docker starten](https://devdocs.magento.com/cloud/docker/docker-config.html).<!--MAGECLOUD-2359-->

   - Het installatieproces van Adobe Commerce on cloud Infrastructure ondersteunt nu de implementatie op zowel read-only- als read-write-bestandssystemen om het Cloud-bestandssysteem beter te emuleren. Zie [Docker configureren](https://devdocs.magento.com/cloud/docker/docker-config.html).&lt;!—MAGECLOUD—2357—>

   - **Redis-service**—Voegt een Redis beeld toe, dat aan een container van de Dokker wordt opgesteld en automatisch om met uw installatie van de Dokker wordt gevormd te werken.&lt;!—MAGECLOUD—2442—>

   - Nu hebt u de mogelijkheid om de database te dumpen wanneer u de Cloud Docker gebruikt [databasecontainer](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#database-container). U kunt ook [bestanden delen](https://devdocs.magento.com/cloud/docker/docker-containers.html#sharing-data-between-host-machine-and-container) tussen een hostcomputer en een container die de `docker/mnt` directory.<!-- MAGECLOUD-2577 -->

   - **Varnish service support**— Er is een vernis-afbeelding toegevoegd, die automatisch wordt geïmplementeerd in een Docker-container. Na plaatsing, kunt u Varnish na de beste praktijken van Adobe Commerce manueel vormen. Zie [Varnish configureren en gebruiken](https://devdocs.magento.com/guides/v2.3/config-guide/varnish/config-varnish.html).&lt;!—MAGECLOUD—2358—>

   - Toegang tot de site beveiligen—Toegevoegde SSL-ondersteuning voor toegang tot uw Adobe Commerce-winkel en het deelvenster Beheer.&lt;!—MAGECLOUD—2360—>

- ![fixepictogram](../../assets/fix.svg) **Verbeterde Adobe Commerce voor ondersteuning van cloudinfrastructuur**—De minimale versie voor het pakket guzzlehttp/guzzle in de Adobe Commerce inzake cloudinfrastructuur is verlaagd [composer.json, bestand](https://devdocs.magento.com/cloud/reference/cloud-composer.html) naar versie 6.2, zodat de `ece-tools` pakket is compatibel met meer extensies.<!--MAGECLOUD-2205-->

- ![nieuw pictogram](../../assets/new.svg) **Aangepaste wijzigingen toepassen op uw Adobe Commerce-toepassing tijdens de constructiefase**—Wij verdelen de bouwstijlfase in twee afzonderlijke processen zodat u haken kunt gebruiken om douaneveranderingen op de geproduceerde statische inhoud toe te passen alvorens de toepassing voor plaatsing te verpakken. De _build:generate_ procesgenereert code, past patches toe en genereert statische inhoud. De _build:overdracht_ De gegenereerde code en statische inhoud worden door het proces naar de uiteindelijke bestemming overgedragen. Zie [Toepassingshaken](https://devdocs.magento.com/cloud/project/magento-app-properties.html#hooks).<!--MAGECLOUD-2363-->

- ![fixepictogram](../../assets/fix.svg) **Configuratiecontroles in de omgeving**—Verbeterde validatie van de configuratie van de omgeving om klanten te waarschuwen voor incompatibiliteiten en configuratiefouten bij versies voordat ze Adobe Commerce bouwen en implementeren op cloudinfrastructuur.

   - Toegevoegde versie-specifieke bevestiging om niet gestaafde of verouderde omgevingsvariabelen en waarden te identificeren.<!--MAGECLOUD-2183-->

   - Er is een compatibiliteitscontrole voor Elasticsearch toegevoegd om gebruikers te waarschuwen voor problemen met de configuratie van Elasticsearch. De implementatie mislukt nu als de versie van de service Elasticsearch op de server niet compatibel is met Adobe Commerce. Eerder, slaagde de plaatsing zelfs als de versie van de Elasticsearch incompatibel was, die de kwesties van de productcatalogus na plaatsplaatsing veroorzaakte.<!--MAGECLOUD-2389-->

     U kunt de incompatibiliteit oplossen door [een ondersteuningsticket indienen](https://devdocs.magento.com/cloud/trouble/trouble.html) om Elasticsearch aan een compatibele versie te bevorderen, of de configuratie van Adobe Commerce te veranderen om een compatibele versie van de Elasticsearch PHP cliënt te specificeren.

      - Voor Adobe Commerce versie 2.1.x tot 2.2.2, bevorder Elasticsearch aan versie 2.4.

      - Voer voor Adobe Commerce versie 2.2.3 en hoger een upgrade uit naar Elasticsearch 5.2.

      - Als u Elasticsearch 1.x of 2.x hebt en geen verbetering wilt, werk de PHP cliëntversievereisten van de Elasticsearch van Adobe Commerce in composer.json bij aan `"elasticsearch/elasticsearch": "~2.0"`.

   - Verbeterde validatie van omgevingsvariabelen om configuratie-instellingen te identificeren die conflicten kunnen veroorzaken tijdens de fasen build, implementatie en implementatie na implementatie. Er wordt bijvoorbeeld een waarschuwingsbericht weergegeven tijdens het installatie- en upgradeproces als de algemene instelling voor de implementatie van statische inhoud een conflict veroorzaakt met instellingen in de ontwikkelings- of implementatiefase.<!--MAGECLOUD-2156-->

- ![fixepictogram](../../assets/fix.svg) **Updates van omgevingsvariabelen**—Gewijzigd de volgende omgevingsvariabelen:

   - **[Globale variabele SKIP_HTML_MINIFICATION](../environment/variables-global.md#skip_html_minification)**—De standaardwaarde is gewijzigd in `true` om op bestelling HTML-inhoud te minimaliseren, waardoor downtime bij de implementatie tot een gefaseerde en productieomgeving wordt beperkt. Deze configuratie wordt vereist voor nul-onderbreking plaatsingen.<!--MAGECLOUD-2435-->

   - **[CLEAN_STATIC_FILES implementeert variabele](../environment/variables-deploy.md#clean_static_files)**—Toegevoegd de capaciteit om de schone statische die dossierverwerking voor statische inhoud te beheren tijdens de bouwstijlfase wordt geproduceerd die op CLEAN_STATIC_FILES milieu veranderlijke het plaatsen wordt gebaseerd. Voorheen werden tijdens de constructiefase gegenereerde statische inhoudsbestanden altijd schoongemaakt.<!--MAGECLOUD-1506-->

- ![fixepictogram](../../assets/fix.svg) **Logboekregistratie**—Breng de volgende wijzigingen aan om de logberichten te verbeteren en de logbestandsgrootte te verkleinen:

   - De de mislukkingslogboekingangen van de plaatsing omvatten nu de beveloutput van de verrichtingen die de mislukkingen veroorzaken zelfs als uw milieuconfiguratie niet zuivert niveau registreren specificeert. Zie [`MIN_LOGGING_LEVEL`](../environment/variables-global.md#min_logging_level).<!--MAGECLOUD-2489-->

   - Toegevoegde logboekregistratie voor implementatiefouten die optreden wanneer gegenereerde fabrieken die door sommige extensies worden vereist, niet correct worden gegenereerd omdat het bestandssysteem alleen-lezen is.<!--MAGECLOUD-2209-->

   - Minder implementatielogboekgrootte en opgeloste opmaakproblemen die worden veroorzaakt door instellingsopdrachten die gebruikmaken van de interactieve voortgangsbalk.<!--MAGECLOUD-2402-->

   - De elimineerde onnodige breedheid en werkte de prioritaire niveaus voor sommige logboekverklaringen bij.<!--MAGECLOUD-2227-->

- ![fixepictogram](../../assets/fix.svg) **Cron-specifieke correcties**—

   - Veranderde de standaard montages van de baanconfiguratie van de kroon voor geschiedenisleven van 3d (4320 min) aan 1h (60 min) om prestatieskwesties en plaatsingsmislukkingen te verhinderen die kunnen voorkomen wanneer de kroonrij te snel vult.<!--MAGECLOUD-2427-->

   - Verbeterde het cron proces van het baanbeheer tijdens de opstellen fase om gegevensbestandsloten en andere kritieke kwesties te verhinderen. Nu, stoppen alle kroonbanen tijdens de plaatsingsfase en beginnen opnieuw na plaatsing voltooit.<!--MAGECLOUD-2445-->

   - Probleem verholpen met het vergrendelingsmechanisme voor het plannen van consumenten die worden opgestart door cron-taken in Adobe Commerce versie 2.2.0 en hoger om te voorkomen dat cron-banen dubbele consumenten op de markt brengen.<!--MAGECLOUD-2464-->

- ![fixepictogram](../../assets/fix.svg) Probleem met de [compressieproces statische inhoud](../environment/variables-intro.md) (`gzip`) die `not overwritten` en `no such file or directory` fouten bij het verwijzen naar het gecomprimeerde bestand tijdens het implementatieproces.<!-- MAGECLOUD-2182-->

- ![fixepictogram](../../assets/fix.svg) Het probleem dat ervoor zorgde dat de `php ./vendor/bin/ece-tools config:dump` bevel van het verwijderen van overtollige secties uit `config.php` bestand tijdens het dumpproces als de landinstelling van de winkel niet is opgegeven. Nu kunt u uw configuratiebestanden eenvoudig tussen omgevingen verplaatsen. Nadat u de update naar `ece-tools` v2002.0.13, oudere versies opnieuw genereren `config.php` bestanden met de verbeterde `config:dump` gebruiken. Zie [Configuratiebeheer voor opslaginstellingen](https://devdocs.magento.com/cloud/live/sens-data-over.html).<!--MAGECLOUD-2444-->

- ![fixepictogram](../../assets/fix.svg) Vaste een kwestie die een fout tijdens opstellen fase veroorzaakte als de routeconfiguratie in `.magento/routes.yaml` bestanden worden omgeleid vanuit een [apex](https://blog.cloudflare.com/zone-apex-naked-domain-root-domain-cname-supp/) naar een `www` domein.<!--MAGECLOUD-2556-->

- ![fixepictogram](../../assets/fix.svg) Probleem met de `_merge` voor de [`SEARCH_CONFIGURATION`](../environment/variables-deploy.md#search_configuration) variabele die onjuiste resultaten bij het samenvoegen heeft veroorzaakt als u de `engine` in de bijgewerkte `.magento.env.yaml` configuratiebestand. Nu overschrijft de samenvoegbewerking alleen de waarden die u in de bijgewerkte versie hebt opgegeven `.magento.env.yaml` zonder dat u de opdracht `engine` parameter.<!--MAGECLOUD-2520-->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen met een configuratie van Redis waarbij sessieslocking voor Adobe Commerce op cloudinfrasinfrastructuurversie 2.2.1 en hoger onjuist is ingeschakeld, wat kan leiden tot trage prestaties en time-outs. Sessievergrendeling is nu standaard uitgeschakeld. Het probleem werd veroorzaakt door een wijziging in het standaardgedrag van de `disable_locking` parameter die is geïntroduceerd in v1.3.4 van het Redis-pakket voor sessiehandlers. Zie [colinmolenhour/php-redis-session-abstract pakket](https://github.com/colinmollenhour/php-redis-session-abstract).<!-- MAGECLOUD-2515-->

## v2002.0.12

- ![nieuw pictogram](../../assets/new.svg) **Docker-compositie voor cloud**—Een opdracht toegevoegd—`docker:build`—om een [Samenstellen dokken](https://devdocs.magento.com/cloud/docker/docker-config.html) configuratie vanuit de cloud `ece-tools` opslagplaats.<!-- MAGECLOUD-2250 -->

- ![nieuw pictogram](../../assets/new.svg) **Landinstellingen wijzigen**—Nu kunt u de opslaglandinstelling wijzigen zonder het configuratieproces voor exporteren en importeren. Terwijl de toepassing in Productie is en SCD_ON_DEMAND wordt toegelaten, zijn de opslag en admin scèneopties beschikbaar.<!-- MAGECLOUD-2019 -->

- ![nieuw pictogram](../../assets/new.svg) <!-- MAGECLOU-1998 -->**Site-overzicht en Robots**—Gemaakt met een [werkstroom](../store/robots-sitemap.md) om een `robots.txt` bestand en genereren een `sitemap.xml` bestand voor een configuratie met één domein zonder dat de infrastructuur hoeft te worden gewijzigd.

- ![nieuw pictogram](../../assets/new.svg) **Wizards**—Twee toegevoegd [wizards](../deploy/smart-wizards.md) voor hulp bij de configuratie van de cloud:<!-- MAGECLOUD-1910 -->

   - `ideal-state`—vorm de ideale staat voor minimale plaatsingsonderbreking

   - `master-slave`—load balancing voor database en Redis configureren

- ![nieuw pictogram](../../assets/new.svg) **Module vernieuwen**—Cloud-opdracht toegevoegd—`module:refresh`—om modules toe te laten die onbruikbaar werden gemaakt of niet uitdrukkelijk toegelaten, gelijkend op de manier dat het automatisch tijdens een bouwstijl wordt gedaan.<!-- MAGECLOUD-1521 -->

- ![nieuw pictogram](../../assets/new.svg) De mogelijkheid toegevoegd om configuratie voor services samen te voegen of te overschrijven met de `_merge` optie in [CACHE](../environment/variables-deploy.md#cache_configuration), [SESSIE](../environment/variables-deploy.md#session_configuration), [WACHTRIJ](../environment/variables-deploy.md#queue_configuration), en [ZOEKEN](../environment/variables-deploy.md#search_configuration) configuraties.<!-- MAGECLOUD-2105 -->

- ![nieuw pictogram](../../assets/new.svg) **Voorbeeldbestand voor configuratie van omgeving**—We hebben een `.magento.env.yaml` voorbeeldbestand bij het ECE-Tools-pakket dat een gedetailleerde beschrijving en mogelijke waarden voor elke omgevingsvariabele bevat.<!-- MAGECLOUD-1908 -->

   - We hebben ook een uitgebreide validatie toegevoegd voor de `.magento.env.yaml` configuratie die mislukkingen in het plaatsingsproces verhindert die door onverwachte waarden worden veroorzaakt. Wanneer een fout optreedt, ontvangt u nu een gedetailleerd foutbericht dat begint met: `Environment configuration is not valid. Please correct .magento.env.yaml file with next suggestions:`<!-- MAGECLOUD-1907 -->

- ![nieuw pictogram](../../assets/new.svg) Het volgende toegevoegd: [**Omgevingsvariabelen**](../environment/variables-intro.md):

   - U kunt nu meerdere landinstellingen definiëren voor elk thema met het nieuwe [SCD_MATRIX](../environment/variables-deploy.md#scd_matrix) omgevingsvariabele, die de hoeveelheid te implementeren themabestanden vermindert.<!-- MAGECLOUD-1501 -->

   - De [DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration) omgevingsvariabele om uw databaseverbindingen aan te passen voor implementatie.<!-- MAGECLOUD-2047 -->

   - De nieuwe [MIN_LOGGING_LEVEL](../environment/variables-global.md#min_logging_level) de variabele treedt het minimumregistrerenniveau voor alle outputstromen met voeten zonder veranderingen in de code aan te brengen.<!-- MAGECLOUD-2129 -->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen die downtime veroorzaakte tussen de implementatiefase en de post-implementatiefase. Nu, begint de post-implementatiefase _onmiddellijk_ nadat de implementatiefase is beëindigd.

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen waarbij de succesvolle snijtaken niet werden gecorrigeerd, die met `status = success`, van het schema.<!-- MAGECLOUD-2268 -->

- ![fixepictogram](../../assets/fix.svg) Probleem met de `post_deploy` haak die het geheime voorgeheugen in opstelt fase in plaats van de post-opstelt fase van het project ontruimde.<!-- MAGECLOUD-2113 -->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen bij het gebruik van SCD met meerdere landinstellingen, wat hetzelfde genereerde `js-translation.json` bestand voor elke landinstelling.<!-- MAGECLOUD-2034 -->

- ![fixepictogram](../../assets/fix.svg) Geoptimaliseerd de `db:dump` in de `ece-tools` pakket om vergrendelde tabellen te voorkomen en de snelheid te verhogen.<!-- MAGECLOUD-2033 -->

## v2002.0.11

>[!NOTE]
>
>Voor compatibiliteit met versie 2.2.4 is ECE-Tools versie 2002.0.11 vereist.

- ![nieuw pictogram](../../assets/new.svg) **Alleen-lezen verbindingen met niet-hoofdknooppunten configureren**—Deze versie voegt de capaciteit toe om een read-only verbinding aan een niet hoofdknoop te vormen om read-only verkeer (voor te ontvangen  [MariaDB](../environment/variables-deploy.md#mysql_use_slave_connection)).<!--MAGECLOUD-143 -->[Redis](../environment/variables-deploy.md#redis_use_slave_connection) en voor <!--MAGECLOUD-143 -->

- ![nieuw pictogram](../../assets/new.svg) **Configuratiewizard**—Toegevoegd een tovenaar helpen uw configuratie voor statische inhoudsplaatsing verifiëren. Zie [Slimme wizards](../deploy/smart-wizards.md).<!--MAGECLOUD-1910 -->

- ![nieuw pictogram](../../assets/new.svg) **Ondersteuning voor Symfony Console**—Toegevoegde ondersteuning voor Symfony Console 4 met Adobe Commerce 2.3.<!-- MAGECLOUD-1966 -->

- ![fixepictogram](../../assets/fix.svg) **Optimalisaties voor uitsnijden plannen**—Verbeterde het rijbeheer en verbeterde registreren om met het zuiveren van op elkaar betrekking hebbende kwesties te helpen.<!-- MAGECLOUD-1607 -->

- ![fixepictogram](../../assets/fix.svg) Validatie van implementatie mislukt als een `ADMIN_EMAIL` of `ADMIN_USERNAME` Deze waarde is gelijk aan een bestaande beheerdersaccount.<!-- MAGECLOUD-1221 -->

- ![fixepictogram](../../assets/fix.svg) Verwijderd SOLR-ondersteuning voor 2.2.x-versies. 2.1.x-versies behouden de mogelijkheid SOLR in te schakelen.<!-- MAGECLOUD-1282 -->

- ![fixepictogram](../../assets/fix.svg) De eerste installatie van de Fases &amp; Production-omgevingen van een PRO-project bevat nu verschillende indexvoorvoegsels voor Elasticsearch om mogelijke conflicten te voorkomen en records die bij elke omgeving horen, te identificeren.<!-- MAGECLOUD-1489 -->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen waarbij de constructiefase voor oudere architectuur tijdens de implementatie van statische inhoud werd onderbroken.<!-- MAGECLOUD-2021 -->

- ![fixepictogram](../../assets/fix.svg) **Cron-specifieke verbeteringen**—Herwerkte de cron-implementatie:<!-- MAGECLOUD-1607 -->

   - Probleem verholpen waarbij de wachtrij voor uitsnijden snel werd gevuld. Nu worden de achterhaalde kroonbanen op een betrouwbaardere manier gewist.

   - Herorganiseerde de opeenvolging van kroonbanen zodat alle banen in afzonderlijke draden vóór de algemene groep lanceren.

   - Verbeterde logboekregistratie om u beter te helpen bij het opsporen van fouten in uitsnijdingen.

   - **OPMERKING**—Deze release behandelt veel problemen met betrekking tot het gebruik van scènes. Als u momenteel bepaalde aan uitsnijden gerelateerde patches gebruikt in _m2-hotfixes_, verwijdert u deze.

- ![fixepictogram](../../assets/fix.svg) **SCD-specifieke verbeteringen**—

   - U kunt de `VERBOSE_COMMANDS` en de `SCD_COMPRESSION_LEVEL` omgevingsvariabelen tijdens beide _build_ en de_ploy-fasen.<!-- MAGECLOUD-1819 -->

   - Probleem verholpen waarbij implementatie mislukte met een willekeurige fout bij het tegenkomen van een onverwachte waarde voor de `SCD_COMPRESSION_LEVEL` omgevingsvariabele. Verbeterde configuratievalidering voor betekenisvolle meldingen. Zie [`SCD_COMPRESSION_LEVEL`](../environment/variables-build.md#scd_compression_level) voor aanvaardbare waarden.<!-- MAGECLOUD-2043 -->

   - Het gedrag van de `SCD_COMPRESSION_LEVEL` omgevingsvariabele configuratiestroom zodat de overschrijvingen werken zoals verwacht.<!-- MAGECLOUD-2044 -->

   - Probleem verholpen waardoor de configuratie van de `SCD_THREADS` omgevingsvariabele in de `.magento.env.yaml` file _inzetten_ in het werkgebied.<!-- MAGECLOUD-2046 -->

## v2002.0.10

- ![nieuw pictogram](../../assets/new.svg) **Static Content Deployment (SCD)**—Er is een nieuw, alternatief plaatsingsproces om statische inhoud te produceren wanneer gevraagd (op bestelling). Dit vermindert onderbreking en verbetert geheim voorgeheugenbehandeling door de meest kritieke activa te produceren.<!-- MAGECLOUD-1285 -->

   - **Nieuwe omgevingsvariabele**—Toegevoegd de `SCD_ON_DEMAND` globale omgevingsvariabele om statische inhoud te genereren wanneer hierom wordt gevraagd.<!-- MAGECLOUD-1738 -->

   - **Haak na implementatie**—Toegevoegd a `post_deploy` haak voor de `.magento.app.yaml` bestand dat de cache wist en de cache vooraf laadt (wringt) _na_ de container begint met het accepteren van verbindingen. Het is alleen beschikbaar voor Pro-projecten die omgevingen voor Staging en Productie bevatten in de [!DNL Cloud Console] en voor Starter-projecten. Hoewel dit niet vereist is, werkt dit in overeenstemming met de `SCD_ON_DEMAND` omgevingsvariabele.<!-- MAGECLOUD-1788 -->

- ![nieuw pictogram](../../assets/new.svg) **Optimalisatie**—Geoptimaliseerd verplaatsen of kopiëren van bestanden tijdens de implementatie om de implementatiesnelheid te verbeteren en de belasting van het bestandssysteem te verminderen.<!-- MAGECLOUD-1842 -->

- ![nieuw pictogram](../../assets/new.svg) **Implementatieregistratie**—Toegevoegd de capaciteit om de managers van het Logboek van Syslog en van Graylog Uitgebreide (GELF) voor outputs logboeken tijdens het plaatsingsproces toe te laten. Zie [Logboekhandlers](../environment/log-handlers.md).<!-- MAGECLOUD-1751 -->

- ![nieuw pictogram](../../assets/new.svg) Het volgende toegevoegd: [**Omgevingsvariabelen**](../environment/variables-intro.md):

   - `CRYPT_KEY`—Verstrek een cryptografische sleutel aan een andere milieu wanneer het bewegen van een gegevensbestand.<!-- MAGECLOUD-1556 -->

   - `SKIP_HTML_MINIFICATION`—_Algemeen_ omgevingsvariabele die het kopiëren van de statische weergavebestanden in de `var/view_preprocessed` en genereert geminificeerde HTML op verzoek.<!-- MAGECLOUD-1621 and MAGECLOUD-1736-->

   - `SCD_ON_DEMAND`—_Algemeen_ omgevingsvariabele om statische inhoud te genereren wanneer hierom wordt gevraagd.<!-- MAGECLOUD-1738 -->

   - `WARM_UP_PAGES`—U kunt de pagina&#39;s vermelden die u wilt gebruiken om de cache vooraf te laden. Beschikbaar in het nieuwe [Variabelen na implementatie](../environment/variables-post-deploy.md).

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen waarbij een lokaal toegepaste patch werd gebruikt die de implementatie op een instantie verbreekt. ECE-Tools kan nu detecteren dat een patch is toegepast.<!-- MAGECLOUD-982 -->

- ![fixepictogram](../../assets/fix.svg) Oplossing voor een conflict tussen JavaScript-bundeling en GZIP-functionaliteit. Deze functies werken nu goed samen.<!-- MAGECLOUD-1735 -->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen waarbij CLI-opdrachten van ECE-Tools mislukten bij gebruik van eerdere PHP 7.0.x-versies.<!-- MAGECLOUD-1744 -->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen dat statische inhoudsplaatsing met de compacte strategie in veelvoudige draden verhinderde.<!-- MAGECLOUD-1822 -->

- ![fixepictogram](../../assets/fix.svg) Probleem verholpen waarbij de sessie van Redis werd vergrendeld en de aanmelding bij Admin werd vertraagd. De oplossing is ook beschikbaar voor 2.1.x.<!-- MAGECLOUD-1853 -->

## v2002.0.9

>[!NOTE]
>
>U moet [upgrade uitvoeren van het Adobe Commerce-pakket voor cloudinfrastructuur](../dev-tools/install-package.md#update-the-metapackage) om dit en alle toekomstige updates te krijgen.

- ![nieuw pictogram](../../assets/new.svg) **Gereedschappen**—De `ece-tools` -pakket ondersteunt nu Adobe Commerce 2.1.x.<!-- MAGECLOUD-1086 -->

- ![nieuw pictogram](../../assets/new.svg) **Redis-configuratie**—U kunt nu [Redis configureren](../environment/variables-deploy.md#cache_configuration) pagina en standaardcache en Redis-sessieopslag met behulp van een omgevingsvariabele.<!-- MAGECLOUD-1552 -->

- ![nieuw pictogram](../../assets/new.svg) **De de dienstverbeteringen van het Onderzoek, AMQP en Redis**—Wij verenigden de stroom van de de dienstconfiguratie zodat het zich nu de zelfde manier voor alle diensten gedraagt. De `env.php` bestand voor het configureren van services wordt niet meer ondersteund. U moet omgevingsvariabelen of de `.magento.env.yaml` in plaats daarvan.<!-- MAGECLOUD-1437 -->

- ![fixepictogram](../../assets/fix.svg) **Omgevingsvariabelen**—

   - Het gebruik van `env:STATIC_CONTENT_THREADS` is vervangen en wordt in een toekomstige versie verwijderd. Gebruik de [SCD_THREADS](../environment/variables-deploy.md#scd_threads) in plaats daarvan.<!-- MAGECLOUD-1507 -->

   - De `STATIC_CONTENT_EXCLUDE_THEMES` omgevingsvariabele is vervangen. U moet de opdracht `SCD_EXCLUDE_THEMES` omgevingsvariabele.<!-- MAGECLOUD-1640 -->

- ![fixepictogram](../../assets/fix.svg) **Logboekregistratie**—We vereenvoudigden het aanmelden bij ingebouwde patchbewerkingen.<!-- MAGECLOUD-1674 -->

- ![fixepictogram](../../assets/fix.svg) We hebben verwijderd `developer` modusondersteuning en de `APPLICATION_MODE` omgevingsvariabele omdat deze tot onverwacht gedrag leidden.<!-- MAGECLOUD-1615 -->

- ![fixepictogram](../../assets/fix.svg) We hebben een probleem verholpen dat ertoe leidde dat er problemen waren met de implementatie van statische inhoud met betrekking tot Redis. De implementatie van meerthreaded statische inhoud wordt nu uitgevoerd zoals is ontworpen.<!-- MAGECLOUD-1630 -->

- ![fixepictogram](../../assets/fix.svg) We hebben een probleem opgelost dat ervoor zorgde dat gebruikers geen wijzigingen konden opslaan in configuratievelden in de Admin. Deze worden gemarkeerd als gevoelig na het uitvoeren van de `app:config:dump` gebruiken.<!-- MAGECLOUD-1175 -->

- ![fixepictogram](../../assets/fix.svg) We hebben ondersteuning toegevoegd voor een eerdere versie van `symfony/yaml` om conflicten op te lossen met sommige pakketten, die nog niet compatibel zijn met de meest recente versie.<!-- MAGECLOUD-1674 -->

## v2002.0.8

>[!NOTE]
>
>We zijn samengevoegd `vendor/magento/ece-patches` with `vendor/magento/ece-tools` in deze release. U hoeft de `vendor/magento/ece-patches` afzonderlijk verpakken.

**Nieuwe functies:**

- **Verbeterde logboekregistratie**<!-- MAGECLOUD-1253 -MAGECLOUD-1495 -->
   - Wij verbeterden logboekoverseinen om betere verklaringen te verstrekken wanneer de bouwstijl of het proces opstelt een milieuvariabele met voeten treedt.
   - U kunt nu de voortgang van de installatie en upgrade in real-time bekijken. Tik de `install_update.log` om de voortgang te bekijken. Bijvoorbeeld:

     ```bash
     tail -f var/log/install_upgrade.log
     ```

- **Nieuwe uitsnede, opdracht**—U kunt nu specifieke vastgezette banen ontgrendelen in plaats van ze allemaal te stoppen en opnieuw te lanceren met de [`cron:unlock`](https://support.magento.com/hc/en-us/articles/360033099451) gebruiken. Niet beschikbaar in 2.1.<!-- MAGECLOUD-1367 -->

- **Unified Configuration-bestand**—U kunt bouwstijl nu vormen en stadia opstellen gebruikend [`.magento.env.yaml`](https://devdocs.magento.com/cloud/project/magento-env-yaml.html) bestand.<!-- MAGECLOUD-1369 -->

- **Back-upconfiguratiebestanden**—Het implementatieproces maakt nu automatisch een back-up van de `app/etc/env.php` en `app/etc/config.php` configuratiebestanden na de implementatie. We hebben ook een [new CLI, opdracht](https://support.magento.com/hc/en-us/articles/360033182871) om deze configuratiedossiers van een steun te herstellen.<!-- MAGECLOUD-1372 -->

- **Problemen met validatiefouten oplossen**—We hebben de opdracht gewijzigd die u moet gebruiken om validatiefouten op te lossen wanneer `config.php` bevat niet genoeg gegevens voor statische inhoudsplaatsing. Eerder gaf het foutbericht u de instructie om te starten `bin/magento app:config:dump`. Nu moet u starten `php ./vendor/bin/ece-tools config:dump`.<!-- MAGECLOUD-1491 -->

- **Nieuwe omgevingsvariabelen**—U kunt nu omgevingsvariabelen gebruiken om aangepaste verbindingen te maken [zoeken](../environment/variables-deploy.md#search_configuration) en [op AMQP gebaseerd](../environment/variables-deploy.md#queue_configuration) services naar uw site.<!-- MAGECLOUD-1410 -->

- We hebben intelligente patching geïmplementeerd. Het pakket past nu patches toe die niet op Adobe Commerce zijn gebaseerd op de versie van de cloudinfrastructuur, maar op de versie van het patchpakket.<!--MAGECLOUD-1090-->

**Opgeloste problemen:**

- We hebben een probleem met logbestanden opgelost dat bouwfouten veroorzaakte.<!-- MAGECLOUD-1162 -->

- We hebben een probleem opgelost dat tot onderbrekingsuitzonderingen leidde wanneer implementaties in de interactieve modus werden uitgevoerd.<!-- MAGECLOUD-1389 -->

- We hebben een probleem opgelost dat fouten veroorzaakte bij het gebruik van de compacte strategie voor het genereren van statische inhoud. Niet beschikbaar in 2.1.<!-- MAGECLOUD-1446 MAGECLOUD-1485-->

- We hebben een probleem opgelost dat voorkwam dat het implementatiescript niet in staat was om testomgevingen en productieomgevingen correct te identificeren.<!-- MAGECLOUD-1493 -->

- We hebben een probleem verholpen dat ervoor zorgde dat netwerkproblemen databaseverbindingen onderbreken en fouten veroorzaken tijdens het installatie- en upgradeproces.<!-- MAGECLOUD-1520 -->

- We hebben een probleem opgelost waardoor u de configuratiebestanden niet kunt exporteren met `app:config:dump` meer dan eenmaal. Niet beschikbaar in 2.1.<!--  MAGECLOUD-1567  -->

- We hebben een Redis-sessie opgelost _vergrendelen_ een probleem dat een _Beheerder_ aanmeldvertraging. Niet beschikbaar in 2.1.<!--  MAGECLOUD-1582  -->

- We hebben een implementatieprobleem opgelost dat te maken had met versioning en dat tot een conflict leidde met andere op composers gebaseerde patchmodules.<!-- MAGECLOUD-1450 -->

- We hebben een probleem opgelost dat tijdens het importeren problemen met het PHP-geheugen veroorzaakte.<!-- MAGECLOUD-1310 -->

- Verwijderde patch; bug herstellen in `colinmollenhour/credis` v1.6 om ondersteuning voor Adobe Commerce op cloudinfrastructuur mogelijk te maken 2.2.1. Niet beschikbaar in 2.1.<!-- MAGECLOUD-1033 -->

## v2002.0.7

**Opgeloste problemen:**

- We hebben verwijderd `var/view_preprocessed` een probleem dat tot JavaScript-minificatieconflicten heeft geleid, met symlinking oplossen.<!-- MAGECLOUD-1454 -->

## v2002.0.6

**Opgeloste problemen:**

- We hebben een probleem opgelost dat `gzip` fouten wanneer een dossier of een foldernaam ruimten bevat.<!-- MAGECLOUD-1413 -->

- We hebben een probleem opgelost dat ervoor zorgde dat implementatiescripts niet naar behoren konden herkennen en moduleafhankelijkheden konden inschakelen.<!-- MAGECLOUD-1424 -->

## v2002.0.5

**Nieuwe functies:**

- **Een cron-consument configureren met een omgevingsvariabele**—U kunt nu randconsumenten configureren met de nieuwe `CRON_CONSUMERS_RUNNER` omgevingsvariabele.

- **Configuratiescherm**—Tijdens het ontwikkelings-/implementatieproces wordt nu naar kritieke componenten gescand en het proces wordt gestopt als de scan mislukt. Hierdoor wordt onnodige downtime voorkomen omdat de site in de onderhoudsmodus staat.

- **Meldingen samenstellen/implementeren**—Wij hebben een configuratiedossier toegevoegd dat u kunt gebruiken aan [Slack- en/of e-mailmeldingen instellen](../environment/set-up-notifications.md) voor het samenstellen/implementeren van acties in al uw omgevingen.

- **Statische inhoudscompressie**—We comprimeren nu statische inhoud met [gzip](https://www.gnu.org/software/gzip/) tijdens de bouw en opstellen fasen. Deze compressie, in combinatie met een snelle compressie, helpt uw winkel te verkleinen en de implementatiesnelheid te verhogen. Indien nodig kunt u compressie uitschakelen met een [build, optie](../environment/variables-build.md) of [variabele implementeren](../environment/variables-deploy.md). Raadpleeg de volgende onderwerpen voor meer informatie:

   - [Omgevingsvariabelen van de toepassing](../application/variables-property.md)

   - [Statische prestaties voor implementatie van inhoud](../deploy/static-content.md)

   - [Implementatieproces](https://devdocs.magento.com/cloud/reference/discover-deploy.html)

- **Configuratiebeheer**—We genereren nu automatisch een `app/etc/config.php` in uw Git-opslagplaats tijdens de bouwfase, als deze nog niet bestaat. Het automatisch gegenereerde bestand bevat alleen een lijst met modules en extensies. Als het bestand al bestaat, gaat de constructiefase verder als normaal. Als u [Configuratiebeheer](../store/store-settings.md) op een later tijdstip wordt het bestand door de opdrachten bijgewerkt zonder dat extra stappen nodig zijn. Zie [Implementatieproces](https://devdocs.magento.com/cloud/reference/discover-deploy.html) voor meer informatie .

- **Database-dumps**—We hebben een `magento/ece-tools` CLI bevel voor het creëren van gegevensbestanddumps in alle milieu&#39;s. Voor de milieu&#39;s van de Productie van het Pro-plan, laat dit bevel slechts dumpen van één van drie high-availability knopen, zodat kunnen de productiegegevens die aan een verschillende knoop tijdens de stortplaats worden geschreven niet worden gekopieerd. Wij adviseren het zetten van de toepassing op onderhoudswijze alvorens een gegevensbestandstortplaats in de milieu&#39;s van de Productie te doen. Zie [Back-upbeheer](https://devdocs.magento.com/cloud/project/project-webint-snap.html#db-dump) voor meer informatie .

- **Beperkingen voor snijinterval opgeheven**—Het standaardinterval voor uitsnijden voor alle omgevingen die zijn ingericht in de regio&#39;s us-3, eu-3 en ap-3 is 1 minuut. Het standaardinterval voor uitsnijden in alle andere gebieden is 5 minuten voor Pro-integratieomgevingen en 1 minuut voor Pro Staging- en Productieomgevingen. Als u de bestaande uitsnijdtaken wilt wijzigen, bewerkt u de instellingen in `.magento.app.yaml` of maak een ondersteuningsticket voor Productie-/Staging-omgevingen. Zie [Uitsnijdtaken instellen](../application/crons-property.md#set-up-cron-jobs) voor meer informatie .

**Opgeloste problemen:**

- We hebben een probleem opgelost dat lange implementatietijden veroorzaakte doordat het implementatieproces het `cache-clean` verrichting vóór statische inhoudsplaatsing.<!-- MAGECLOUD-1327 -->

- We hebben een probleem verholpen dat fouten veroorzaakte tijdens de stationeringsstap voor statische inhoud in productieomgevingen.<!-- MAGECLOUD-1322 -->

- We hebben een probleem opgelost waardoor sommige `magento/ece-tools` opdrachten van logboekuitvoer naar `stderr`.<!-- MAGECLOUD-1264 -->

- We hebben een probleem opgelost waarbij basis-URL-waarden voorkomen in `env.php` van bijwerken in geknepen vertakkingen.<!-- MAGECLOUD-1242 -->

- We hebben een probleem opgelost dat de oorzaak was van `magento setup:install` gebruiken om een onbeveiligd voorvoegsel toe te voegen (`http://`) om basis-URL&#39;s te beveiligen.<!-- MAGECLOUD-1171 -->

- We hebben een probleem verholpen waardoor patchfouten geen implementatiefouten veroorzaken.<!-- MAGECLOUD-1170 -->

- We hebben een probleem opgelost dat `ece-tools` van het stoppen van uitvoering en het werpen van een uitzondering als geen flarden kunnen worden toegepast.<!-- MAGECLOUD-1152 -->

- We hebben een probleem verholpen dat fouten veroorzaakte bij het laden van de opslagruimte nadat het minieren van HTML in de beheerder was ingeschakeld.<!-- MAGECLOUD-1138 -->

## v2002.0.4

**Opgeloste problemen:**

- U kunt nu [handmatig opnieuw instellen van geplakte snijtaken](https://support.magento.com/hc/en-us/articles/360033099451) het gebruiken van een CLI bevel in alle milieu&#39;s via de toegang van SSH. Het implementatieproces herstelt automatisch snijtaken.<!-- MAGECLOUD-1355 -->

## v2002.0.3

**Opgeloste problemen:**

- We hebben een probleem opgelost dat ertoe leidde dat pagina&#39;s uitvielen omdat Redis te lang duurde om te lezen/schrijven. U kunt nu de opdracht `disable_locking` parameter in Redis-configuraties om dit probleem te voorkomen.<!-- MAGECLOUD-1311 -->

## v2002.0.2

**Opgeloste problemen:**

- De [!DNL RabbitMQ] bij het configuratieproces worden nu automatisch alle vereiste parameters opgehaald.<!-- MAGECLOUD-1246 -->

## v2002.0.1

**Nieuwe functies:**

- Adobe Commerce op cloudinfrastructuur ondersteunt nu het bereik en [strategieën voor implementatie van statische inhoud](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-static-deploy-strategies.html). We hebben de `–s` parameter met een standaardinstelling van `quick` voor de strategie voor de implementatie van statische inhoud. U kunt de omgevingsvariabele gebruiken [SCD_STRATEGY](../environment/variables-deploy.md) om deze strategieën met uw bouw aan te passen en acties op te stellen. Deze variabele ondersteunt de opties `standard`, `quick`, of `compact`. Als u `compact`, overschrijven we de `STATIC_CONTENT_THREADS` waarde met `1`, die de implementatie kan vertragen, vooral in productieomgevingen. Niet beschikbaar in 2.1.<!--- MAGECLOUD-1057 -->

- We hebben een logbestand voor omgevingen gemaakt om acties vast te leggen en te compileren en implementeren. De `var/log/cloud.log` bevindt zich in de hoofdmap van de toepassing.<!--- MAGECLOUD-1014 & MAGECLOUD-1023 -->

**Opgeloste problemen:**

- Refactoring `ece-tools` -pakket om het compatibel te maken met Adobe Commerce op cloudinfrastructuur 2.2.0 en hoger.<!-- MAGECLOUD-919 & MAGECLOUD-1030 -->

- We hebben een probleem opgelost dat verhinderd was `ece-tools` van het stoppen van uitvoering en het werpen van een uitzondering als geen flarden kunnen worden toegepast.<!-- MAGECLOUD-1186 -->

- We hebben een probleem opgelost dat ervoor zorgde dat er uitzonderingen werden gegenereerd wanneer de compilatie van de injectie van afhankelijkheid (di) tijdens builds wordt overgeslagen.<!-- MAGECLOUD-1047 & MAGECLOUD-1049 -->

- We hebben een probleem opgelost waardoor het implementatieproces aangepaste Redis-configuraties in het dialoogvenster `env.php` bestand.<!-- MAGECLOUD-1019 -->

- We hebben een probleem opgelost dat zorgt voor omleiding als gevolg van een uitgeschakelde functie voor veilig beheer.<!-- MAGECLOUD-1020 -->

## v2002.0.0

>[!WARNING]
>
>Dit pakket is niet meer compatibel met andere versies van Adobe Commerce op cloudinfrastructuur en **mogen niet** worden gebruikt.

### Eerste release

Eerste release van `ece-tools` voor Adobe Commerce op cloudinfrastructuur 2.2.0.
