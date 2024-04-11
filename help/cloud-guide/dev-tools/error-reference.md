---
title: Foutberichten voor het pakket ECE-Tools
description: Zie een lijst met foutcodes en berichten die tijdens de Adobe Commerce kunnen optreden bij het ontwikkelen, implementeren en implementeren van processen in de cloud-infrastructuur.
recommendations: noDisplay
role: Developer
exl-id: d8cc8d49-32da-43cf-a105-aa56b5334000
source-git-commit: 9dda6fe7f6a9d6064436820a3c8426ec982b5230
workflow-type: tm+mt
source-wordcount: '2763'
ht-degree: 4%

---

# Foutberichten voor ECE-Tools

Deze naslaggids voor foutberichten bevat informatie voor het oplossen van fouten die kunnen optreden tijdens de Adobe Commerce voor het ontwikkelen, implementeren en implementeren van processen in de cloud-infrastructuur.

Alle kritieke en waarschuwingsfoutmeldingen die tijdens de implementatie optreden, worden naar zowel de `var/log/cloud.log` en `/var/log/cloud.error.log` bestanden. Het logbestand van de cloud-fout bevat alleen fouten van de laatste implementatie. Een leeg bestand geeft aan dat de implementatie zonder fouten is gelukt.

In de `cloud.error.log` bestand, wordt elk item geformatteerd als een JSON-tekenreeks, zodat het gemakkelijker kan worden geparseerd:

```json
{"errorCode":1006,"stage":"build","step":"validate-config","suggestion":"No stores/website/locales found in config.php\n  To speed up the deploy process do the following:\n  1. Using SSH, log in to your Magento Cloud account\n  2. Run \"php ./vendor/bin/ece-tools config:dump\"\n  3. Using SCP, copy the app/etc/config.php file to your local repository\n  4. Add, commit, and push your changes to the app/etc/config.php file","title":"The configured state is not ideal","type":"warning"}
```

Foutberichten worden gecategoriseerd door een van de implementatiefasen: maken, implementeren en na implementatie. Elke sectie bevat een lijst met bijbehorende fouten met de volgende informatie voor elke fout:

