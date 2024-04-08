---
title: Cloud Docker-pakket
description: Zie een lijst met de meest recente verbeteringen in het Cloud Docker-pakket.
feature: Cloud, Docker, Release Notes
recommendations: noDisplay, catalog
last-substantial-update: 2024-04-08T00:00:00Z
exl-id: 907d977f-2e9c-4553-a46b-000bc6a57b28
source-git-commit: bc76cba0219f16fd055c20289811b51c35c9b026
workflow-type: tm+mt
source-wordcount: '3662'
ht-degree: 0%

---

# Cloud Docker-pakket

De [`magento/magento-cloud-docker`](https://github.com/magento/magento-cloud-docker) -pakket biedt functionaliteit en Docker-afbeeldingen om Adobe Commerce te implementeren in een lokale Cloud-omgeving. In deze releaseopmerkingen worden de meest recente verbeteringen van dit pakket beschreven. Dit pakket maakt deel uit van [Cloud Tools Suite voor handel](cloud-tools-suite.md).

De `magento/magento-cloud-docker` het pakket gebruikt de volgende versiereeks: `<major>.<minor>.<patch>`

De opmerkingen bij de release omvatten:

- ![nieuw pictogram](../../assets/new.svg) Nieuwe functies
- ![fixepictogram](../../assets/fix.svg) Oplossingen en verbeteringen

<!--Add release notes below-->

## v1.3.7 {#latest}

Releasedatum: 8 april 2024

- ![nieuw pictogram](../../assets/new.svg) **PHP** — Toegevoegde ondersteuning voor PHP 8.3- en PHP 8.3-afbeeldingen.
- ![nieuw pictogram](../../assets/new.svg) **Nginx** — Toegevoegde afbeelding nginx v. 1.24.
- ![nieuw pictogram](../../assets/new.svg) **Openssearch** - Toegevoegde afbeelding OpenSearch v. 2.12, 1.3.
- ![nieuw pictogram](../../assets/new.svg) **Composer** - Bijgewerkte Composer-versie naar 2.2.23.

## v1.3.6

Releasedatum: 31 juli 2023

- ![nieuw pictogram](../../assets/new.svg) **Nieuwe serviceversie toegevoegd**—OpenSearch 2.5.
- ![nieuw pictogram](../../assets/new.svg) **Composer-cache inschakelen**—Nu kunt u de configuratie van het Dok uitbreiden om Composer duidelijke geheime voorgeheugen toe te laten wanneer het beginnen van de container van het Dok. Zie [De Docker-configuratie uitbreiden](https://developer.adobe.com/commerce/cloud-tools/docker/configure/extend-docker-configuration/) in de _Cloud Docker voor handel_ hulplijn.

## v1.3.5

Releasedatum: 10 maart 2023

- ![nieuw pictogram](../../assets/new.svg) **ionCube**—De ionCube-extensie toegevoegd voor de PHP 8.1-afbeelding.
- ![nieuw pictogram](../../assets/new.svg) **Nieuwe serviceversies toegevoegd**—OpenSearch 2.3 en 2.4, PHP 8.2, Varnish 7.1.1.
- ![nieuw pictogram](../../assets/new.svg) **Verbeterde ondersteuning voor PHP 8.2**—Oplossingen voor compatibiliteitsproblemen met bepaalde PHP 8.2.x-versies ter ondersteuning van Commerce 2.4.6.
- ![fixepictogram](../../assets/fix.svg) **Composer-probleem**—Opgeloste problemen die optraden na het bijwerken van de Composer-versie in de Docker-containers.

## v1.3.4

Releasedatum: 27 oktober 2022

- ![nieuw pictogram](../../assets/new.svg) **Nieuwe vernis-afbeeldingen toegevoegd**—Toegevoegde afbeeldingen voor Varnish 6.5, 7.0 en 7.1.<!-- MCLOUD-7879 -->

## v1.3.3

Releasedatum: 13 september 2022

- ![nieuw pictogram](../../assets/new.svg) **Apple M1 (ARM64)-ondersteuning**—Toegevoegde wijzigingen aan Docker-afbeeldingen om ondersteuning voor Apple M1 (ARM64)-architectuur mogelijk te maken.<!-- MCLOUD-7989-2 MCLOUD-7989 -->
- ![fixepictogram](../../assets/fix.svg) **Mailhog**—Oplossing voor een probleem waarbij de mailhog-service e-mailberichten niet afsloot in de modus voor ontwikkelaars.<!-- MCLOUD-8643 -->
- ![fixepictogram](../../assets/fix.svg) **init-docker.sh**—Oplossing voor de validator van de serviceversies in het dialoogvenster `init-docker.sh` script.<!-- MCLOUD-8765 -->

## v1.3.2

Releasedatum: 31 maart 2022

- ![nieuw pictogram](../../assets/new.svg) **Afbeelding met Elasticsearch 7.10 toegevoegd**<!-- MCLOUD-8548 -->

## v1.3.1

Releasedatum: 10 maart 2022

- ![nieuw pictogram](../../assets/new.svg) **Ondersteuning voor PHP 8.1**—Toegevoegde ondersteuning voor PHP 8.1.
- ![nieuw pictogram](../../assets/new.svg) **OpenSearch**—Toegevoegde afbeeldingen van OpenSearch versies 1.1 en 1.2.
- ![nieuw pictogram](../../assets/new.svg) **Composer 2.1**—Stel composer 2.1.x standaard in in PHP 8.x-afbeeldingen.
- ![nieuw pictogram](../../assets/new.svg) **Verbeteringen voor PHP-afbeeldingen**—

   - PHP 8.1-afbeeldingen toegevoegd
   - Bijgewerkte versie xDebug 3.1.2
   - Bijgewerkt xmlrpc 1.0.0RC3

- ![fixepictogram](../../assets/fix.svg) **Verbeteringen voor Elasticsearch en OpenSearch**—Verbeteringen in Elasticsearch- en OpenSearch Dockerfiles; verwijder de Elasticsearch 5.2-afbeelding.
- ![fixepictogram](../../assets/fix.svg) **Natriumextensie**—Enabled `sodium` in alle PHP afbeeldingen.
- ![fixepictogram](../../assets/fix.svg) **Cachevolume van composer**—Vast pad voor Composer-cachevolume dat in de cache geplaatste Composer-pakketten bevat.
- ![fixepictogram](../../assets/fix.svg) **Geheugenbeperking in nginx**—Opgeloste geheugenbeperking in NGINX-afbeelding.

## v1.3.0

Releasedatum: 25 oktober 2021

- ![fixepictogram](../../assets/fix.svg) **Workflow voor de modus Ontwikkelaar verbeteren**—Eerder, moest u de wijze in de bouwstijl specificeren en stappen opstellen. Nu, `--mode` in de `build` stap bepaalt de wijze in de recentere `deploy` stap. Het instellen van de modus na de implementatie is niet meer vereist. Zie [Modus Ontwikkelaar](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html).<!-- ACMP-1086 -->
- ![fixepictogram](../../assets/fix.svg) **Verbeteringen voor alleen-lezen bestandssysteem**—<!-- ACMP-1106 -->
   - Probleem verhelpen met een PHP-container voor e-mailconfiguratie.
   - Kan omgevingsvariabelen gebruiken in INI-bestanden.
   - Zorg ervoor dat voor PHP-ingangspunten geen schrijfmachtiging nodig is.
- ![fixepictogram](../../assets/fix.svg) **Knooppunt bijwerken**—Werk de gebundelde versie van de Knoop bij; wanneer het installeren van Knoop in PHP-CLI beelden, gebruikt het nu de huidige versie LTS.<!-- ACMP-1539 -->
- ![fixepictogram](../../assets/fix.svg) **Symfony bijwerken**—De Symfony config-afhankelijkheden zijn bijgewerkt om compatibel te zijn met Adobe Commerce 2.4.4.<!-- ACMP-1533 -->

## v1.2.4

Releasedatum: 29 juli 2021

- ![nieuw pictogram](../../assets/new.svg) **Nieuw `Zookeeper` container**—Toegevoegd a [Zookeeper container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#zookeeper-container) om de configuratie van de vergrendelingenprovider te beheren voor projecten die niet worden geïmplementeerd op de Adobe Commerce-infrastructuur in de cloud.<!--MCLOUD-8000-->

- ![nieuw pictogram](../../assets/new.svg) **Toegevoegde ondersteuning voor Composer 2.0.**—Toegevoegde Composer versie 2.0 aan het Composer configuratiedossier om verbeteringen van Composer 1.0 te steunen die eind-van-leven nadert.<!--MCLOUD-8003-->

## v1.2.3

Releasedatum: 14 juni 2021

- ![nieuw pictogram](../../assets/new.svg) **PHP 8.0 toegevoegd**—Bijgewerkt PHP naar versie 8.0, waardoor je alle nieuwe functies en optimalisaties kunt benutten die PHP 8.0 bevat.<!--MCLOUD-7941-->
- ![nieuw pictogram](../../assets/new.svg) **Bijgewerkt naar Varnish 6.6 en Elasticsearch 7.11.2**—De volgende koppelingen bevatten releasegegevens over [Varnish Cache 6.6](https://varnish-cache.org/releases/rel6.6.0.html#rel6-6-0) en Elasticsearch 7.11.2.<!--MCLOUD-7921-->
- ![nieuw pictogram](../../assets/new.svg) **Toegevoegd `ioncube` extensie voor PHP 7.4 image**—De `ioncube` De extensie is opnieuw toegevoegd aan de PHP 7.4 afbeelding nadat deze aanvankelijk was uitgesloten van de PHP 7.3 upgrade naar PHP 7.4 upgrade. *[Verzonden door mattskr](https://github.com/magento/magento-cloud-docker/pull/314).*<!--PR #314-->
- ![nieuw pictogram](../../assets/new.svg) **Er is een optie voor bestandssync toegevoegd:`manual-native`**—De `manual-native` de optie voor bestandssynchronisatie biedt handmatige controle over synchronisatie, wat de beste prestaties biedt voor macOS- en Windows-omgevingen. Meer informatie over het gebruik van de `manual-native` optie in [Modus Ontwikkelaar](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html) en [Gegevens synchroniseren in een Docker-ontwikkelomgeving](https://devdocs.magento.com/cloud/docker/docker-syncing-data.html#file-synchronization-options).<!--MCLOUD-7977-->
- ![nieuw pictogram](../../assets/new.svg) **Verwijderen van volume uit `up` en `down` opdrachten**—De `--volume` is verwijderd uit de `bin/magento-docker up` en `bin/magento-docker down` opdrachten, vervangen door de nieuwe `bin/magento-docker init` met een waarschuwing voor gegevensverlies. Door deze wijziging voorkomt u dat gegevens per ongeluk verloren gaan. *[Door joeshelton-wagento ingediend](https://github.com/magento/magento-cloud-docker/pull/319).*<!--PR #319-->
- ![fixepictogram](../../assets/fix.svg) **Bijgewerkt `CN` waarde voor het gegenereerde certificaat**—Verwijderd de hardcoded `CN` waarde uit het Dockerfile. Met deze waarde is een certificaatfout gemaakt (`NET::ERR_CERT_INVALID`) die de `--host` voor de `ece-docker build:compose` te negeren opdracht.<!--MCLOUD-7934-->

## v1.2.2

Releasedatum: 20 april 2021

- ![nieuw pictogram](../../assets/new.svg) **Bijgewerkt `host.docker.internal` onafhankelijk van het platform**—U kunt nu de zelfde Docker creëren stelt manuscripten voor Ubuntu, Vensters, en macOS samen. Het gebruik van Xdebug op Ubuntu vereist niet langer een afzonderlijke omgevingsvariabele. [Fix ingediend door Igor Vitol](https://github.com/magento/magento-cloud-docker/pull/299).<!--Issue #298-->
- ![nieuw pictogram](../../assets/new.svg) **Bijgewerkt in-docker.sh**—Toegevoegd de `mounts` aan `MAGENTO_CLOUD_APPLICATION` omgevingsvariabele. [Fix ingediend door Chiranjeevi](https://github.com/magento/magento-cloud-docker/pull/299).<!--Issue #299-->
- ![nieuw pictogram](../../assets/new.svg) **Bijgewerkt in-docker.sh**—De `init-docker.sh` script met PHP 7.4 en Cloud Docker 1.2.1 versies. [Correctie ingediend door Adarsh Manickam](https://github.com/magento/magento-cloud-docker/pull/300).<!--Issue #300-->
- ![nieuw pictogram](../../assets/new.svg) **Normaal ingeschakeld natrium**—Enabled `sodium` PHP extensie standaard in PHP Docker afbeeldingen.<!--MCLOUD-7548-->
- ![nieuw pictogram](../../assets/new.svg) **`custom-registry`option**—Toegevoegd a `--custom-registry` optie voor `php ./vendor/bin/ece-docker build:compose` gebruiken voor het gebruik van uw eigen afbeeldingsregister.<!--MCLOUD-7476-->

  ```bash
  ./vendor/bin/ece-docker build:compose --custom-registry=my-registry.example.com
  ```

- ![nieuw pictogram](../../assets/new.svg) **Oude versies van Elasticsearch zijn verwijderd**—Verwijderd Elasticsearch versie 1.7 en 2.4 uit de beelden van de Elasticsearch.<!--MCLOUD-7504-->
- ![nieuw pictogram](../../assets/new.svg) **Auto-Generating NGINX-certificaten**—De bestaande certificaten zijn verwijderd uit de NGINX-afbeelding. De NGINX-certificaten worden nu automatisch gegenereerd bij elke nieuwe implementatie voor betere beveiliging.<!--MCLOUD-7396-->
- ![fixepictogram](../../assets/fix.svg) **Ingeschakeld`opcache.validate_timestamps`**—Enabled `opcache.validate_timestamps` PHP-instelling standaard in de ontwikkelaarsmodus. Als u deze instelling inschakelt, is het probleem verholpen waarbij wijzigingen in het bestandssysteem niet werden herkend in Docker.<!--MCLOUD-7466-->
- ![fixepictogram](../../assets/fix.svg) **Vast`build:custom:compose`**—Vast de `build:custom:compose` gebruiken om een fout te genereren wanneer bestanden tijdens het samenstellen niet kunnen worden overschreven. Door een fout te genereren voorkomt u situaties waarin `docker-compose up` kunnen de verkeerde bestanden gebruiken.<!--MCLOUD-7457-->
- ![fixepictogram](../../assets/fix.svg) **Vast `--sync_engine="native"` option**—Oplossing voor het probleem waarbij in de productiemodus (`--mode="production"`), `--sync_engine="native"` maakt geen items voor lokale mappen in de `docker.composer.yml` bestand.<!--MCLOUD-7254-->
- ![fixepictogram](../../assets/fix.svg) **Validatiefouten van versie van vaste service**—Toegevoegde de dienstversies voor [!DNL RabbitMQ], Elasticsearch en andere diensten aan de `type` eigenschap in de `MAGENTO_CLOUD_RELATIONSHIP` variabele. Deze versies toevoegen aan de `relationships` De variabele verhelpt de validatiefouten die tijdens de implementatiefase zijn opgetreden.<!--MCLOUD-7572-->

## v1.2.1

Releasedatum: 21 december 2020

- ![nieuw pictogram](../../assets/new.svg) **NGINX-opdrachtopties**—Opdrachtopties voor samenstellen toegevoegd om het aantal NGINX te wijzigen `worker_processes` en NGINX `worker_connections` voor TLS- en webservices. De `worker_process` parameter behoudt de mogelijkheid om de waarde in te stellen op `auto`. Voorbeelden: <!--MCLOUD-7259-->

  ```terminal
  ./vendor/bin/ece-docker build:compose --nginx-worker-processes=2
  ./vendor/bin/ece-docker build:compose --nginx-worker-connections=2048
  ```

- ![nieuw pictogram](../../assets/new.svg) **Optie voor TLS-opdracht**—Toegevoegde bouwstijlbeveloptie om een configuratie zonder de dienst tot stand te brengen TLS. Voorbeeld: <!--MCLOUD-7259-->

  ```terminal
  ./vendor/bin/ece-docker build:compose --no-tls
  ```

- ![nieuw pictogram](../../assets/new.svg) **NGINX-geheugenverbruik**—Minder geheugen verbruikt door het NGINX-proces voor TLS- en webservices.<!--MCLOUD-7259-->

- ![nieuw pictogram](../../assets/new.svg) **Blackfire**—PHP-extensie voor Uitgeschakelde Blackfire standaard opgenomen in de Cloud Docker-afbeelding.

- ![fixepictogram](../../assets/fix.svg) **PHP-FPM container**—Fixed PHP-FPM container health check by change the `WEB_PORT` van `80` tot `8080`.<!--MCLOUD-7232-->

- ![fixepictogram](../../assets/fix.svg) **Ongeldige volumenaam**—Oplossing voor een fout met ongeldige volumenaam in de modus Ontwikkelaar.<!--MCLOUD-7442-->

- ![fixepictogram](../../assets/fix.svg) **NGINX upstream-poort**—De Docker NGINX 1.19-afbeelding is bijgewerkt en poort 8080 wordt gebruikt om een oneindige lus te voorkomen. [Correctie ingediend door Adarsh Manickam](https://github.com/magento/magento-cloud-docker/pull/296).<!--Issue 295-->

## v1.2.0

Releasedatum: 9 november 2020

- ![nieuw pictogram](../../assets/new.svg) **Containerupdates—**

   - ![nieuw pictogram](../../assets/new.svg) **PHP-FPM container**—Toegevoegde ondersteuning voor de gnupg PHP extensie. [Oplossing ingediend door G Arvind van de Technologie van Zilker](https://github.com/magento/magento-cloud-docker/pull/210).<!--MCLOUD-5981-->

   - ![fixepictogram](../../assets/fix.svg) **Database-container**—Vaste de gezondheidscontrole van de gegevensbestandcontainer door het vereiste gegevensbestandwachtwoord aan het bevel van de gezondheidscontrole toe te voegen.<!--MCLOUD-7122-->

   - ![nieuw pictogram](../../assets/new.svg) **Elasticsearch container**

      - Extra ondersteuning voor Elasticsearch 7.9 voor compatibiliteit met toekomstige Adobe Commerce-releases.<!--MCLOUD-7190-->

      - **Configuratie van Elasticsearch-insteekmodule**—Toegevoegde ondersteuning voor het gebruik van de configuratiegegevens van de Elasticsearch-insteekmodule uit de `services.yaml` bestand om het `docker-compose.yaml` bestand voor een Cloud Docker voor handel. Zie [Elasticsearch-plug-ins](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-plugins).<!--MCLOUD-2789-->

      - **Ondersteuning voor Elasticsearch-insteekmodule**—Toegevoegde ondersteuning voor de volgende Elasticsearch-plug-ins: `analysis-icu`, `analysis-phonetic`, `analysis-stempel`, en `analysis-nori`. De `analysis-icu` en `analysis-phonetic` insteekmodules worden standaard geïnstalleerd. U kunt de `analysis-stempel` en `analysis-nori` naar behoefte.<!--MCLOUD-2789-->

   - ![nieuw pictogram](../../assets/new.svg) **CLI-container**

      - **Opdrachten uitvoeren in PHP-containers voor Docker**—Nu kunt u de Cloud Docker CLI gebruiken om opdrachten uit te voeren in PHP containers in uw Docker-omgeving zonder PHP op de host te hoeven installeren. Bijvoorbeeld, bouwt het volgende bevel de configuratie:  `./bin/magento-docker php 7.3 vendor/bin/ece-docker build:compose`. Zie [Cloud Docker CLI](https://devdocs.magento.com/cloud/docker/docker-quick-reference.html#magento-cloud-docker-cli). [Oplossing ingediend door G Arvind van de Technologie van Zilker](https://github.com/magento/magento-cloud-docker/pull/209).<!--MCLOUD-5982-->

      - OpenSSH-client toegevoegd aan PHP CLI containers. Nu, kunt u ssh-agent gebruiken door:sturen voor Composer als `composer.json` Het bestand bevat persoonlijke git-opslagruimten waarvoor een ssh-client Composer-opdrachten moet gebruiken.<!--MCLOUD-6008-->

   - ![fixepictogram](../../assets/fix.svg) **TLS-container**—Nu, de [TLS-container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#tls-container) is gebaseerd op de `https://hub.docker.com/r/magento/magento-cloud-docker-nginx` Afbeelding dokken in plaats van de CentOS-afbeelding. Deze wijziging verhelpt problemen die fouten veroorzaakten bij het verzenden van HTTPS-aanvragen tussen containers in de Cloud Docker-omgeving.<!--MCLOUD-6469-->

   - ![nieuw pictogram](../../assets/new.svg) **Testcontainer**—Een testcontainer toevoegen voor het testen van de toepassing en de `--with-test` aan de Docker `build:compose` gebruiken om de container alleen te maken tijdens het testen in de Docker-omgeving. Zie [toepassing testen](https://devdocs.magento.com/cloud/docker/docker-test-app-mftf.html).<!--MCLOUD-6394-->

   - ![nieuw pictogram](../../assets/new.svg) **FPM-XDEBUG-container**

      - ![nieuw pictogram](../../assets/new.svg) **Xdebug configureren onder Linux**—Toegevoegd de `--set-docker-host` aan de `ece-docker build:compose` bevel om te vormen `host.docker.internal` waarde in de container Xdebug. Deze optie is vereist als u Xdebug wilt gebruiken op Linux-systemen. Zie [Xdebug configureren voor Docker](https://devdocs.magento.com/cloud/docker/docker-development-debug.html).<!--MCLOUD-6430-->

      - ![fixepictogram](../../assets/fix.svg) Vaste de Xdebug veranderlijke configuratie voor het BINNENTRYPOINT van de Docker om op te lossen `uninitialized "with_xdebug" variable` fouten in de logbestanden. [Fix, ingediend door Florent Olivaud](https://github.com/magento/magento-cloud-docker/pull/218)<!--MCLOUD-6043-->

- ![nieuw pictogram](../../assets/new.svg) **Wijzigingen in de Docker-configuratie**

   - **Configuratie MailHog**—Nu kunt u het volgende gebruiken: `ece-docker build:compose` opdrachtopties om MailHog uit te schakelen en poorten op te geven: `--no-mailhog`, `--mailhog-http-port`, en `--mailhog-smtp-port`. Zie [E-mail instellen](https://devdocs.magento.com/cloud/docker/docker-config.html#set-up-email).<!--MCLOUD-6898, MCLOUD-6660-->

   - Voor Cloud Docker voor Handel 1.2.0 en later, verstrekt de Adobe nu de beelden van de Docker voor elke flardversie, en de de configuratiegenerator van de Dokker leidt tot de configuratie van de Dokker met een gespecificeerde flardversie in plaats van het gebruiken van recentste. Eerder, bouwde de configuratiegenerator van de Docker de configuratie gebruikend de recentste flardversie die Cloud Docker voor de milieu&#39;s van de Handel kon breken die gebruikend een vroegere versie werden gebouwd.<!--MCLOUD-7093-->

   - **Aangepaste afbeeldingen en versies opgeven in aangepaste Cloud Docker-configuratie**—De `build:custom:compose` bevel met opties om douanebeelden en versies te specificeren wanneer het produceren van een douaneDocker stelt configuratiedossier samen (`docker-compose.yaml`). Zie [Een aangepaste Docker Compose-configuratie maken](https://devdocs.magento.com/cloud/docker/docker-config-sources.html#build-a-custom-docker-compose-configuration). <!--MCLOUD-7089-->

   - Bijgewerkt de Docker gastheerconfiguratie om haven 443 bloot te stellen om toegang tot Adobe Commerce toe te laten (`https://magento2.docker`) van alle CLI-containers. U kunt de standaardpoort wijzigen door de `--tls-port` als u het Docker-configuratiebestand genereert.<!--MCLOUD-6806-->

- ![fixepictogram](../../assets/fix.svg) Probleem opgelost waarbij de &#39;Cloud Docker for Commerce&#39;-build failliet ging als de `app/etc/env.php` bestand bestaat.<!--MCLOUD-6732-->

- ![fixepictogram](../../assets/fix.svg) Bijgewerkt de bouwstijlconfiguratie om genoemde volumes met regelmatige volumes te vervangen om kwesties te verhinderen wanneer het opstellen van de Dok van de Wolk voor Handel op Linux of Subsysteem van Vensters voor Linux (WSL2).<!--MCLOUD-6732-->

- ![fixepictogram](../../assets/fix.svg) De functionele tests van Cloud Docker for Commerce zijn bijgewerkt om Composer 2.0 te ondersteunen.<!--MCLOUD-7183-->

## v1.1.2

Releasedatum: 9 september 2020

- ![nieuw pictogram](../../assets/new.svg) Extra ondersteuning voor Elasticsearch 7.7<!--MCLOUD-6219-->

## v1.1.1

Releasedatum: 5 augustus 2020

- ![fixepictogram](../../assets/fix.svg) **Bijgewerkte e-mailconfiguratie**—Bijgewerkt standaardCloud Docker voor de configuratie van de Handel om de dienst te steunen MailHog in plaats van het gebruiken van SendMail. Zie [E-mail instellen](https://devdocs.magento.com/cloud/docker/docker-config.html#set-up-email).<!--MCLOUD-5624-->

- ![fixepictogram](../../assets/fix.svg) De PS-bibliotheek is hersteld naar de omgevingsconfiguratie van Cloud Docker om deze te herstellen `ps:  command not found` fouten.<!--MCLOUD-6621-->

- ![fixepictogram](../../assets/fix.svg) De standaardconfiguratie van Cloud Docker voor handel is bijgewerkt om automatische montage van het ingangspunt van de database en de volumes van MariaDB te verwijderen en te herstellen `Cannot create container for service db` fouten die kunnen optreden bij het starten van de Cloud Docker-omgeving.

  Nu kunt u de Cloud Docker-omgeving configureren om de databasemappen te koppelen door de volgende opties toe te voegen aan de `ece-docker build:compose` opdracht: `--with-entry-point` en `with-mariadb-conf`. Zie [Serviceconfiguratieopties](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-configuration-options).<!--MCLOUD-6424-->

- ![nieuw pictogram](../../assets/new.svg) **CLI-opdrachtupdates**

| Handeling | Opdracht |
| ------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| Voeg een ingangspunt aan de gegevensbestandcontainer toe om het gegevensbestand van steun te herstellen | `./vendor/bin/ece-docker build:compose --db --with-entrypoint` |
| Een MariaDB-configuratievolume toevoegen | `./vendor/bin/ece-docker build:compose --db --mariadb-conf` |

## v1.1.0

Releasedatum: 25 juni 2020

- ![nieuw pictogram](../../assets/new.svg) **Toegevoegde steun voor de gespleten oplossing van gegevensbestandprestaties**—Nu kunt u een opslag vormen en opstellen gebruikend de Gesplitste oplossing van gegevensbestandprestaties in het milieu van de Docker van de Wolk.<!--MCLOUD-3740-->

- ![nieuw pictogram](../../assets/new.svg) **Ondersteuning voor implementatie van Adobe Commerce en Magento Open Source**—Nu kunt u Cloud Docker voor Handel gebruiken om een lokale ontwikkelomgeving te implementeren voor projecten die niet op Adobe Commerce worden gehost op cloudinfrastructuur.<!--MCLOUD-5667-->

- ![nieuw pictogram](../../assets/new.svg) **Blackfire.io-ondersteuning**—Extra ondersteuning voor het gebruik van de [Blackfire.io-extensie](https://devdocs.magento.com/cloud/docker/docker-config-blackfire-io.html) voor geautomatiseerde prestatietests. [Fix ingediend door Adarsh Manickam van Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/202)<!--MCLOUD-5857-->

- ![nieuw pictogram](../../assets/new.svg) **Containerupdates**

   - **Varnish**—Nu is Varnish de standaardcache wanneer u Adobe Commerce implementeert in een Cloud Docker-omgeving met behulp van een ondersteunde versie van de Cloud-toepassingssjabloon. Zie [Varnish container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container).<!--MCLOUD-2634-->

   - De `--no-varnish` optie om de service-installatie van Varnish over te slaan wanneer u het configuratiebestand van Cloud Docker genereert.<!--MCLOUD-2634-->

   - ![nieuw pictogram](../../assets/new.svg) **Database**

      - De ondersteuning voor de MySQL-database is toegevoegd. Nu kunt u de Cloud Docker-omgeving configureren met MariaDB of MySQL. Zie [Serviceconfiguratieopties](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-configuration-options).<!--MCLOUD-5691-->

      - Toegevoegd de capaciteit om de verhogings en compensatiemontages voor gegevensbestandreplicatie te plaatsen wanneer u het Docker samenstelt dossier produceert. Zie [Servicecontainers](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-containers).<!--MCLOUD-5735-->

   - ![nieuw pictogram](../../assets/new.svg) **PHP-FPM**

      - Toegevoegde ondersteuning voor PHP 7.4. [Fix ingediend door Mohanela Murugan van Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/198)<!--MCLOUD-198-->

      - Mogelijkheid toegevoegd om een `php.ini` bestand in de hoofdprojectmap naar de Cloud Docker-omgeving en pas aangepaste PHP-instellingen toe op de PHP-FPM- en CLI-containers. Zie [PHP-instellingen aanpassen](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#customize-php-settings). [Fix ingediend door Mathew Beane van Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/130).<!--MCLOUD-6012-->

      - Er is een containerhealth check toegevoegd. [Oplossing ingediend door Visanth Sampath van Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/188).<!--MCLOUD-5752-->

   - ![fixepictogram](../../assets/fix.svg) **Node.js**—De standaardversie van Node.js van versie 8 tot versie 10 is bijgewerkt om de beveiliging te verbeteren. Node.js versie 8 is afgekeurd en niet meer bijgewerkt met insectenmoeilijke situaties of veiligheidspatches. [Fix ingediend door Mohan Elamurugan van Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/183).<!--MCLOUD-5586-->

   - ![nieuw pictogram](../../assets/new.svg) **Elasticsearch**

      - Extra ondersteuning voor Elasticsearch 6.8, 7.2, 7.5 en 7.6.<!--MCLOUD-4050, MCLOUD-5855,MCLOUD-5860-->

      - De mogelijkheid toegevoegd om de [Configuratie van container Elasticsearch](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) wanneer u het Docker samenstelt configuratiedossier produceert.<!--MCLOUD-3059-->

      - De `--no-es` optie aan de opties van de de dienstconfiguratie om het Docker samen te stellen configuratiedossier te produceren. Gebruik deze optie om de containerinstallatie van de Elasticsearch over te slaan en in plaats daarvan MySQL-zoekopdracht te gebruiken. Deze optie wordt alleen ondersteund voor Adobe Commerce versie 2.3.5 en lager.<!--MCLOUD-3766-->

   - ![nieuw pictogram](../../assets/new.svg) **FPM-XDEBUG-container**—Er is een serviceconfiguratieoptie toegevoegd voor het installeren en configureren van Xdebug voor foutopsporing in PHP in uw Cloud Docker-omgeving. Zie [Xdebug configureren](https://devdocs.magento.com/cloud/docker/docker-development-debug.html).<!--MCLOUD-4098-->

- ![nieuw pictogram](../../assets/new.svg) **Wijzigingen in de Docker-configuratie**

   - Added health checks for the PHP-FPM, Redis, Elasticsearch, and MySQL Docker service containers.<!--MCLOUD-3335 and MCLOUD-5856-->

   - De standaardmodus voor bestandssynchronisatie is gewijzigd in `native` in de modus Ontwikkelaar.<!--MCLOUD-3890 -->

   - Toegevoegde versieinformatie aan het generische beeld van de de dienstcontainer van het Docker wanneer het produceren van `docker-compose.yml` bestand.<!--MCLOUD-3878-->

   - Verbeterde capaciteit om grote reacties van de stroomopwaartse container te behandelen PHP-FPM door te verhogen `fastcgi_buffers` waarde voor de Nginx-server.<!--MCLOUD-5980-->

   - Verbeterde synchronisatieprestaties voor mutagene bestanden door een tweede synchronisatiesessie toe te voegen om bestanden te synchroniseren in de `vendor` directory. Deze wijziging voorkomt dat mutageen vastzit tijdens het synchronisatieproces van het bestand. [Fix ingediend door Mathew Beane van Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/127).<!--MCLOUD-6010-->

   - ![nieuw pictogram](../../assets/new.svg) **CLI-opdrachtupdates**

| Handeling | Opdracht |
| -------- | --------------- |
| Redis-cache wissen | `bin/magento-docker flush-redis` |
| Varnish-cache wissen | `bin/magento-docker flush-varnish` |
| De standaardinstallatie van Varnish overslaan | `.vendor/bin/ece-docker build:compose --no-varnish`<!--MCLOUD-2634--> |
| [Opties voor Elasticsearch aanpassen](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) | `.vendor/bin/ece-docker build:compose --es-env-var`<!--MCLOUD-3059--> |
| [Configuratie van Elasticsearch verwijderen](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) | `.vendor/bin/ece-docker build:compose --no-es`<!--MCLOUD-3766--> |
| DB-container configureren met MySQL versie 5.6 of 5.7 | `./vendor/bin/ece-docker build:compose --db <mysql-version-number> --db-image mysql`<!--MCLOUD-5691--> |
| Aangepaste basis-URL opgeven | `./vendor/bin/ece-docker build:compose --host=<hostname> --port=<port-number>`<!--MCLOUD-3063--> |
| [Container toevoegen voor Xdebug-configuratie](https://devdocs.magento.com/cloud/docker/docker-development-debug.html) | `.vendor/bin/ece-docker build:compose --mode developer --sync-engine native --with-xdebug`<!--MCLOUD-4098--> |

- ![fixepictogram](../../assets/fix.svg) Correctie van de configuratie van de synchronisatie van mutagene bestanden om te voorkomen dat mutagene agentia &#39;stale sessies&#39; creëren. [Fix ingediend door Mathew Beane van Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/127).<!--MCLOUD-6010-->

- ![fixepictogram](../../assets/fix.svg) Oplossing voor een configuratieprobleem dat syntaxisfouten veroorzaakte in het Docker-compositielogboek bij het starten van de PHP-FPM container. [Fix ingediend door Mathew Beane van Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/129)<!--MCLOUD-3958-->

- ![fixepictogram](../../assets/fix.svg) Fouten met volumeconflicten die soms optraden bij het gebruik van meerdere Docker-omgevingen, zijn opgelost. [Oplossing ingediend door G Arvind van de Technologie van Zilker](https://github.com/magento/magento-cloud-docker/pull/168).

- ![fixepictogram](../../assets/fix.svg) Het probleem dat de oorzaak was van de `ece-docker build:compose` bevel om te ontbreken als de configuratie Blackfire.io omvatte. [Oplossing ingediend door G Arvind van de Technologie van Zilker](https://github.com/magento/magento-cloud-docker/pull/199). <!--MCLOUD-5797-->

- ![fixepictogram](../../assets/fix.svg) De PHP CLI-afbeeldingsconfiguratie is bijgewerkt om fouten met onvoldoende geheugen te voorkomen die optraden bij de installatie van meerdere pakketten met gebruik van Cloud Docker for Commerce. [Fix ingediend door Mohan Elamurugan van Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/197).*<!--MCLOUD-5818-->

- ![fixepictogram](../../assets/fix.svg) Extra ondersteuning voor meerdere MySQL-gebruikers in de Cloud Docker-omgeving. In eerdere versies worden de `build:compose` bewerking is mislukt als de `magento.app.yaml` bestand heeft meerdere databasegebruikers opgegeven. [Oplossing ingediend door G Arvind van de Technologie van Zilker](https://github.com/magento/magento-cloud-docker/pull/181).<!--MCLOUD-5670-->

- ![fixepictogram](../../assets/fix.svg) Verwijderd `rsyslog` in de Cloud Docker for Commerce PHP-containers om compatibiliteitsproblemen op te lossen die tijdens de implementatie waarschuwingsmeldingen hebben veroorzaakt. Cloud Docker gebruikt het hulpprogramma rsyslog niet.<!--MCLOUD-6173-->

## v1.0.0

Releasedatum: 5 februari 2020

- ![nieuw pictogram](../../assets/new.svg) **Een afzonderlijk pakket gemaakt voor levering`Cloud Docker for Commerce`**—Verplaatst de broncode om Cloud Docker voor Handel van te leveren `ece-tools` aan de [new `magento-cloud-docker` opslagplaats](https://github.com/magento/magento-cloud-docker) om de kwaliteit van de code te handhaven en onafhankelijke versies te verstrekken. Het nieuwe pakket is afhankelijk van ECE-Tools v2002.1.0 en hoger.

  Wanneer u de gereedschappen voor gereedschappen bijwerkt, werkt u ook de `magento/magento-cloud-docker` pakket naar versie 1.0.0. Als u Cloud Docker hebt gebruikt voor handel met een eerdere `ece-tools` release (2002.0.x), bekijk de [achterwaartse onverenigbaarheden](backward-incompatible-changes.md) en werk uw project bij als manuscripten, bevelen, en processen zoals nodig.

- ![nieuw pictogram](../../assets/new.svg) **Versie toegevoegd aan de Docker-afbeeldingen**—U moet nu de `magento/magento-cloud-docker` om de bijgewerkte afbeeldingen op te halen.<!--MAGECLOUD-4737-->

- ![nieuw pictogram](../../assets/new.svg) **Containerupdates**—

   - ![nieuw pictogram](../../assets/new.svg) **PHP-FPM container**—

      - ![nieuw pictogram](../../assets/new.svg) **Extra ondersteuning voor Node.js**—De PHP-FPM afbeelding is bijgewerkt om node-, npm- en grijpclipmogelijkheden in de PHP container te ondersteunen.<!--MAGECLOUD-3953-->

      - ![nieuw pictogram](../../assets/new.svg) **Extra ondersteuning voor [ionCube](https://www.ioncube.com/)**—Bijgewerkt de standaardconfiguratie van de Dokker om ionCube in de lokale ontwikkelomgeving van de Docker te steunen.<!--MAGECLOUD-4354-->

   - ![nieuw pictogram](../../assets/new.svg) **Webcontainer**—

      - ![nieuw pictogram](../../assets/new.svg) **NGINX-configuratie aanpassen**—Toegevoegd de capaciteit om een douane op te zetten `nginx.conf` bestand naar de Cloud Docker for Commerce-omgeving. Zie [Webcontainer](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#web-container).<!--MAGECLOUD-4204-->

      - ![nieuw pictogram](../../assets/new.svg) **Automatisch gegenereerde NGINX-certificaten**—Het de configuratiedossier van de Docker omvat nu de configuratie om NGINX certificaten voor de container van het Web auto-te produceren.<!--MAGECLOUD-4258-->

   - ![nieuw pictogram](../../assets/new.svg) **Nieuwe Selenium-container**—Toegevoegd a [Seleniumcontainer](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#selenium-container) ondersteunen van het testen van Adobe Commerce-toepassingen met behulp van het Magento Functional Testing Framework (MFTF).<!--MAGECLOUD-4040-->

   - ![nieuw pictogram](../../assets/new.svg) **[!DNL RabbitMQ]versieondersteuning**—De [!DNL RabbitMQ] containerconfiguratie die wordt ondersteund [!DNL RabbitMQ] versie 3.8.<!--MAGECLOUD-4674-->

   - ![fixepictogram](../../assets/fix.svg) **Blijvende databasecontainer**—De `magento-db: /var/lib/mysql` het databasevolume blijft nu bestaan nadat u de Docker-configuratie hebt gestopt en verwijderd en wanneer u de Docker-configuratie opnieuw start. Nu moet u het databasevolume handmatig verwijderen. Zie [Databasecontainers].<!--MAGECLOUD-3978-->

   - ![nieuw pictogram](../../assets/new.svg) **TLS-container**—

      - ![nieuw pictogram](../../assets/new.svg) **De basisafbeelding van de container is bijgewerkt en er wordt een officiële afbeelding gebruikt**—De [Cloud TLS-container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#tls-container) het beeld is nu gebaseerd op de officiële `debian:jessie` Afbeelding dokken.—<!--MAGECLOUD-4163-->

      - ![nieuw pictogram](../../assets/new.svg) **Extra ondersteuning voor de [Volgorde voor TLS-beëindiging gevonden]**—De [Pond configuratiebestand](https://github.com/magento/magento-cloud-docker/blob/1.0/images/tls/) voegt de volgende ENV-variabelen toe om de Docker-configuratie voor de TLS-container aan te passen:

         - **`TimeOut`**—Stelt de time-outwaarde voor Tijd in op Eerste byte (TTFB). De standaardwaarde is 300 seconden.

         - **`RewriteLocation`**—Determines whether the Pound proxy rewrites the location to the request URL by default. Standaardwaarden: `0` om te voorkomen dat het herschrijven leidt naar externe websites zoals een externe SSO-site. [Corrigeren door Sorin Sugar](https://github.com/magento/magento-cloud-docker/pull/37)<!--MAGECLOUD-4061-->

      - ![nieuw pictogram](../../assets/new.svg) De time-outwaarde in de TLS-containerconfiguratie is verhoogd van 15 tot 300 seconden. [Fix ingediend door Mathew Beane van Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/78)<!--MAGECLOUD-4460-->

   - ![nieuw pictogram](../../assets/new.svg) **Varnish container**—

      - ![nieuw pictogram](../../assets/new.svg) **De basisafbeelding van de container is bijgewerkt en er wordt een officiële afbeelding gebruikt**—De [Cloud Varnish-container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container) is nu gebaseerd op de officiële `centos` Afbeelding dokken.<!--MAGECLOUD-4163-->

      - ![nieuw pictogram](../../assets/new.svg) **Verbeterde standaardconfiguratie voor time-out**-Toegevoegd `.first_byte_timeout` en `.between_bytes_timeout` configuratie aan de container van Varnish. Beide time-outwaarden zijn standaard ingesteld op `300s` (5 minuten). [Fix ingediend door Mathew Beane van Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/78)<!--MAGECLOUD-4460-->

      - ![fixepictogram](../../assets/fix.svg) **Varnish overslaan tijdens Xdebug-sessies**—Bijgewerkt de de containerconfiguratie van Varnish om terug te keren `pass` op ontvangen aanvragen wanneer Xdebug is ingeschakeld. In vorige versies kon u geen Xdebug gebruiken als Varnish in de Docker-omgeving was opgenomen. [Fix ingediend door Mathew Beane van Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/111).<!--MAGECLOUD-4873-->

- ![nieuw pictogram](../../assets/new.svg) **Wijzigingen in de Docker-configuratie**—

   - ![nieuw pictogram](../../assets/new.svg) **Mappen en volumes beheren voor uw project**—De mogelijkheid toegevoegd om monts en volumes te beheren bij het starten van een dockeromgeving voor lokale ontwikkeling. Zie [Projectgegevens delen].<!--MAGECLOUD-3248-->

   - ![nieuw pictogram](../../assets/new.svg) **Ondersteuning voor de netwerkbrugmodus**—Toegevoegde steun voor de wijze van de netwerkbrug om verbindingen tussen de containers van de Docker over het lokale netwerk toe te laten.<!--MAGECLOUD-4165-->

   - ![nieuw pictogram](../../assets/new.svg) **Container voor uitsnijden standaard uitgeschakeld**—Om prestaties te verbeteren, wordt de container van het Gewas niet meer gevormd door gebrek wanneer u het milieu van de Dokker bouwt. U kunt de `--with-cron` optie op Docker bouwt bevel om een container van het Gewas aan uw milieu toe te voegen. Zie [Snijtaken beheren](https://devdocs.magento.com/cloud/docker/docker-manage-cron-jobs.html).<!--MAGECLOUD-5181-->

   - ![nieuw pictogram](../../assets/new.svg) **Synchroniseren van grote back-upbestanden stoppen**—Toegevoegde DB-dumps en archiefbestanden—ZIP, SQL, GZ en BZ2—aan de uitsluitingslijst in het dialoogvenster `dist/docker-sync.yml` en `dist/mutagen.sh` bestanden. Door het synchroniseren van grote bestanden (>1 GB) kan een periode van inactiviteit ontstaan en voor back-upbestanden is doorgaans geen synchronisatie vereist, omdat u deze opnieuw kunt genereren.<!--MAGECLOUD-3979-->

- ![nieuw pictogram](../../assets/new.svg) **Opdrachtwijzigingen**—

   - ![fixepictogram](../../assets/fix.svg) De naam van de `./bin/docker` bestand naar `./bin/magento-docker` om een probleem op te lossen dat ertoe heeft geleid dat sommige Docker-omgevingen zijn verbroken omdat de `./bin/docker` bestand overschrijft bestaande binaire Docker-bestanden. Dit is een [incompatibele wijziging terugdraaien](backward-incompatible-changes.md) dat updates van uw scripts en opdrachten vereist.<!-- MAGECLOUD-4038 -->

   - ![nieuw pictogram](../../assets/new.svg) **Een optie voor serviceconfiguratie toegevoegd om de databasepoort aan de host beschikbaar te maken**—Gebruik de `--expose-db-port= [Fix submitted by Adarsh Manickam from Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/101).<PORT>` optie om de gegevensbestandhaven aan de gastheer bloot te stellen wanneer het bouwen van `docker-compose.yml` bestand: `bin/ece-docker build:compose --expose-db-port=<PORT>`<!--MAGECLOUD-4454-->

   - ![nieuw pictogram](../../assets/new.svg) **Nieuwe opdracht voor na implementatie**—Eerder de in de `.magento.app.yaml` Het bestand wordt automatisch uitgevoerd nadat u Adobe Commerce via `cloud-deploy` gebruiken. Nu moet u een aparte `cloud-post-deploy` bevel om de haken in werking te stellen post-opstellen nadat u opstelt. Zie de bijgewerkte startinstructies voor [ontwikkelaar](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html) en [productie](https://devdocs.magento.com/cloud/docker/docker-mode-production.html) -modus.<!--MAGECLOUD-3996-->

   - ![nieuw pictogram](../../assets/new.svg) De `--rm` optie voor `./bin/magento-docker` bevelen voor de bouwstijl en stel containers op. Hierdoor wordt de container verwijderd nadat de taak is voltooid.<!--MAGECLOUD-4205-->

   - ![nieuw pictogram](../../assets/new.svg) **Updates voor `build:compose` command**—

      - ![nieuw pictogram](../../assets/new.svg) De `--sync-engine="native"` aan de `docker-build` bevel om dossiersynchronisatie onbruikbaar te maken wanneer u het Docker stelt configuratiedossier in ontwikkelaarwijze produceert. Gebruik deze optie bij het ontwikkelen op Linux-systemen, waarvoor geen bestandssynchronisatie is vereist voor lokale Docker-ontwikkeling. Zie [Gegevens synchroniseren in de Docker-omgeving](https://devdocs.magento.com/cloud/docker/docker-syncing-data.html).<!--MCLOUD-3231, MCLOUD-3890-->

   - ![nieuw pictogram](../../assets/new.svg) De standaardinstelling voor bestandssynchronisatie is gewijzigd van `docker-sync` tot `native`. [Fix ingediend door Mathew Beane van Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/124).<!--MAGECLOUD-5066-->

- ![nieuw pictogram](../../assets/new.svg) **Verbeteringen voor validatie**—

   - ![nieuw pictogram](../../assets/new.svg) Toegevoegde bevestiging aan het plaatsingsproces voor lokale de ontwikkelomgevingen van de Docker om te verifiëren dat de de milieuconfiguratie van de Wolk de encryptiesleutel omvat die wordt vereist om het gegevensbestand te decrypteren. Nu, krijgt u een foutenmelding in het logboek als de omgevingsconfiguratie geen waarde voor de encryptiesleutel specificeert.<!--MAGECLOUD-4423-->

   - ![nieuw pictogram](../../assets/new.svg) Voegt een containergezondheidscontrole aan de dienst van de Elasticsearch toe om ervoor te zorgen dat de dienst klaar is alvorens met bouw voort te gaan en verwerking op te stellen. Als de health check een fout retourneert, wordt de container automatisch opnieuw gestart.<!--MAGECLOUD-4456-->
