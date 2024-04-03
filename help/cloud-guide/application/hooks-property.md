---
title: Hooks, eigenschap
description: Zie voorbeelden over hoe te om het bezit van haken in te vormen [!DNL Commerce] toepassingsconfiguratiebestand.
feature: Cloud, Configuration, Build, Deploy
exl-id: d9561f09-5129-4b72-978e-2e3873e8efae
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Hooks, eigenschap

Gebruik de `hooks` sectie om shell bevelen tijdens de bouw in werking te stellen, stelt, en post-opstelt fasen in werking:

- **`build`**—Opdrachten uitvoeren _voor_ de toepassing verpakken. De diensten, zoals het gegevensbestand of Redis, zijn niet beschikbaar aangezien de toepassing nog niet is opgesteld. Aangepaste opdrachten toevoegen _voor_ standaard `php ./vendor/bin/ece-tools` bevel zodat de douane-geproduceerde inhoud aan de plaatsingsfase verdergaat.

- **`deploy`**—Opdrachten uitvoeren _na_ verpakken en implementeren van uw toepassing. U kunt tot andere diensten op dit punt toegang hebben. Omdat de standaardwaarde `php ./vendor/bin/ece-tools` de opdracht kopieert de `app/etc` aan de correcte plaats, moet u douanebevelen toevoegen _na_ stelt bevel op om douanebevelen te verhinderen ontbreken.

- **`post_deploy`**—Opdrachten uitvoeren _na_ de implementatie van uw toepassing en _na_ de container begint met het accepteren van verbindingen. De `post_deploy` De haak ontruimt het geheime voorgeheugen en laadt (wratten) het geheime voorgeheugen vooraf. U kunt de lijst met pagina&#39;s aanpassen met de opdracht `WARM_UP_PAGES` in de [Positie na implementatie](../environment/variables-post-deploy.md). Hoewel dit niet vereist is, werkt dit in overeenstemming met de `SCD_ON_DEMAND` omgevingsvariabele.

In het volgende voorbeeld wordt de standaardconfiguratie getoond in de `.magento.app.yaml` bestand. CLI-opdrachten toevoegen onder `build`, `deploy`, of `post_deploy` secties _voor_ de `ece-tools` opdracht:

```yaml
hooks:
    # We run build hooks before your application has been packaged.
    build: |
        set -e
        composer install
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    # We run deploy hook after your application has been deployed and started.
    deploy: |
        php ./vendor/bin/ece-tools run scenario/deploy.xml
    # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
    post_deploy: |
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
```

Ook kunt u de bouwstijlfase verder aanpassen door te gebruiken `generate` en `transfer` opdrachten om aanvullende handelingen uit te voeren wanneer u specifiek code maakt of bestanden verplaatst.

```yaml
hooks:
    # We run build hooks before your application has been packaged.
    build: |
        set -e
        php ./vendor/bin/ece-tools build:generate
        # php /path/to/your/script
        php ./vendor/bin/ece-tools build:transfer
```

- `set -e`—veroorzaakt haken om op het eerste ontbroken bevel, in plaats van het definitieve ontbroken bevel te ontbreken.
- `build:generate`—past flarden toe, bevestigt configuratie, produceert DI, en produceert statische inhoud als SCD voor bouwstijlfase wordt toegelaten.
- `build:transfer`—brengt geproduceerde code en statische inhoud naar de definitieve bestemming over.

De opdrachten die vanuit de toepassing worden uitgevoerd (`/app`). U kunt de `cd` gebruiken om de map te wijzigen. De haken mislukken als het definitieve bevel daarin ontbreekt. Om ervoor te zorgen dat ze mislukken bij de eerste mislukte opdracht, voegt u `set -e` aan het begin van de haak.

**Volgorde van bestanden compileren met grijswaarden**:

```yaml
dependencies:
    ruby:
        sass: "3.4.7"
    nodejs:
        grunt-cli: "~0.1.13"

hooks:
    build: |
        cd public/profiles/project_name/themes/custom/theme_name
        npm install
        grunt
        cd
        php ./vendor/bin/ece-tools build
```

Bestanden met meerdere statussen compileren met `grunt` vóór statische inhoudsplaatsing, die tijdens de bouwstijl gebeurt. Plaats de `grunt` vóór de `build` gebruiken.

{{scenarios}}
