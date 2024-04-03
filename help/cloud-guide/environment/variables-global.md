---
title: Algemene variabelen
description: Zie de lijst met omgevingsvariabelen die acties in de Adobe Commerce besturen over het implementatieproces van de cloudinfrastructuur.
feature: Cloud, Configuration, Build, Deploy, Eventing, Logs, SCD
recommendations: noDisplay, catalog
role: Developer
exl-id: 04c2861d-746d-42d4-a678-f6c7b464eb51
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Algemene variabelen

Algemene variabelen beheren acties in elke fase van de [!DNL Commerce] implementatieproces: maken, implementeren en achteraf implementeren. Omdat globale variabelen elke fase beïnvloeden, moet u hen in plaatsen `global` stadium van de `.magento.env.yaml` bestand:

```yaml
stage:
  global:
    GLOBAL_VARIABLE_NAME: value
```

Voor meer informatie over het aanpassen van het bouwstijl en opstellen proces:

- [Implementatieconfiguratie](configure-env-yaml.md)
- [Implementatieproces](../deploy/process.md)

## `ENABLE_EVENTING`

- **Standaard**-_Niet ingesteld_
- **Versie**—Adobe Commerce 2.4.5 en hoger

Wanneer ingesteld op `true`, laat cron toe om berichtrijconsumenten in werking te stellen. Adobe I/O Gebeurtenissen voor Adobe Commerce gebruiken berichtenrijen om de levering van kritieke gebeurtenissen te versnellen.

