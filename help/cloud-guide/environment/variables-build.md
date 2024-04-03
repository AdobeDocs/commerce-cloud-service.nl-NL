---
title: Variabelen samenstellen
description: Zie de lijst met omgevingsvariabelen die acties in de Adobe Commerce besturen over de bouwfase van de cloudinfrastructuur.
feature: Cloud, Configuration, Build, SCD, Upgrade
recommendations: noDisplay, catalog
role: Developer
exl-id: 243aaa45-a5ef-4ed2-8800-3d0f07bf3740
source-git-commit: 7b9c6a4cd17069c25455195bd8f273664b8a29eb
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%

---

# Variabelen samenstellen

Het volgende _build_ variabelen beheren acties in de bouwstijlfase en kunnen waarden van erven en met voeten treden [Algemene variabelen](variables-global.md). Deze variabelen invoegen in het dialoogvenster `build` stadium van de `.magento.env.yaml` bestand:

```yaml
stage:
  build:
    BUILD_VARIABLE_NAME: value
```

Voor meer informatie over het aanpassen van het bouwstijl en opstellen proces:

- [Implementatieconfiguratie](configure-env-yaml.md)
- [Implementatieproces](../deploy/process.md)

De volgende variabelen zijn verwijderd uit v2.2:

- `skip_di_clearing`
- `skip_di_compilation`

## `ERROR_REPORT_DIR_NESTING_LEVEL`

- **Standaard**—`1`
- **Versie**—Adobe Commerce 2.1.4 en hoger

Stel het nestniveau van directory&#39;s in voor het opslaan van foutrapportbestanden om te voorkomen dat de rapportmap wordt gevuld met tienduizenden bestanden, wat het moeilijk kan maken om de gegevens te beheren en te bekijken. Deze instelling is standaard ingesteld op `1`. Doorgaans hoeft u de standaardwaarde niet te wijzigen, tenzij u problemen ondervindt met het beheren van foutrapportbestanden in het dialoogvenster `<magento_root>/var/report/` directory.

```yaml
stage:
  build:
    ERROR_REPORT_DIR_NESTING_LEVEL: 2
```

## `QUALITY_PATCHES`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.1.4 en hoger

Geef een lijst met Adobe Commerce-kwaliteitspatches op die u tijdens de implementatie wilt toepassen.

```yaml
stage:
  build:
    QUALITY_PATCHES: [ ]
```

In het volgende voorbeeld worden drie patches opgegeven die tijdens de implementatie moeten worden toegepast.

```yaml
stage:
  build:
    QUALITY_PATCHES:
      - MC-31387
      - MDVA-4567
      - MC-456345
```

Zie [Patches toepassen](../development/apply-patches.md).

## `SCD_COMPRESSION_LEVEL`

- **Standaard**—`6`
- **Versie**—Adobe Commerce 2.1.4 en hoger

