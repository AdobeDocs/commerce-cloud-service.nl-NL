---
title: Achteruit incompatibele wijzigingen
description: Leer meer over achterwaartse verenigbaarheid wanneer het bevorderen van bestaande projecten van de Wolk.
feature: Cloud, Release Notes
recommendations: noDisplay, catalog
exl-id: 9847c565-6d59-429a-9593-c2eba5cf2da4
source-git-commit: f9edcc85c14354a2eddacbc5219557e107a367cb
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 0%

---

# Achteruit incompatibele wijzigingen

Voor wijzigingen die niet compatibel zijn met oudere versies, moet u mogelijk de configuratie en processen van de cloud aanpassen voor bestaande Cloud-projecten wanneer u een upgrade uitvoert naar de meest recente versie van het dialoogvenster `ece-tools` pakket of andere Cloud Tools Suite voor handelspakketten.

## Wijzigingen in `ece-tools` package

Enkele functionaliteit die eerder in de `ece-tools` de verpakking wordt nu in afzonderlijke pakketten geleverd . Deze pakketten zijn composerafhankelijkheden voor `ece-tools`, die automatisch worden geïnstalleerd en bijgewerkt wanneer u hulpprogramma&#39;s installeert of bijwerkt.

De nieuwe architectuur zou uw installatie of updateprocessen niet moeten beïnvloeden. Het kan echter zijn dat u bepaalde syntaxis en processen voor opdrachten moet wijzigen wanneer u met uw Adobe Commerce werkt aan een infrastructuurproject voor de cloud. Voor meer informatie raadpleegt u de volgende, incompatibele gegevens over de wijzigingen en de [Opmerkingen bij de release Cloud Tools Suite](cloud-tools-suite.md).

### Wijzigingen in de vereisten voor serviceversie

We hebben de minimale PHP versie vereiste gewijzigd van 7.0.x in 7.1.x voor Cloud-projecten die `ece-tools` versie 2002.1.0 en hoger. Als uw omgevingsconfiguratie PHP 7.0 opgeeft, werkt u de [php-configuratie](../application/php-settings.md) in de `.magento.app.yaml` bestand.

>[!WARNING]
>
>Vanwege de wijziging van de PHP-versie, `ece-tools` 2002.1.0 biedt alleen ondersteuning voor Adobe Commerce voor cloud-infrastructuurprojecten met Adobe Commerce 2.1.15 of hoger. Als uw project een vroegere versie gebruikt, moet u [upgrade](../development/commerce-version.md) voordat u een update uitvoert naar `ece-tools` 2002.1.0.

### Wijzigingen in de configuratie van omgeving

De volgende lijst verstrekt informatie over omgevingsvariabelen en andere dossiers van de omgevingsconfiguratie die werden verwijderd of verouderd in `ece-tools` v2002.1.0.