Adobe raadt u aan ook de [`CRON_CONSUMERS_RUNNER`](./variables-deploy.md#cron_consumers_runner) aan de `deploy` stadium van de `.magento.env.yaml` bestand met `cron_run` instellen op `true`.

Het volgende voorbeeld toont volledig gevormd `ENABLE_EVENTING` variabele.

```yaml
stage:
  global:
    ENABLE_EVENTING: true
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 0
      consumers: []
```

## ENABLE_WEBHOOKS

- **Standaard**-_Niet ingesteld_
- **Versie**—Adobe Commerce 2.4.4 en hoger

Wanneer ingesteld op `true`, schakelt webhooks voor handel in. De webhaak wordt uitgevoerd op een extern eindpunt, zoals een runtimeactie van App Builder of een voorraadbeheersysteem van derden. De [_Handleiding voor webhaken_](https://developer.adobe.com/commerce/extensibility/webhooks) beschrijft deze functie in detail.

```yaml
stage:
  global:
    ENABLE_WEBHOOKS: true
```

## `MIN_LOGGING_LEVEL`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.1.4 en hoger

Overschrijft het minimale registrerenniveau voor alle outputstromen zonder de code te veranderen, die wanneer het oplossen van problemenproblemen met plaatsing helpt. Bijvoorbeeld, als uw plaatsing ontbreekt, kunt u deze variabele gebruiken om de registrerengranulariteit globaal te verhogen. Zie [Logboekniveaus](log-handlers.md#log-levels). De `min_level` waarde in Logging-handlers overschrijft deze instelling.

```yaml
stage:
  global:
    MIN_LOGGING_LEVEL: debug
```

>[!WARNING]
>
>De instelling voor de `MIN_LOGGING_LEVEL` variable verandert niet de configuratie van het logboekniveau voor de dossiermanager, die aan wordt geplaatst `debug` standaard.

## `SCD_ON_DEMAND`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.1.4 en hoger

Het genereren van statische inhoud op verzoek van een gebruiker (SCD) inschakelen. Statische inhoud op aanvraag is ideaal voor de ontwikkelings- en testworkflow, omdat hierdoor de implementatietijd afneemt.

De cache vooraf laden met behulp van de [`post_deploy` haak](../application/hooks-property.md) verlaagt downtime van sites. De opwarming van het geheime voorgeheugen is beschikbaar slechts voor Pro projecten die het Opvoeren en de milieu&#39;s van de Productie in het [!DNL Cloud Console] en voor Starter-projecten. Voeg de `SCD_ON_DEMAND` omgevingsvariabele voor de `global` in de `.magento.env.yaml` bestand:

```yaml
stage:
  global:
    SCD_ON_DEMAND: true
```

De `SCD_ON_DEMAND` de variabele slaat SCD in beide fasen (bouwt en opstelt) over, ontruimt `pub/static` en `var/view_preprocessed` en schrijft het volgende naar de `app/etc/env.php` bestand:

```php?start_inline=1
return array(
   ...
   'static_content_on_demand_in_production' => 1,
   ...
);
```

## `SCD_MAX_EXECUTION_TIME`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.2.0 en hoger

Staat u toe om de maximale verwachte uitvoeringstijd voor statische inhoudsplaatsing te verhogen.

Door gebrek, plaatst Adobe Commerce de maximum verwachte uitvoering aan 900 seconden, maar in sommige scenario&#39;s zou u meer tijd kunnen nodig hebben om de statische inhoudsplaatsing voor een project van de Wolk te voltooien.

```yaml
stage:
  global:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_NO_PARENT`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.4.2 en hoger

Instellen op `true` om het produceren van statische inhoud voor ouderthema&#39;s tijdens de bouw en plaatsingsfasen te verhinderen. Wanneer deze optie is ingesteld op `true`, wordt minder statische inhoud geproduceerd, die uw algemene bouwstijl en plaatsingstijden verbetert.

```yaml
stage:
  global:
    SCD_NO_PARENT: true
```

## `SCD_USE_BALER`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.3.0 en hoger

[Baler](https://github.com/magento/baler) is een module die uw gegenereerde JavaScript-code scant en een geoptimaliseerde JavaScript-bundel maakt. Als u de geoptimaliseerde bundel op uw site implementeert, kan het aantal netwerkaanvragen bij het laden van uw site afnemen en de laadtijden van de pagina verbeteren.

Instellen op `true` om Baler uit te voeren na het uitvoeren van statische inhoudsimplementatie.

```yaml
stage:
  build:
    SCD_USE_BALER: true
```

>[!NOTE]
>
>Installeer en configureer de module Baler voordat u deze functie gebruikt. Aangezien Baler zich in alfaversie bevindt, moet u deze optie alleen inschakelen in testomgevingen.

## `SKIP_HTML_MINIFICATION`

- **Standaard**:
   - `true`—for `ece-tools` 2002.0.13 en hoger
   - `false`—voor eerdere versies van `ece-tools`
- **Versie**—Adobe Commerce 2.1.4 en hoger

Hiermee schakelt u het kopiëren van statische weergavebestanden naar de `<magento_root>/init/` directory aan het einde van het bouwstijlstadium. Indien ingesteld op `true`, worden de bestanden niet gekopieerd en is minificatie van de HTML beschikbaar op verzoek. Deze waarde instellen op `true` om downtime te reduceren bij de implementatie naar omgevingen voor Staging en Productie.

- **`false`**—Kopieert de `view_preprocessed` aan de `<magento_root>/init/` directory aan het eind van de bouwstijlfase, en herstelt de folder in `<magento_root>/var` aan het begin van de implementatiefase.
- **`true`**—Schakelt HTML-minificatie op aanvraag in; doet dit _niet_ kopieer de `<magento_root>var/view_preprocessed` aan de `<magento_root>/init/` directory aan het eind van de bouwstijlfase.

Voeg de `SKIP_HTML_MINIFICATION` omgevingsvariabele voor de `global` in de `.magento.env.yaml` bestand:

```yaml
stage:
  global:
    SKIP_HTML_MINIFICATION: true
```

## `X_FRAME_CONFIGURATION`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.1.4 en hoger

Gebruik de `X_FRAME_CONFIGURATION` variabele om de [`X-Frame-Options`](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/security/xframe-options.html) headerconfiguratie voor je Adobe Commerce-site. Deze configuratie bepaalt hoe de browser een pagina in een `<frame>`, `<iframe>`, of `<object>`. Gebruik een van de volgende opties:

- `DENY`—Pagina kan niet in een kader worden weergegeven.
- `SAMEORIGIN`— (De standaard Adobe Commerce-instelling.) De pagina kan alleen worden weergegeven in een kader dat zich op dezelfde oorsprong bevindt als de pagina zelf.

>[!WARNING]
>
>De `ALLOW-FROM <uri>` Deze optie is vervangen omdat de door Adobe Commerce ondersteunde browsers deze niet meer ondersteunen. Zie [Browsercompatibiliteit](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options#Browser_compatibility).

Voeg de `X_FRAME_CONFIGURATION` omgevingsvariabele voor de `global` in de `.magento.env.yaml` bestand:

```yaml
stage:
  global:
    X_FRAME_CONFIGURATION: SAMEORIGIN
```