- **Foutcode**: De door Adobe Commerce toegewezen id voor het foutbericht
- **Werkgebied**: Geeft aan of de fout is opgetreden tijdens het werkgebied voor samenstellen, implementeren of na implementatie
- **Stap**: Geeft de stap in het implementatiescenario aan die de fout kan retourneren. Als de _Stap_ de kolom leeg is, is de fout een algemene fout die door veelvoudige stappen, of tijdens preprocessing verrichtingen kan worden teruggekeerd. Zie [Implementatie op basis van scenario&#39;s](../deploy/scenario-based.md) voor meer informatie over de bouw, opstellen, en post-opstellen stappen.
- **Suggestie**: Biedt richtlijnen voor het oplossen van problemen met de fout
- **Titel (beschrijving van fout)**: Een beschrijving die de oorzaak van de fout samenvat
- **Type**: Geeft aan of de fout een kritieke fout of een waarschuwing is

<!-- Note: The error code tables in this file are auto-generated from source code. To request changes to error code descriptions or suggestions, submit a GitHub issue to the magento/ece-tools repository. -->

## Kritieke fouten

Kritieke fouten wijzen op een probleem met Commerce op de projectconfiguratie van de wolkeninfrastructuur die plaatsingsmislukking veroorzaakt, bijvoorbeeld onjuiste, niet gestaafde, of ontbrekende configuratie voor vereiste montages. Voordat u kunt implementeren, moet u de configuratie bijwerken om deze fouten op te lossen.

### Werkgebied bouwen

| Foutcode | Stap maken | Foutbeschrijving (titel) | Voorgestelde actie |
| - | - | - | - |
| 2 |  | Kan niet schrijven naar de `./app/etc/env.php` file | Implementatiescript kan geen vereiste wijzigingen aanbrengen in het dialoogvenster `/app/etc/env.php` bestand. Controleer de bestandssysteemmachtigingen. |
| 3 |  | Configuratie is niet gedefinieerd in het dialoogvenster `schema.yaml` file | Configuratie is niet gedefinieerd in het dialoogvenster `./vendor/magento/ece-tools/config/schema.yaml` bestand. Controleer of de naam van de configuratievariabele correct en bepaald is. |
| 4 |  | Parseren van `.magento.env.yaml` file | De `./.magento.env.yaml` bestandsindeling is ongeldig. Gebruik een parser YAML om de syntaxis te controleren en om het even welke fouten te bevestigen. |
| 5 |  | Kan de `.magento.env.yaml` file | Kan de `./.magento.env.yaml` bestand. Controleer de bestandsmachtigingen. |
| 6 |  | Kan de `.schema.yaml` file | Kan de `./vendor/magento/ece-tools/config/magento.env.yaml` bestand. Bestandsmachtigingen controleren en opnieuw implementeren (`magento-cloud environment:redeploy`). |
| 7 | verfrissingsmodules | Kan niet schrijven naar de `./app/etc/config.php` file | Het plaatsingsmanuscript kan vereiste veranderingen in het `/app/etc/config.php` bestand. Controleer de bestandssysteemmachtigingen. |
| 8 | validate-config | Kan de `composer.json` file | Kan de `./composer.json` bestand. Controleer de bestandsmachtigingen. |
| 9 | validate-config | De `composer.json` vereist gedeelte voor automatisch laden van bestand ontbreekt | Vereist `autoload` sectie ontbreekt in de `composer.json` bestand. Vergelijk de sectie Automatisch laden met de `composer.json` en voeg de ontbrekende configuratie toe. |
| 10 | validate-config | De `.magento.env.yaml` bestand bevat een optie die niet in het schema is gedeclareerd of een optie die is geconfigureerd met een ongeldige waarde of een ongeldig werkgebied | De `./.magento.env.yaml` bestand bevat ongeldige configuratie. Controleer het foutenlogboek voor gedetailleerde informatie. |
| 11 | verfrissingsmodules | Opdracht is mislukt: `/bin/magento module:enable --all` | Uitvoeren `composer update` lokaal. Dan, verbind en duw bijgewerkt `composer.lock` bestand. Controleer ook de `cloud.log` voor meer informatie . Voor meer gedetailleerde beveloutput, voeg toe `VERBOSE_COMMANDS: '-vvv'` aan de `.magento.env.yaml` bestand. |
| 12 | toepassen-patches | Kan patch niet toepassen |  |
| 13 | set-report-dir-nesting-level | Kan niet schrijven naar het bestand `/pub/errors/local.xml` |  |
| 14 | kopiëren-voorbeeld-gegevens | Kan voorbeeldgegevensbestanden niet kopiëren |  |
| 15 | compile-di | Opdracht is mislukt: `/bin/magento setup:di:compile` | Controleer de `cloud.log` voor meer informatie . Toevoegen `VERBOSE_COMMANDS: '-vvv'` in `.magento.env.yaml` voor meer gedetailleerde beveloutput. |
| 16 | dump-autoload | Opdracht is mislukt: `composer dump-autoload` | De `composer dump-autoload` command failed. Controleer de `cloud.log` voor meer informatie . |
| 17 | renbaan | De uit te voeren opdracht `Baler` voor Javascript-bundeling mislukt | Controleer de `SCD_USE_BALER` omgevingsvariabele om te controleren of de module Baler is geconfigureerd en ingeschakeld voor JS-bundeling. Als u de module Baler niet nodig hebt, stelt u `SCD_USE_BALER: false`. |
| 18 | compress-static-content | Vereist hulpprogramma niet gevonden (timeout, bash) |  |
| 19 | implementatie-statische inhoud | Opdracht `/bin/magento setup:static-content:deploy` mislukt | Controleer de `cloud.log` voor meer informatie . Voor meer gedetailleerde beveloutput, voeg toe `VERBOSE_COMMANDS: '-vvv'` aan de `.magento.env.yaml` bestand. |
| 20 | compress-static-content | Statische inhoudscompressie is mislukt | Controleer de `cloud.log` voor meer informatie . |
| 21 | back-upgegevens: statische inhoud | Kan statische inhoud niet kopiëren naar de `init` directory | Controleer de `cloud.log` voor meer informatie . |
| 22 | back-upgegevens: schrijfbare dirs | Kan sommige beschrijfbare mappen niet kopiëren naar de `init` directory | Kan beschrijfbare mappen niet kopiëren naar de `./init` map. Controleer de bestandssysteemmachtigingen. |
| 23 |  | Kan geen logboekobject maken |  |
| 24 | back-upgegevens: statische inhoud | Kan het bestand niet opschonen `./init/pub/static/` directory | Kan niet opschonen `./init/pub/static` map. Controleer de bestandssysteemmachtigingen. |
| 25 |  | Kan het Composer-pakket niet vinden | Als u de Adobe Commerce-toepassingsversie rechtstreeks van de GitHub-opslagplaats hebt geïnstalleerd, controleert u of de `DEPLOYED_MAGENTO_VERSION_FROM_GIT` omgevingsvariabele is geconfigureerd. |
| 26 | validate-config | Verwijder de configuratie van de module van de Braintree van het Magento die niet meer in Adobe Commerce en Magento Open Source 2.4 en recentere versies wordt gesteund. | Ondersteuning voor de module Braintree is niet meer opgenomen in Magento 2.4.0 en hoger. Verwijder de variabele CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL uit de sectie Variabelen van het dialoogvenster `.magento.app.yaml` bestand. Gebruik in plaats daarvan een officiële extensie van de Commerce Marketplace voor de Braintree van de betalingsondersteuning. |

### Werkgebied implementeren

| Foutcode | Stap implementeren | Foutbeschrijving (titel) | Voorgestelde actie |
| - | - | - | - |
| 101 | vooraf implementeren: cache | Onjuiste cacheconfiguratie (ontbrekende poort of host) | De vereiste parameters ontbreken in de cacheconfiguratie `server` of `port`. Controleer de `cloud.log` voor meer informatie . |
| 102 |  | Kan niet schrijven naar de `./app/etc/env.php` file | Implementatiescript kan geen vereiste wijzigingen aanbrengen in het dialoogvenster `/app/etc/env.php` bestand. Controleer de bestandssysteemmachtigingen. |
| 103 |  | Configuratie is niet gedefinieerd in het dialoogvenster `schema.yaml` file | Configuratie is niet gedefinieerd in het dialoogvenster `./vendor/magento/ece-tools/config/schema.yaml` bestand. Controleer of de naam van de configuratievariabele correct is en of deze is gedefinieerd. |
| 104 |  | Parseren van `.magento.env.yaml` file | Configuratie is niet gedefinieerd in het dialoogvenster `./vendor/magento/ece-tools/config/schema.yaml` bestand. Controleer of de naam van de configuratievariabele correct is en of deze is gedefinieerd. |
| 105 |  | Kan de `.magento.env.yaml` file | Kan de `./.magento.env.yaml` bestand. Controleer de bestandsmachtigingen. |
| 106 |  | Kan de `.schema.yaml` file |  |
| 107 | vooraf implementeren: clean-redis-cache | Kan de Redis-cache niet opschonen | Kan de Redis-cache niet opschonen. Controleer of de cachemonfiguratie van Redis correct is en of de service Redis beschikbaar is. Zie [Redis-service instellen](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/redis.html). |
| 108 | pre-implementatie: set-production-mode | Opdracht `/bin/magento maintenance:enable` mislukt | Controleer de `cloud.log` voor meer informatie . Voor meer gedetailleerde beveloutput, voeg toe `VERBOSE_COMMANDS: '-vvv'` aan de `.magento.env.yaml` bestand. |
| 109 | validate-config | Onjuiste databaseconfiguratie | Controleer of de `DATABASE_CONFIGURATION` omgevingsvariabele is correct geconfigureerd. |
| 110 | validate-config | Onjuiste sessieconfiguratie | Controleer of de `SESSION_CONFIGURATION` omgevingsvariabele is correct geconfigureerd. De configuratie moet ten minste het volgende bevatten `save` parameter. |
| 111 | validate-config | Onjuiste zoekconfiguratie | Controleer of de `SEARCH_CONFIGURATION` omgevingsvariabele is correct geconfigureerd. De configuratie moet ten minste het volgende bevatten `engine` parameter. |
| 112 | validate-config | Onjuiste bronconfiguratie | Controleer of de `RESOURCE_CONFIGURATION` omgevingsvariabele is correct geconfigureerd. De configuratie moet ten minste `connection` parameter. |
| 113 | validate-config:elasticsuite-integriteit | ElasticSuite is geïnstalleerd, maar de service Elasticsearch is niet beschikbaar | Controleer of de `SEARCH_CONFIGURATION` omgevingsvariabele wordt correct geconfigureerd en controleert of de service Elasticsearch beschikbaar is. |
| 114 | validate-config:elasticsuite-integriteit | ElasticSuite is geïnstalleerd, maar er wordt een andere zoekmachine gebruikt | ElasticSuite is geïnstalleerd, maar een andere zoekmachine is geconfigureerd. Werk de `SEARCH_CONFIGURATION` milieu variabele om Elasticsearch toe te laten, en de de dienstconfiguratie van de Elasticsearch in te verifiëren `services.yaml` bestand. |
| 115 |  | Uitvoering van databasequery mislukt |  |
| 116 | install-update: setup | Opdracht `/bin/magento setup:install` mislukt | Controleer de `cloud.log` en `install_upgrade.log` voor meer informatie . Voor meer gedetailleerde beveloutput, voeg toe `VERBOSE_COMMANDS: '-vvv'` aan de `.magento.env.yaml` bestand. |
| 117 | install-update: config-import | Opdracht `app:config:import` mislukt | Controleer de `cloud.log` voor meer informatie . Voor meer gedetailleerde beveloutput, voeg toe `VERBOSE_COMMANDS: '-vvv'` aan de `.magento.env.yaml` bestand. |
| 118 |  | Vereist hulpprogramma niet gevonden (timeout, bash) |  |
| 119 | install-update: implementatie-static-content | Opdracht `/bin/magento setup:static-content:deploy` mislukt | Controleer de `cloud.log` voor meer informatie . Voor meer gedetailleerde beveloutput, voeg toe `VERBOSE_COMMANDS: '-vvv'` aan de `.magento.env.yaml` bestand. |
| 120 | compress-static-content | Statische inhoudscompressie is mislukt | Controleer de `cloud.log` voor meer informatie . |
| 121 | implementeren-statische inhoud:genereren | Kan de geïmplementeerde versie niet bijwerken | Kan de `./pub/static/deployed_version.txt` bestand. Controleer de bestandssysteemmachtigingen. |
| 122 | zuiver-statische inhoud | Kan bestanden met statische inhoud niet opschonen |  |
| 123 | install-update: split-db | Opdracht `/bin/magento setup:db-schema:split` mislukt | Controleer de `cloud.log` voor meer informatie . Voor meer gedetailleerde beveloutput, voeg toe `VERBOSE_COMMANDS: '-vvv'` aan de `.magento.env.yaml` bestand. |
| 124 | onbewerkt | Kan het bestand niet opschonen `var/view_preprocessed` map | Kan de `./var/view_preprocessed` map. Controleer de bestandssysteemmachtigingen. |
| 125 | install-update: reset-password | Kan het bestand niet bijwerken `/var/credentials_email.txt` file | Kan het bestand niet bijwerken `/var/credentials_email.txt` bestand. Controleer de bestandssysteemmachtigingen. |
| 126 | install-update: update | Opdracht `/bin/magento setup:upgrade` mislukt | Controleer de `cloud.log` en `install_upgrade.log` voor meer informatie . Voor meer gedetailleerde beveloutput, voeg toe `VERBOSE_COMMANDS: '-vvv'` aan de `.magento.env.yaml` bestand. |
| 127 | schone cache | Opdracht `/bin/magento cache:flush` mislukt | Controleer de `cloud.log` voor meer informatie . Voor meer gedetailleerde beveloutput, voeg toe `VERBOSE_COMMANDS: '-vvv'` aan de `.magento.env.yaml` bestand. |
| 128 | uit-onderhoud-modus | Opdracht `/bin/magento maintenance:disable` mislukt | Controleer de `cloud.log` voor meer informatie . Toevoegen `VERBOSE_COMMANDS: '-vvv'` in `.magento.env.yaml` voor meer gedetailleerde beveloutput. |
| 129 | install-update: reset-password | Kan de sjabloon voor opnieuw instellen van wachtwoord niet lezen |  |
| 130 | install-update: cache_type | Opdracht is mislukt: `php ./bin/magento cache:enable` | Opdracht `php ./bin/magento cache:enable` wordt alleen uitgevoerd als Adobe Commerce is geïnstalleerd, maar `./app/etc/env.php` bestand was niet aanwezig of leeg aan het begin van de implementatie. Controleer de `cloud.log` voor meer informatie . Toevoegen `VERBOSE_COMMANDS: '-vvv'` in `.magento.env.yaml` voor meer gedetailleerde beveloutput. |
| 131 | installeren-bijwerken | De `crypt/key`  de sleutelwaarde bestaat niet in `./app/etc/env.php` of de `CRYPT_KEY` variabele cloudomgeving | Deze fout treedt op als `./app/etc/env.php` Het bestand is niet aanwezig wanneer de Adobe Commerce-implementatie wordt gestart of als de `crypt/key` waarde is ongedefinieerd. Als u de database uit een andere omgeving hebt gemigreerd, haalt u de waarde van de cryptsleutel uit die omgeving op. Voeg vervolgens de waarde toe aan de [CRYPT_KEY](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html#crypt_key) cloudomgevingsvariabele in uw huidige omgeving. Zie [Adobe Commerce-coderingssleutel](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/overview.html#gather-credentials). Als u per ongeluk de `./app/etc/env.php` bestand, gebruikt u de volgende opdracht om het bestand te herstellen van de back-upbestanden die zijn gemaakt op basis van een vorige implementatie: `./vendor/bin/ece-tools backup:restore` CLI-opdracht.&quot; |
| 132 |  | Kan geen verbinding maken met de service Elasticsearch | Controleren op geldige Elasticsearch en controleren of de service wordt uitgevoerd |
| 137 |  | Kan geen verbinding maken met de OpenSearch-service | Controleren op geldige OpenSearch-referenties en controleren of de service wordt uitgevoerd |
| 133 | validate-config | Verwijder de configuratie van de module van de Braintree van het Magento die niet meer in Adobe Commerce of Magento Open Source 2.4 en recentere versies wordt gesteund. | Ondersteuning voor de module Braintree is niet meer inbegrepen bij Adobe Commerce of Magento Open Source 2.4.0 en hoger. Verwijder de variabele CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL uit de sectie Variabelen van het dialoogvenster `.magento.app.yaml` bestand. Gebruik voor ondersteuning door de Braintree in plaats daarvan een officiële verlenging van de Braintree van de Commerce Marketplace. |
| 134 | validate-config | Adobe Commerce en Magento Open Source 2.4.0 vereisen dat de Elasticsearch-service wordt geïnstalleerd | Elasticsearch-service installeren |
| 138 | validate-config | Adobe Commerce en Magento Open Source 2.4.4 vereisen dat de OpenSearch- of Elasticsearch-service wordt geïnstalleerd | OpenSearch-service installeren |
| 135 | validate-config | De zoekmachine moet op Elasticsearch voor Adobe Commerce en Magento Open Source >= 2.4.0 worden ingesteld | Controleer de variabele SEARCH_CONFIGURATION voor de `engine` -optie. Als het wordt gevormd, verwijder de optie, of plaats de waarde aan &quot;elasticsearch&quot;. |
| 136 | validate-config | Splitste database is verwijderd vanaf Adobe Commerce en Magento Open Source 2.5.0. | Als u gesplitste database gebruikt, moet u terugkeren naar of migreren naar één database of een alternatieve benadering gebruiken. |
| 139 | validate-config | Onjuiste zoekfunctie | Deze Adobe Commerce- of Magento Open Source-versie biedt geen ondersteuning voor OpenSearch. U moet de versies 2.3.7-p3, 2.4.3-p2 of hoger gebruiken |

### Positie na implementatie

| Foutcode | Stap na implementatie | Foutbeschrijving (titel) | Voorgestelde actie |
| - | - | - | - |
| 201 | is-implementatie-mislukt | Werkgebied implementeren is mislukt |  |
| 202 |  | De `./app/etc/env.php` bestand is niet beschrijfbaar | Implementatiescript kan geen vereiste wijzigingen aanbrengen in het dialoogvenster `/app/etc/env.php` bestand. Controleer de bestandssysteemmachtigingen. |
| 203 |  | Configuratie is niet gedefinieerd in het dialoogvenster `schema.yaml` file | Configuratie is niet gedefinieerd in het dialoogvenster `./vendor/magento/ece-tools/config/schema.yaml` bestand. Controleer of de naam van de configuratievariabele correct is en of deze is gedefinieerd. |
| 204 |  | Parseren van `.magento.env.yaml` file | De `./.magento.env.yaml` bestandsindeling is ongeldig. Gebruik een parser YAML om de syntaxis te controleren en om het even welke fouten te bevestigen. |
| 205 |  | Kan de `.magento.env.yaml` file | Controleer de bestandsmachtigingen. |
| 206 |  | Kan de `.schema.yaml` file |  |
| 207 | opwarmen | Voorladen van enkele opwarmpagina&#39;s is mislukt |  |
| 208 | time-to-firs-byte | Kan tijd naar eerste byte (TTFB) niet testen |  |
| 227 | schone cache | Opdracht `/bin/magento cache:flush` mislukt | Controleer de `cloud.log` voor meer informatie . Toevoegen `VERBOSE_COMMANDS: '-vvv'` in `.magento.env.yaml` voor meer gedetailleerde beveloutput. |

### Algemeen

| Foutcode | Algemene stap | Foutbeschrijving (titel) | Voorgestelde actie |
| - | - | - | - |
| 243 |  | Configuratie is niet gedefinieerd in het dialoogvenster `schema.yaml` file | Controleer of de naam van de configuratievariabele correct is en of deze is gedefinieerd. |
| 244 |  | Parseren van `.magento.env.yaml` file | De `./.magento.env.yaml` bestandsindeling is ongeldig. Gebruik een parser YAML om de syntaxis te controleren en om het even welke fouten te bevestigen. |
| 245 |  | Kan de `.magento.env.yaml` file | Kan de `./.magento.env.yaml` bestand. Controleer de bestandsmachtigingen. |
| 246 |  | Kan de `.schema.yaml` file |  |
| 247 |  | Kan geen module voor gebeurtenissen genereren | Controleer de `cloud.log` voor meer informatie . |
| 248 |  | Kan een module voor gebeurtenissen niet inschakelen | Controleer de `cloud.log` voor meer informatie . |
| 249 |  | Kan de module AdobeCommerceWebhoogins niet genereren | Controleer de `cloud.log` voor meer informatie . |
| 250 |  | Kan de module AdobeCommerceWebhoogins niet inschakelen | Controleer de `cloud.log` voor meer informatie . |

## Waarschuwingsfouten

De fouten van de waarschuwing wijzen op een probleem met de Handel op het projectconfiguratie van de wolkeninfrastructuur zoals onjuist, afgekeurd, niet gesteund, of het ontbreken van configuratiemontages voor facultatieve eigenschappen die plaatsverrichting kunnen beïnvloeden. Hoewel een waarschuwing geen plaatsingsmislukking veroorzaakt, zou u waarschuwingsberichten moeten herzien en de configuratie bijwerken om hen op te lossen.

### Werkgebied bouwen

| Foutcode | Stap maken | Foutbeschrijving (titel) | Voorgestelde actie |
| - | - | - | - |
| 1001 | validate-config | Bestand app/etc/config.php bestaat niet |  |
| 1002 | validate-config | De ./build_options.ini-bestand wordt niet meer ondersteund |  |
| 1003 | validate-config | De modulesectie mist van het gedeelde configdossier |  |
| 1004 | validate-config | De configuratie is niet compatibel met deze versie van Magento |  |
| 1005 | validate-config | SCD-opties genegeerd |  |
| 1006 | validate-config | De geconfigureerde status is niet ideaal |  |
| 1007 | renbaan | Baler JS-bundeling kan niet worden gebruikt |  |

### Werkgebied implementeren

| Foutcode | Stap implementeren | Foutbeschrijving (titel) | Voorgestelde actie |
| - | - | - | - |
| 2001 | vooraf implementeren:cache | Het geheime voorgeheugen wordt gevormd voor de dienst Redis die niet beschikbaar is. Configuratie wordt genegeerd. |  |
| 2002 | validate-config | De geconfigureerde status is niet ideaal |  |
| 2003 | validate-config | De geneste niveauwaarde van de folder voor fout het melden is niet gevormd |  |
| 2004 | validate-config | Ongeldige configuratie in de ./pub/errors/local.xml. |  |
| 2005 | validate-config | Beheerdersgegevens worden alleen tijdens de eerste installatie gebruikt om een beheerder te maken. Wijzigingen in de beheergegevens worden tijdens het upgradeproces genegeerd. | Na de eerste installatie kunt u de beheergegevens uit de configuratie verwijderen. |
| 2006 | validate-config | Admin-gebruiker is niet gemaakt omdat e-mail met beheerder niet is ingesteld | Na de installatie kunt u handmatig een beheerder maken: gebruik SSH om verbinding te maken met uw omgeving. Voer vervolgens de `bin/magento admin:user:create` gebruiken. |
| 2007 | validate-config | PHP-versie bijwerken naar aanbevolen versie |  |
| 2008 | validate-config | In Adobe Commerce en Magento Open Source 2.1 is de ondersteuning van zonne-energie afgekeurd. |  |
| 2009 | validate-config | Solr wordt niet meer ondersteund door Adobe Commerce en Magento Open Source 2.2 of hoger. |  |
| 2010 | validate-config | De dienst van de Elasticsearch wordt geïnstalleerd bij infrastructuurlaag, maar het wordt niet gebruikt als onderzoekmachine. | Overweeg de dienst van de Elasticsearch uit de infrastructuurlaag te verwijderen om middelgebruik te optimaliseren. |
| 2011 | validate-config | De de dienstversie van de Elasticsearch op infrastructuurlaag is niet compatibel met huidige versie van elasticsearch/elasticsearch module, die door uw toepassing van Adobe Commerce wordt gebruikt. |  |
| 2012 | validate-config | De huidige configuratie is niet compatibel met deze versie van Adobe Commerce |  |
| 2013 | validate-config | SCD opties genegeerd omdat het plaatsingsproces niet op de bouwstijlfase werd in werking gesteld |  |
| 2014 | validate-config | De configuratie bevat vervangen variabelen of waarden |  |
| 2015 | validate-config | Omgevingsconfiguratie is niet geldig |  |
| 2016 | validate-config | Kan JSON-typeconfiguratie niet decoderen |  |
| 2017 | validate-config | De huidige configuratie is niet compatibel met deze versie van Adobe Commerce |  |
| 2018 | validate-config | Sommige services zijn overgegaan tot EOL |  |
| 2019 | validate-config | De MySQL optie van de onderzoeksconfiguratie is verouderd | Gebruik in plaats hiervan Elasticsearch. |
| 2029 | validate-config | De gesplitste Gegevensbestand werd afgekeurd in Adobe Commerce en Magento Open Source 2.4.2 en zal in 2.5 worden verwijderd. | Als u gesplitste database gebruikt, moet u beginnen met het plannen om terug te keren naar of te migreren naar één database of een alternatieve benadering gebruiken. |
| 2020 | installeren-bijwerken | Adobe Commerce-installatie voltooid, maar de `app/etc/env.php` configuratiebestand ontbreekt of is leeg. | De vereiste gegevens worden teruggezet vanuit omgevingsconfiguraties en vanuit het bestand .magento.env.yaml. |
| 2021 | install-update:db-connection | Voor gesplitste databases die aangepaste verbindingen gebruiken |  |
| 2022 | install-update:db-connection | U bent veranderd in een gegevensbestandconfiguratie die niet compatibel met de slave verbinding is. |  |
| 2023 | install-update:split-db | Het inschakelen van een gesplitste database wordt overgeslagen. |  |
| 2024 | install-update:split-db | De SPLIT_DB-variabele mist de configuratie voor gesplitste verbindingstypen. |  |
| 2025 | install-update:split-db | Verbinding met slave niet ingesteld. |  |
| 2026 | vooraf implementeren:herschrijfbare dirs | Kan sommige gegevens die tijdens de constructiefase zijn gegenereerd, niet terugzetten naar de gekoppelde directory&#39;s | Controleer de `cloud.log` voor meer informatie . |
| 2027 | validate-config:image-mode-variable | Modus value for MAGE_MODE environment variable not supported | Verwijder de MAGE_MODE omgevingsvariabele, of verander zijn waarde in &quot;productie&quot;. Adobe Commerce op cloud-infrastructuur ondersteunt alleen de modus &quot;productie&quot;. |
| 2028 | externe opslag | Externe opslag kan niet worden ingeschakeld. | Verifieer externe opslagreferenties. |
| 2030 | validate-config | Elasticsearch- en OpenSearch-services zijn beide geïnstalleerd op de infrastructuurlaag. Adobe Commerce en Magento Open Source 2.4.4 en hoger gebruiken standaard OpenSearch | U kunt overwegen de Elasticsearch- of OpenSearch-service uit de infrastructuurlaag te verwijderen om het gebruik van bronnen te optimaliseren. |

### Positie na implementatie

| Foutcode | Stap na implementatie | Foutbeschrijving (titel) | Voorgestelde actie |
| - | - | - | - |
| 3001 | validate-config | Foutopsporingsregistratie is ingeschakeld in Adobe Commerce | Als u schijfruimte wilt besparen, moet u foutopsporingslogboekregistratie niet inschakelen voor uw productieomgevingen. |
| 3002 | opwarmen | Kan winkelURL&#39;s niet ophalen |  |
| 3003 | opwarmen | Kan URL van winkel niet ophalen |  |
| 3004 | back-up | Kan geen back-upbestanden maken |  |

### Algemeen

| Foutcode | Algemene stap | Foutbeschrijving (titel) | Voorgestelde actie |
| - | - | - | - |
| 4001 |  | Kan het aantal systeemprocessors niet ophalen: |  |