Hiermee wordt opgegeven welke [gzip](https://www.gnu.org/software/gzip) compressieniveau (`0` tot `9`) te gebruiken bij het comprimeren van statische inhoud; `0` Schakelt compressie uit.

```yaml
stage:
  build:
    SCD_COMPRESSION_LEVEL: 4
```

## `SCD_COMPRESSION_TIMEOUT`

- **Standaard**—`600`
- **Versie**—Adobe Commerce 2.1.4 en hoger

Wanneer de tijd die nodig is om de statische elementen te comprimeren, de time-outlimiet voor compressie overschrijdt, wordt het implementatieproces onderbroken. Stel de maximale uitvoeringstijd, in seconden, in voor de opdracht voor het comprimeren van statische inhoud.

```yaml
stage:
  build:
    SCD_COMPRESSION_TIMEOUT: 800
```

## `SCD_NO_PARENT`

- **Standaard**—`false`
- **Versie**—Adobe Commerce 2.4.2 en hoger

Instellen op `true` om het produceren van statische inhoud voor ouderthema&#39;s tijdens de bouwstijlfase te verhinderen.

Set `SCD_NO_PARENT: false` tijdens de bouwstijlfase zodat het produceren van statische inhoud voor de ouderthema&#39;s plaatsplaatsing niet beïnvloedt of onnodige plaatsonderbreking veroorzaakt. Zie [Statische implementatie van inhoud](../deploy/static-content.md).

```yaml
stage:
  build:
    SCD_NO_PARENT: false
```

## `SCD_MATRIX`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.1.4 en hoger

U kunt meerdere landinstellingen per thema configureren. Deze aanpassing helpt het bouwstijlproces te versnellen door het aantal onnodige themadossiers te verminderen. U kunt bijvoorbeeld de _magento/backend_ thema in het Engels en een aangepast thema in andere talen.

In het volgende voorbeeld wordt het `Magento/backend` thema met drie landinstellingen:

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

In het volgende voorbeeld worden drie thema&#39;s met drie landinstellingen samengesteld:

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
      "Magento/blank":
        language:
          - en_US
          - fr_FR
          - af_ZA
      "Magento/luma":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

U kunt ook _niet_ Stel een thema op:

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend": [ ]
```

## `SCD_MAX_EXECUTION_TIME`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.2.0 en hoger

Staat u toe om de maximale verwachte uitvoeringstijd voor statische inhoudsplaatsing te verhogen.

Standaard stelt Adobe Commerce op de cloudinfrastructuur de maximale verwachte uitvoering in op 900 seconden, maar in sommige scenario&#39;s hebt u wellicht meer tijd nodig om de implementatie van statische inhoud voor een Cloud-project te voltooien.

```yaml
stage:
  build:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_STRATEGY`

- **Standaard**—`quick`
- **Versie**—Adobe Commerce 2.2.0 en hoger

De [implementatiestrategie](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-strategy.html) voor statische inhoud. Zie [Statische weergavebestanden gebruiken](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html).

Deze opties gebruiken _alleen_ als u meerdere landinstellingen hebt:

- `standard`—implementeert alle statische weergavebestanden voor alle pakketten.
- `quick`—(_default_) minimaliseert de implementatietijd.
- `compact`—bespaart schijfruimte op de server. In Adobe Commerce versie 2.2.4 en eerder overschrijft deze instelling de waarde voor `scd_threads` met een waarde van `1`.

```yaml
stage:
  build:
    SCD_STRATEGY: "compact"
```

## `SCD_THREADS`

- **Standaard**—Automatisch
- **Versie**—Adobe Commerce 2.1.4 en hoger

Plaatst het aantal draden voor statische inhoudsplaatsing. De standaardwaarde wordt geplaatst gebaseerd op de ontdekte de draadtelling van cpu en overschrijdt geen waarde van 4. Verhoog het aantal draden versnelt de statische plaatsing van inhoud; het verminderen van het aantal draden vertraagt het. U kunt bijvoorbeeld de waarde van de thread instellen:

```yaml
stage:
  build:
    SCD_THREADS: 2
```

Gebruik [Configuratiebeheer](../store/store-settings.md) met de `scd-dump` bevel om statische plaatsing in de bouwstijlfase te bewegen.

## `SCD_USE_BALER`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.3.0 en hoger

[Baler](https://github.com/magento/baler) scant de gegenereerde JavaScript-code en maakt een geoptimaliseerde JavaScript-bundel. Als u de geoptimaliseerde bundel op uw site implementeert, kan het aantal netwerkaanvragen bij het laden van uw site afnemen en de laadtijden van de pagina verbeteren.

Instellen op `true` om Baler uit te voeren na het uitvoeren van statische inhoudsimplementatie.

```yaml
stage:
  build:
    SCD_USE_BALER: true
```

>[!NOTE]
>
>Omdat Baler in alpha- versie is, is het niet raadzaam om het in de milieu&#39;s van de Productie te gebruiken.

## `SKIP_COMPOSER_DUMP_AUTOLOAD`

- **Standaard**— _Niet ingesteld_
- **Versie**—Adobe Commerce 2.1.4 en hoger

Instellen op `true` om de `composer dump-autoload` gebruiken tijdens een installatie van Cloud Docker. Deze variabele is alleen relevant voor Cloud Docker-containers met schrijfbare bestandssystemen. In dergelijke gevallen voorkomt het overslaan van de opdracht fouten van andere opdrachten die toegang proberen te krijgen tot code van de verwijderde `generated` directory.

Wanneer Adobe Commerce wordt uitgevoerd `composer dump-autoload`, worden automatisch bestanden gemaakt met koppelingen naar gegenereerde klassen in het dialoogvenster `generated` -map, wat geen probleem is in productieomgevingen met alleen-lezen bestandssystemen. Voor Cloud Docker-installaties met schrijfbare bestandssystemen (die alleen zijn gemaakt voor testen en ontwikkelen met `./vendor/bin/ece-docker build:compose --with-test`), kunt u de `bin/magento -n setup:upgrade` zonder de `--keep-generated` , waardoor de `generated` directory. Als de map wordt verwijderd, wordt `composer dump-autoload` de opdracht mislukt omdat het automatisch laden koppelingen naar bestanden in de verwijderde map bevat.

```yaml
stage:
  build:
    SKIP_COMPOSER_DUMP_AUTOLOAD: true
```

## `SKIP_SCD`

- **Standaard**— _Niet ingesteld_
- **Versie**—Adobe Commerce 2.1.4 en hoger

Instellen op `true` om statische inhoudsplaatsing tijdens de bouwstijlfase over te slaan.

Als u reeds statische inhoud tijdens bouwstijlfase met opstelt [Configuratiebeheer](../store/store-settings.md), kunt u statische inhoudsplaatsing voor een snelle bouwstijltest overslaan.

Voor de bouwstijlfase, reeks `SKIP_SCD: false` zodat de statische inhoud tijdens de bouwstijlfase wordt opgebouwd waar het proces plaatsplaatsing niet beïnvloedt of onnodige plaatsonderbreking veroorzaakt. Zie [Statische implementatie van inhoud](../deploy/static-content.md).

```yaml
stage:
  build:
    SKIP_SCD: false
```

## `VERBOSE_COMMANDS`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.1.4 en hoger

Schakel de [Symfony](https://symfony.com/doc/current/console/verbosity.html) debug-breedbeeldniveau voor `bin/magento` CLI bevelen die tijdens de plaatsingsfase worden uitgevoerd.

>[!NOTE]
>
>VERBOSE_COMMANDS gebruiken om de details in beveloutput voor zowel succesvol als ontbroken te controleren `bin/magento` CLI-opdrachten, moet u instellen [MIN_LOGGING_LEVEL](variables-global.md#minlogginglevel) `debug`.

Kies het detailniveau in de logboeken:

- `-v`= normale uitvoer
- `-vv`= uitgebreidere uitvoer
- `-vvv` = uitgebreide uitvoer, ideaal voor foutopsporing

```yaml
stage:
  build:
    VERBOSE_COMMANDS: "-vv"
```
