---
title: Omgeving configureren
description: Leer hoe te om bouwstijl te vormen en acties over alle Handel op de milieu's van de wolkeninfrastructuur, met inbegrip van Pro het Staging en Productie op te stellen, gebruikend omgevingsvariabelen.
feature: Cloud, Build, Configuration, Deploy, SCD
role: Developer
exl-id: 66e257e2-1eca-4af5-9b56-01348341400b
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# Omgevingsvariabelen voor implementatie configureren

De `.magento.env.yaml` het dossier gebruikt omgevingsvariabelen om het beheer van bouwstijl te centraliseren en acties over al uw milieu&#39;s, met inbegrip van Pro het Staging en Productie op te stellen. Om unieke acties in elke milieu te vormen, moet u dit dossier in elke milieu wijzigen.

>[!TIP]
>
>YAML-bestanden zijn hoofdlettergevoelig en staan geen tabs toe. Wees voorzichtig met het gebruik van consistente inspringing in de gehele `.magento.env.yaml` of uw configuratie werkt mogelijk niet zoals verwacht. De voorbeelden in de documentatie en in het voorbeeldbestand gebruiken _met twee spaties_ inspringing. Gebruik de [ece-tools validate, opdracht](#validate-configuration-file) om uw configuratie te controleren.

## Bestandsstructuur

De `.magento.env.yaml` bestand bevat twee secties: `stage` en `log`. De `stage` sectie controleert acties die tijdens de fasen van [Implementatieproces voor cloud](../deploy/process.md).

- `stage`—Gebruik de sectie Werkgebied om bepaalde acties voor de volgende stadia van plaatsing te bepalen:
   - `global`—Controles acties in zowel de bouw, opstellen, en post-opstelt fasen. U kunt deze montages in bouwstijl met voeten treden, opstelt, en post-opstelt secties.
   - `build`—Controls acties in de bouwstijlfase slechts. Als u geen montages in deze sectie specificeert, gebruikt de bouwstijlfase montages van de globale sectie.
   - `deploy`—Controles acties in opstellen slechts fase. Als u geen montages in deze sectie specificeert, de plaatsingsfase gebruikt montages van de globale sectie.
   - `post-deploy`—Besturingsacties _na_ de implementatie van uw toepassing en _na_ de container begint met het accepteren van verbindingen.
- `log`—Gebruik de logboeksectie om te vormen [meldingen](set-up-notifications.md), met inbegrip van de soorten meldingen en de mate van gedetailleerdheid.
   - `slack`—Configureer een bericht om naar een Slack bot te verzenden.
   - `email`—Configureer een e-mailbericht om naar een of meer e-mailontvangers te verzenden.
   - [loghandlers](log-handlers.md)—Configureer hardware- en softwaretoepassingsberichten die naar een externe logboekserver worden verzonden.

### Omgevingsvariabelen

De `ece-tools` pakket stelt waarden in in de `env.php` bestand op basis van waarden van [Cloud-variabelen](variables-cloud.md), variabelen die zijn ingesteld in het [!DNL Cloud Console]en de `.magento.env.yaml` configuratiebestand. De omgevingsvariabelen in de `.magento.env.yaml` de Cloud-omgeving aanpassen door de bestaande Commerce-configuratie te overschrijven. Als een standaardwaarde is `Not Set`en vervolgens de `ece-tools` pakket neemt **NEE** handeling en gebruikt de [!DNL Commerce] gebrek of de waarde van de configuratie MAGENTO_CLOUD_RELATIONSHIPS. Als de standaardwaarde is ingesteld, wordt `ece-tools` Deze standaardinstelling wordt ingesteld door het pakket.

De volgende onderwerpen bevatten gedetailleerde definities, zoals of een standaardwaarde is ingesteld of niet, van alle variabelen die u kunt gebruiken in het dialoogvenster `.magento.env.yaml` bestand:

- [Algemeen](variables-global.md)—variabelen de controleacties in elke fase: bouw, stel, en post-opstellen op
- [Opbouwen](variables-build.md)—variabelen: besturingselementen voor het samenstellen van handelingen
- [Implementeren](variables-deploy.md)—variabelen besturen implementatiehandelingen
- [Na implementatie](variables-post-deploy.md)—variabelen: besturingsacties na implementatie

### Configuratiebestand maken van CLI

U kunt een `.magento.env.yaml` configuratiebestand voor een Cloud-omgeving met het volgende: `ece-tools` opdrachten.

>Maakt een configuratiebestand

```bash
php ./vendor/bin/ece-tools cloud:config:create `<configuration-json>`
```

>Waarden bijwerken in het configuratiebestand

```bash
php ./vendor/bin/ece-tools cloud:config:update `<configuration-json>`
```

Voor beide opdrachten is één argument vereist: een array in JSON-indeling die een waarde opgeeft voor ten minste één variabele voor build, implementatie of implementatie na implementatie. Met de volgende opdracht stelt u bijvoorbeeld waarden in voor de `SCD_THREADS` en `CLEAN_STATIC_FILES` variabelen:

```bash
php vendor/bin/ece-tools cloud:config:create '{"stage":{"build":{"SCD_THREADS":5}, "deploy":{"CLEAN_STATIC_FILES":false}}}'
```

En maakt een `.magento.env.yaml` bestand met de volgende instellingen:

```yaml
stage:
  build:
    SCD_THREADS: 5
  deploy:
    CLEAN_STATIC_FILES: false
```

U kunt de `cloud:config:update` gebruiken om het nieuwe bestand bij te werken. Met de volgende opdracht wijzigt u bijvoorbeeld de opdracht `SCD_THREADS` en voegt de `SCD_COMPRESSION_TIMEOUT` configuratie:

```bash
php vendor/bin/ece-tools cloud:config:update '{"stage":{"build":{"SCD_THREADS":3, "SCD_COMPRESSION_TIMEOUT":1000}}}'
```

Het bijgewerkte bestand bevat de volgende configuratie:

```yaml
stage:
  build:
    SCD_THREADS: 3
    SCD_COMPRESSION_TIMEOUT: 1000
  deploy:
    CLEAN_STATIC_FILES: false
```

### Configuratiebestand valideren

Gebruik het volgende `ece-tools` bevel om te bevestigen `.magento.env.yaml` configuratiebestand voordat wijzigingen in de externe cloud-omgeving worden doorgevoerd.

```bash
php ./vendor/bin/ece-tools cloud:config:validate
```

De volgende voorbeeldreactie bevat een lijst met te corrigeren items:

```terminal
Environment configuration is not valid. Correct the following items in your .magento.env.yaml file:
The SCD_THREADS variable contains an invalid value of type string. Use the following type: integer.
The SCD_STRATEGY variable contains an invalid value fast. Use one of the available value options: compact, quick, standard.
The NOT_EXIST_OPTION variable is not allowed in configuration.
```

## PHP-constanten

U kunt PHP-constanten gebruiken in `.magento.env.yaml` bestandsdefinities in plaats van waarden voor harde codes. In het volgende voorbeeld wordt het `driver_options` gebruiken van een PHP-constante:

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      connection:
        default:
          driver_options:
            !php/const:\PDO::MYSQL_ATTR_LOCAL_INFILE : 1
        indexer:
          driver_options:
            !php/const:\PDO::MYSQL_ATTR_LOCAL_INFILE : 1
      _merge: true
```

>[!WARNING]
>
>Constante parsering werkt niet wanneer u een `symfony/yaml` pakketversie ouder dan 3.2.

## Foutafhandeling

Wanneer een fout optreedt als gevolg van een onverwachte waarde in het dialoogvenster `.magento.env.yaml` configuratiebestand, ontvangt u een foutbericht. In het volgende foutbericht wordt bijvoorbeeld een lijst met voorgestelde wijzigingen in elk item met een onverwachte waarde weergegeven, waarbij soms geldige opties worden geboden:

```terminal
- Environment configuration is not valid. Please correct .magento.env.yaml file with next suggestions:
  Item CRON_CONSUMERS_RUNNER is not supposed to be in stage build. Please move it to one of possible stages: global, deploy
  Item SKIP_SCD has unexpected type string. Please use one of next types: boolean
  Item VERBOSE_COMMANDS has unexpected type boolean. Please use one of next types: string
  Item SKIP_HTML_MINIFICATION has unexpected type string. Please use one of next types: boolean
  Item CRON_CONSUMERS_RUNNER has unexpected type boolean. Please use one of next types: array
  Item VAR_WARM_UP_PAGES is not allowed in configuration.
  Item WARM_UP_PAGES has unexpected type string. Please use one of next types: array
```

Breng de gewenste correcties aan, wijs deze toe en duw op de wijzigingen. Als u geen foutbericht ontvangt, slagen de wijzigingen in het configuratiebestand voor de validatie.

## Optimalisatie van configuratiebeheer

Als u het Beheer van de Configuratie na het dumpen van de configuraties hebt toegelaten, zou u de variabelen SCD_* van opstellen aan het bouwstijlstadium moeten bewegen. Zie [Statische strategieën voor implementatie van inhoud](../deploy/static-content.md).

>Voor configuratiebeheer:

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

>Na het toelaten van het Beheer van de Configuratie, verplaats de variabelen SCD_* naar het bouwstijlstadium:

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