| Item | Vervanging |
| -------- | ----------- |
| `SCD_EXCLUDE_THEMES` variabel | [`SCD_MATRIX`](../environment/variables-build.md#scd_matrix) |
| `STATIC_CONTENT_THREADS` variabel | [`SCD_THREADS`](../environment/variables-build.md#scd_threads) |
| `DO_DEPLOY_STATIC_CONTENT` variabel | [`SKIP_SCD`](../environment/variables-build.md#skip_scd) |
| `STATIC_CONTENT_SYMLINK` variabel | Geen. De build maakt nu altijd een koppeling naar de map met statische inhoud `pub/static`. |
| `build_options.ini` file | Gebruik de [`.magento.env.yaml`](../application/configure-app-yaml.md) bestand voor het configureren van omgevingsvariabelen voor het beheren van ontwikkelings- en implementatieacties in al uw omgevingen.<p>Als u een Cloud-omgeving maakt die de `build_options.ini` bestand, mislukt het samenstellen. |

### Wijzigingen in CLI-opdracht

De volgende lijst vat CLI bevelveranderingen in ECE-Tools v2002.1.0 samen die u zouden kunnen vereisen om bevelen of manuscripten bij te werken.

| Opdracht | Vervanging |
|-------- | ----------- |
| `m2-ece-build` | `vendor/bin/ece-tools build` |
| `m2-ece-deploy` | `vendor/bin/ece-tools deploy` |
| `m2-ece-scd-dump` | `vendor/bin/ece-tools config:dump` |
| `vendor/bin/ece-tools patch` | `vendor/bin/ece-patches apply` |
| `vendor/bin/ece-tools docker:build` | `vendor/bin/ece-docker build:compose` |
| `vendor/bin/ece-tools docker:config:convert` | `vendor/bin/ece-docker  image:generate:php` |

In eerdere ECE-Tools-releases kunt u de opdracht `m2-ece-build` en `m2-ece-deploy` bevelen om plaatsingshaken in te vormen `.magento.app.yaml` bestand. Wanneer u een update naar versie 2002.1.0 uitvoert, moet u de opdracht `hooks` in de `.magento.app.yaml` bestand voor de verouderde opdrachten en deze indien nodig vervangen.

## Wijzigingen in cloudpatches

- **Gedownloade patches verwijderen**-De `magento/magento-cloud-patches` pakket bundelt alle patches die beschikbaar zijn via het [softwaredownloads](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/commerce.html) pagina en past deze automatisch toe wanneer u deze implementeert op de cloud. Om flardconflicten na bevordering aan ECE-Tools 2002.1.0 of later te verhinderen, verwijder om het even welke Adobe-geleverde flarden die u aan uw project manueel downloadde en toevoegde.

- **De opdracht Patches toepassen bijwerken**-We hebben de opdracht voor het toepassen van patches verplaatst vanuit de `vendor/bin/ece-tools` aan de `vendor/bin/ece-patches` directory. Gebruik het nieuwe pad als u deze opdracht gebruikt om handmatig patches toe te passen.

  > Patches handmatig toepassen

  ```bash
  php ./vendor/bin/ece-patches apply
  ```

## Wijzigingen in Cloud Docker

- **De minimum PHP versie vereiste is nu PHP 7.1**- Als uw Cloud Docker voor Handel gastheer een vroegere versie in werking stelt, bevorder aan PHP v7.1 of later.

- **Wijzigingen in de opdracht Cloud Docker voor handel**-

   - **Cloud Docker bijwerken voor handelsopdrachten voor Docker-ontwikkelbewerkingen**-We hebben de opdrachten in de Cloud Docker for Commerce verplaatst van de `vendor/bin/ece-tools` aan de `vendor/bin/ece-docker` directory. Werk uw scripts en opdrachten bij om het nieuwe pad te gebruiken.

     Na de upgrade naar `ece-tools` 2002.1.0, gebruik het volgende bevel aan mening beschikbaar `ece-docker` opdrachten.

     ```bash
     php ./vendor/bin/ece-docker list
     ```

   - **Opdrachten voor het bijwerken van de Cloud-docker-compositie**-De naam van het pad is gewijzigd in het opdrachtbestand. `./bin/docker` tot `./bin/magento-docker`. Werk uw scripts en opdrachten bij om het nieuwe pad te gebruiken.

   - **De container voor uitsnijden is niet langer opgenomen in de standaarddocker-configuratie**-Nu moet u de opdracht `--with-cron` aan de `ece-docker build:compose` bevel om de container van het Gewas in de de omgevingsconfiguratie van de Dokker te omvatten. Zie [Snijtaken beheren](https://developer.adobe.com/commerce/cloud-tools/docker/configure/manage-cron-jobs/) in de _Cloud Docker voor handel_ hulplijn.

     Scripts die eerder containers met uitsnijdtaken hebben gegenereerd, zijn nu zonder de uitsnijdcontainer.

   - **Tijdelijke containers gebruiken**- In vorige versies, de containers die door worden gecreeerd `bin/magento-docker` opdrachtbewerkingen zijn niet verwijderd, zodat u ze voor andere bewerkingen kunt gebruiken. Nu, `magento-docker` met opdrachten verwijdert u alle containers die ze maken nadat de opdracht is voltooid.

     Als u een container wilt houden die door een docker-samenstelt verrichting wordt gecreeerd, gebruik `docker-compose run` in plaats van de `bin/magento-docker` gebruiken.

   - **Haken na implementatie uitvoeren**-De `cloud-deploy` voert geen hooks meer uit na implementatie. De nieuwe `cloud-post-deploy` gebruiken om hooks na implementatie uit te voeren nadat u deze hebt geïmplementeerd. Werk uw manuscripten bij om het bevel toe te voegen om haken in werking te stellen post-opstellen.

     ```shell
     bin/magento-docker ece-deploy
     bin/magento-docker ece-post-deploy
     ```

     Als u `docker-compose` opdrachten rechtstreeks uitvoeren `docker-compose run deploy cloud-post-deploy` bevel na het opstellen bevel.

- **De database vernieuwen**- De container van het Gegevensbestand wordt nu opgeslagen in `magento-db` blijvend Docker-volume. Wanneer u de Docker-omgeving vernieuwt, wordt de database niet meer automatisch verwijderd. Indien nodig, gebruik één van de volgende bevelen om het manueel te verwijderen.

   - Verwijder de `magento-db` container:

     ```bash
     docker volume rm magento-db
     ```

   - Alle bijbehorende volumes verwijderen bij het sluiten van de Docker-containers:

     ```bash
     docker-compose down -v
     ```

- **Instellingen voor bestandssynchronisatie negeren voor archiefbestanden en back-upbestanden**-Archief en reservedossiers met de volgende uitbreidingen zijn niet meer gesynchroniseerd wanneer het gebruiken van docker-synch of mutageen: SQL, GZ, ZIP, en BZ2. U kunt de standaardbestandssynchronisatie voor deze bestandstypen negeren door de naam van het bestand te wijzigen zodat het eindigt met een andere extensie. Bijvoorbeeld: `synchronize-me.zip-backup`
