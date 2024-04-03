---
title: Beheer van winkelconfiguratie
description: Leer hoe u de configuratie-instellingen van de winkel in alle Adobe Commerce kunt beheren en synchroniseren in omgevingen met cloudinfrastructuren.
feature: Cloud, Configuration, SCD
exl-id: f2dd876d-24ee-4d47-b9ac-44fcf77b61b5
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 0%

---

# Beheer van winkelconfiguratie

De standaardconfiguraties voor uw opslag worden opgeslagen in een `config.xml` voor de desbetreffende module. Wanneer u montages in Admin van de Handel of CLI verandert `bin/magento config:set` , worden de wijzigingen weerspiegeld in de kerndatabase, met name in de `core_config_data` tabel. Deze instellingen overschrijven de standaardconfiguraties die zijn opgeslagen in het dialoogvenster `config.xml` bestand.

De montages van de opslag die naar de configuraties in Admin verwijzen **Winkels** > **Instellingen** > **Configuratie** sectie, worden opgeslagen in de dossiers van de plaatsingsconfiguratie die op het type van configuratie worden gebaseerd:

- `app/etc/config.php`—configuratiemontages voor opslag, websites, modules of uitbreidingen, statische dossieroptimalisering, en systeemwaarden met betrekking tot statische inhoudsplaatsing. Zie de [config.php reference](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-configphp.html) in de _Configuratiegids_.
- `app/etc/env.php`—waarden voor systeemspecifieke overschrijvingen en gevoelige instellingen die _NOT_ worden opgeslagen in broncontrole. Zie de [env.php reference](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-envphp.html) in de _Configuratiegids_.

>[!NOTE]
>
>Omdat Adobe Commerce op cloudinfrastructuur alleen de productie- en onderhoudsmodi ondersteunt, **Geavanceerd** > **Ontwikkelaar** is niet toegankelijk in de Admin. U moet [rechten voor omgevingbeheerder](../project/user-access.md) om configuratiemanagementtaken te voltooien. U kunt aanvullende instellingen configureren met [omgevingsvariabelen](../environment/configure-env-yaml.md).

Het beheer van de configuratie verstrekt een manier om verenigbare opslagmontages over uw milieu&#39;s met minimale onderbreking op te stellen gebruikend de plaatsing van de Pijpleiding. Adobe Commerce on cloud Infrastructure-project omvat de constructieserver, de build-server, de implementatie van scripts en implementatieomgevingen die zijn ontworpen met de [implementatiestrategie voor pijpleidingen](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/deployment/technical-details.html) in gedachten.

## Configuratieoverschrijvingsschema

Alle systeemconfiguraties worden ingesteld tijdens de bouw- en implementatiefasen volgens het volgende overschrijfschema:

1. Als een omgevingsvariabele bestaat, gebruikt u de aangepaste configuratie en negeert u de standaardconfiguratie.
1. Als een omgevingsvariabele niet bestaat, gebruikt u de configuratie van een `MAGENTO_CLOUD_RELATIONSHIPS` naam-waardepaar in de [`.magento.app.yaml` file](../application/configure-app-yaml.md). De standaardconfiguratie negeren.
1. Indien een omgevingsvariabele niet bestaat en `MAGENTO_CLOUD_RELATIONSHIPS` bevat geen naam-waarde paar, verwijdert alle aangepaste configuratie en gebruikt de waarden uit de standaardconfiguratie.

Samengevat overschrijven omgevingsvariabelen alle andere waarden.

>[!TIP]
>
>Zie [Configuratiebeheer](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/deployment/technical-details.html) in de _Configuratiegids_ voor meer over de opheffingsregeling voor pijpleidingplaatsing.

Als het zelfde plaatsen in veelvoudige plaatsen wordt gevormd, baseert de toepassing zich op de volgende configuratiehiërarchie om te bepalen welke waarde op het milieu van toepassing is:

| Prioriteit | Configuratie<br>Methode | Beschrijving |
| -------- | ------------------------ | ----------- |
| 1 | [!DNL Cloud Console]<br>omgevingsvariabelen | Waarden die zijn toegevoegd via de _Variabelen_ tabblad voor de configuratie van de omgeving in het dialoogvenster [!DNL Cloud Console]. Geef hier waarden op voor gevoelige of omgevingspecifieke configuraties. De hier opgegeven instellingen kunnen niet worden bewerkt via de beheerder. Zie [Omgevingsconfiguratievariabelen](../project/overview.md#configure-environment). |
| 2 | `.magento.app.yaml` | Waarden toegevoegd in het dialoogvenster `variables` van de `.magento.app.yaml` bestand. Geef hier waarden op voor een consistente configuratie in alle omgevingen. **Geef geen gevoelige waarden op in het dialoogvenster `.magento.app.yaml` bestand.** Zie [Toepassingsinstellingen](../application/configure-app-yaml.md). |
| 3 | `app/etc/env.php` | De milieu-specifieke configuratiewaarden die hier worden opgeslagen worden toegevoegd door te gebruiken `app:config:dump` gebruiken. Plaats de systeem-specifieke en gevoelige waarden gebruikend omgevingsvariabelen of CLI. Zie [Gevoelige gegevens](#sensitive-data). De `env.php` bestand is **niet** opgenomen in broncontrole. |
| 4 | `app/etc/config.php` | Waarden die hier zijn opgeslagen, worden toegevoegd met de `app:config:dump` gebruiken. Gedeelde configuratiewaarden worden toegevoegd aan `config.php`. Stel de gedeelde configuratie in via de beheerfunctie of via de CLI. De `config.php` bestand is opgenomen in bronbesturingselement. |
| 5 | Database | De waarden die hier worden opgeslagen, worden toegevoegd door configuraties in te stellen in Admin. Configuraties die zijn ingesteld met een van de voorgaande methoden zijn vergrendeld (grijs weergegeven) en kunnen niet worden bewerkt met de beheerfunctie. |
| 6 | `config.xml` | Veel configuraties hebben standaardwaarden die zijn ingesteld in het dialoogvenster `config.xml` bestand voor een module. Als Adobe Commerce geen waarde kan vinden die door een van de voorgaande methoden is ingesteld, wordt de standaardwaarde (indien ingesteld) geretourneerd. |

{style="table-layout:auto"}

## Configuratiedrukschijf

U kunt het volgende gebruiken `ece-tools` opdracht om een `config.php` bestand dat alle huidige opslagconfiguraties bevat:

```bash
./vendor/bin/ece-tools config:dump
```

De gegevens &quot;gedumpt&quot; op de `app/etc/config.php` bestand wordt _vergrendeld_, wat betekent dat het desbetreffende veld in de Commerce Admin **alleen-lezen**. De `config.php` bevat alleen de instellingen die u configureert. De standaardwaarden worden niet vergrendeld. Door alleen de waarden te vergrendelen die u bijwerkt, zorgt u ervoor dat alle extensies die worden gebruikt in de omgevingen voor Staging en Productie niet worden verbroken door alleen-lezen configuraties, met name snel.

>[!WARNING]
>
>De `ece-tools config:dump` het bevel wint geen gedetailleerde configuraties voor modules, zoals B2B terug. Als u een uitvoerige configuratiedrempel nodig hebt, gebruik `app:config:dump` bevel, maar dit bevel vergrendelt configuratiewaarden in een read-only staat.

### Gevoelige gegevens

Om het even welke gevoelige configuraties uitvoeren naar `app/etc/env.php` bestand wanneer u het `bin/magento app:config:dump` gebruiken. U kunt gevoelige waarden plaatsen gebruikend het CLI bevel: `bin/magento config:sensitive:set`. Zie  [Gevoelige en omgevingsspecifieke instellingen](https://developer.adobe.com/commerce/php/development/configuration/sensitive-environment-settings/) in de _PHP-extensies voor handelsdoeleinden_ gids om te leren hoe te om configuratiemontages als gevoelig of systeem-specifiek aan te wijzen.

Zie een lijst met [Gevoelige of systeemspecifieke instellingen](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/config-reference-sens.html) in de _Configuratiegids_.

### SCD-prestaties

Afhankelijk van de grootte van uw winkel, hebt u mogelijk een groot aantal statische inhoudsbestanden om te implementeren. Normaalgesproken wordt statische inhoud tijdens de implementatiefase geïmplementeerd wanneer de toepassing zich in de onderhoudsmodus bevindt. De meest optimale configuratie moet statische inhoud tijdens de bouwstijlfase produceren. Zie [Een implementatiestrategie kiezen](../deploy/static-content.md).

Als u het Beheer van de Configuratie na het dumpen van de configuraties hebt toegelaten, zou u de variabelen SCD_* van het opstellen stadium aan het bouwstijlstadium moeten bewegen om statische inhoudsgeneratie tijdens de bouwstijlfase behoorlijk toe te laten. Zie [Omgevingsvariabelen](../environment/configure-env-yaml.md#environment-variables).

**Voor configuratiebeheer**:

```yaml
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      consumers: []
    SCD_STRATEGY: compact
    SCD_MATRIX:
      ...
    REDIS_USE_SLAVE_CONNECTION: 1
```

**Na het inschakelen van configuratiebeheer**:

Verplaats de variabelen SCD_* naar het bouwstijlstadium:

```yaml
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      consumers: []
    REDIS_USE_SLAVE_CONNECTION: 1
  build:
    SCD_STRATEGY: compact
    SCD_MATRIX:
      ...
```

>[!NOTE]
>
>Voordat u statische bestanden implementeert, comprimeert de build- en implementatiefase statische inhoud met GZIP. Het comprimeren van statische bestanden verlaagt de serverlading en verbetert de prestaties van de site. Zie [build-opties](../environment/variables-build.md) voor meer informatie over het aanpassen of uitschakelen van bestandscompressie.

## Procedure voor het beheren van uw instellingen

Hieronder ziet u een overzicht op hoog niveau van dit proces:

![Overzicht van Starter-configuratiebeheer](../../assets/starter/configuration-management-flow.png)

**Om uw opslag te vormen en een configuratiedossier te produceren**:

1. Voltooi alle configuraties voor uw winkels in Admin voor een van de omgevingen:

   - Starter: een actieve ontwikkelingstak
   - Pro: Een actieve vertakking in de integratieomgeving

   Deze configuraties omvatten niet de daadwerkelijke producten tenzij u van plan bent om het gegevensbestand van dit milieu aan het Opvoeren en de milieu&#39;s van de Productie te dumpen. Doorgaans bevatten ontwikkelingsdatabases niet uw volledige opslaggegevens.

1. Wijzig op uw lokale werkstation de projectmap.

1. Creeer een lokale stortplaats van het verre gegevensbestand.

   ```bash
   magento-cloud db:dump
   ```

1. Wijzigingen in code toevoegen, toewijzen en doorvoeren om een externe omgeving bij te werken.

   ```bash
   git add app/etc/config.php
   ```

   ```bash
   git commit -m "Add system-specific configuration"
   ```

   ```bash
   git push origin <branch-name>
   ```

Nadat de implementatie is voltooid, meldt u zich aan bij de beheerder voor de bijgewerkte omgeving om de instellingen te controleren. Ga door met het samenvoegen van eventuele aanvullende configuraties in de omgevingen Staging en Productie.

### Configuraties bijwerken

Wanneer u uw omgeving wijzigt via Admin en de opdracht opnieuw uitvoert, worden nieuwe configuraties toegevoegd aan de code in het dialoogvenster `config.php` bestand.

>[!WARNING]
>
>Terwijl u de `config.php` bestand in de omgeving van Staging en Production **niet** aanbevolen. Het bestand helpt alle configuraties in alle omgevingen consistent te houden. De `config.php` bestand om opnieuw samen te stellen. Als u het bestand verwijdert, worden mogelijk specifieke configuraties en instellingen verwijderd die vereist zijn voor het samenstellen en implementeren van processen.

### Configuratiebestanden herstellen

Exemplaren van het origineel `app/etc/env.php` en `app/etc/config.php` bestanden zijn gemaakt tijdens het implementatieproces en opgeslagen in dezelfde map. Hieronder ziet u de BAK (back-upbestanden) en PHP (oorspronkelijke bestanden) in dezelfde `app/etc` map:

```terminal
...
config.php.bak
di.xml
env.php.bak
vendor_path.php
config.php
db_schema.xml
env.php
...
```

Oudere configuraties gebruikt de `app/etc/config.local.php` bestand. Zie [Oudere configuraties migreren](#migrate-older-configurations).

**Configuratiebestanden herstellen**:

1. Voor uw lokale werkstation, gebruik SSH aan login aan het verre project en het milieu.

   ```bash
   magento-cloud ssh
   ```

1. De locatie en beschikbaarheid van de back-upbestanden controleren.

   ```bash
   ./vendor/bin/ece-tools backup:list
   ```

   Monsterrespons:

   ```terminal
   The list of backup files:
   app/etc/env.php
   app/etc/config.php
   ```

1. Back-upbestanden herstellen.

   ```bash
   ./vendor/bin/ece-tools backup:restore
   ```

### Oudere configuraties migreren

Als u een upgrade naar Adobe Commerce uitvoert op cloudinfrastructuur 2.2 of hoger, kunt u de instellingen migreren uit het dialoogvenster `config.local.php` bestand naar uw nieuwe `config.php` bestand. Als de configuratie-instellingen in uw beheerder overeenkomen met de inhoud van het bestand, volgt u de instructies om de `config.php` bestand.

Als deze verschillen, kunt u inhoud toevoegen van de `config.local.php` bestand naar uw nieuwe `config.php` bestand:

1. Volg de instructies om de `config.php` bestand.

1. Open de `config.php` en verwijder de laatste regel.

1. Open de `config.local.php` en kopieert u de inhoud.

1. Plak de inhoud in de `config.php` bestand, opslaan en voltooien en toevoegen aan Git.

1. Implementeer in uw omgeving.

U voltooit deze migratie maar één keer. Gebruik na migratie de `config.php` bestand.

### Landinstellingen wijzigen

U kunt de landinstellingen van uw winkel wijzigen zonder een complex import- en exportproces te volgen. _indien_ u hebt [SCD_ON_DEMAND](../environment/variables-global.md#scd_on_demand) ingeschakeld. U kunt de landinstellingen bijwerken met de beheerfunctie.

U kunt een andere landinstelling toevoegen aan de testomgeving of de productieomgeving door `SCD_ON_DEMAND` in een integratietak, een bijgewerkte versie genereren `config.php` bestand met de nieuwe landinstellingsgegevens en kopieer het configuratiebestand naar de doelomgeving.

>[!WARNING]
>
>Dit proces **overschrijven** de opslagconfiguratie; doe slechts het volgende als de milieu&#39;s de zelfde opslag bevatten.

1. In de integratieomgeving `SCD_ON_DEMAND` variabele die de [`.magento.env.yaml` file](../environment/configure-env-yaml.md).

1. Voeg de vereiste landinstellingen toe met uw beheerder.

1. SSH gebruiken om u aan te melden bij de externe omgeving en om de `/app/etc/config.php` bestand met alle landinstellingen.

   ```bash
   ssh <SSH-URL> "./vendor/bin/ece-tools config:dump"
   ```

1. Kopieer het nieuwe configuratiedossier van de verre integratiemilieu aan uw lokale milieufolder.

   ```bash
   rsync <SSH-URL>:app/etc/config.php ./app/etc/config.php
   ```

1. Wijzigingen in code toevoegen, toewijzen en doorvoeren om een externe omgeving bij te werken.
