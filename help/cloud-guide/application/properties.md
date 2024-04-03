---
title: Eigenschappen
description: Gebruik de eigenschappenlijst als een referentie bij het configureren van de [!DNL Commerce] toepassing voor de bouw en de implementatie in de wolkeninfrastructuur.
feature: Cloud, Configuration, Build, Deploy, Roles/Permissions, Storage
exl-id: 58a86136-a9f9-4519-af27-2f8fa4018038
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# Eigenschappen voor toepassingsconfiguratie

De `.magento.app.yaml` het dossier gebruikt eigenschappen voor het beheer van omgevingssteun voor [!DNL Commerce] toepassing.

| Naam | Beschrijving | Standaard | Vereist |
| ------ | --------------------------------- | ------- | -------- |
| [`access`](#access) | Gebruikersrollen aanpassen | — | Nee |
| [`crons`](crons-property.md) | Specificaties bijwerken en uitsnijdtaken plannen | — | Nee |
| [`dependencies`](#dependencies) | Aanvullende afhankelijkheden inschakelen | `php:composer/composer: '2.2.4'` | Nee |
| [`disk`](#disk) | De grootte van de vaste schijf definiëren | `5120` | Ja |
| [`firewall`](firewall-property.md) | (Alleen Starter) Uitgaand verkeer besturen | — | Nee |
| [`hooks`](hooks-property.md) | Pas shellbevelen voor de bouw, opstellen, en post-opstellen fasen aan | — | Nee |
| [`mounts`](#mounts) | Paden instellen | Paden:<ul><li>`"var": "shared:files/var"`</li><li>`"app/etc": "shared:files/etc"`</li><li>`"pub/media": "shared:files/media"`</li><li>`"pub/static": "shared:files/static"`</li></ul> | Nee |
| [`name`](#name) | De toepassingsnaam definiëren | `mymagento` | Ja |
| [`relationships`](#relationships) | Kaartservices | Services:<ul><li>`database: "mysql:mysql"`</li><li>`redis: "redis:redis"`</li><li>`opensearch: "opensearch:opensearch"`</li></ul> | Nee |
| [`runtime`](#runtime) | De runtime-eigenschap bevat extensies die vereist zijn voor de [!DNL Commerce] toepassing. | Extensies:<ul><li>`xsl`</li><li>`newrelic`</li><li>`sodium`</li></ul> | Ja |
| [`type`](#type-and-build) | De basiscontainerafbeelding instellen | `php:8.1` | Ja |
| [`variables`](variables-property.md) | Pas een omgevingsvariabele toe voor een specifieke versie van de Handel | — | Nee |
| [`web`](web-property.md) | Externe verzoeken afhandelen | — | Ja |
| [`workers`](workers-property.md) | Externe verzoeken afhandelen | — | Ja, als de webeigenschap niet wordt gebruikt |

{style="table-layout:auto"}

## `name`

De `name` eigenschap bevat de toepassingsnaam die in het dialoogvenster [`routes.yaml`](../routes/routes-yaml.md) bestand om de HTTP upstream te definiëren (standaard), `mymagento:http`). Als bijvoorbeeld de waarde van `name` is `app`moet u `app:http` in het upstreamveld.

>[!WARNING]
>
>Wijzig de naam van de toepassing niet nadat deze is geïmplementeerd. Dit leidt tot gegevensverlies.

## `type` en `build`

De `type`  en `build` eigenschappen verstrekken informatie over het beeld van de basiscontainer om het project te bouwen en in werking te stellen.

De ondersteunde `type` taal is PHP. Geef de PHP-versie als volgt op:

```yaml
type: php:<version>
```

De `build` het bezit bepaalt wat door gebrek gebeurt wanneer het bouwen van het project. De `flavor` geeft een standaardset bouwtaken aan die moet worden uitgevoerd. Het volgende voorbeeld toont de standaardconfiguratie voor `type` en `build` van `magento-cloud/.magento.app.yaml`:

```yaml
# The toolstack used to build the application.
type: php:8.1
build:
    flavor: none

dependencies:
    php:
        composer/composer: '2.2.4'
```

### Composer 2 installeren en gebruiken

De `build: flavor:` Deze eigenschap wordt niet gebruikt voor Composer 2.x. Daarom moet u Composer handmatig installeren tijdens de constructiefase. Als u Composer 2.x wilt installeren en gebruiken in uw Starter- en Pro-projecten, moet u drie wijzigingen aanbrengen in uw `.magento.app.yaml` configuratie:

1. Verwijderen `composer` als de `build: flavor:` en toevoegen `none`. Door deze wijziging wordt voorkomen dat Cloud de standaardversie 1.x van Composer gebruikt voor het uitvoeren van ontwikkeltaken.
1. Toevoegen `composer/composer: '^2.0'` als `php` afhankelijkheid voor het installeren van Composer 2.x.
1. Voeg de `composer` taken aan een `build` haak om de bouwstijltaken in werking te stellen gebruikend Composer 2.x.

Gebruik de volgende configuratiefragmenten in uw eigen configuratie `.magento.app.yaml` configuratie:

```yaml
# 1. Change flavor to none.
build:
    flavor: none

# 2. Add Composer ^2.0 as a php dependency.
dependencies:
    php:
        composer/composer: '^2.0'

# 3. Add a build hook to run the build tasks using Composer 2.x.
hooks:
    build: |
        set -e
        composer --no-ansi --no-interaction install --no-progress --prefer-dist --optimize-autoloader
```

Zie [Vereiste pakketten](../development/overview.md#required-packages) voor meer informatie over Composer.

## `dependencies`

Specificeer gebiedsdelen die uw toepassing tijdens het bouwstijlproces zou kunnen vereisen.

Adobe Commerce ondersteunt afhankelijkheden voor de volgende talen:

- PHP
- Ruby
- Node.js

Die gebiedsdelen zijn onafhankelijk van de uiteindelijke gebiedsdelen van uw toepassing, en zijn beschikbaar in `PATH`, tijdens het constructieproces en in de runtimeomgeving van uw toepassing.

U kunt die gebiedsdelen als volgt specificeren:

```yaml
ruby:
   sass: "~3.4"
nodejs:
   grunt-cli: "~0.3"
```

## `runtime`

Gebruik deze optie om de PHP-configuratie tijdens runtime te wijzigen, bijvoorbeeld om extensies in te schakelen. De volgende extensies zijn vereist:

```yaml
runtime:
    extensions:
        - xsl
        - newrelic
        - sodium
```

Zie [PHP-instellingen](php-settings.md) voor meer informatie over het inschakelen van extensies.

## `disk`

Definieert de permanente schijfgrootte van de toepassing in MB.

```yaml
disk: 5120
```

De minimale aanbevolen schijfgrootte is 256 MB. Als u de fout ziet `UserError: Error building the project: Disk size may not be smaller than 128MB`, vergroot de grootte tot 256 MB.

>[!NOTE]
>
>Voor Pro Staging- en Productomgevingen moet u [Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om de `mounts` en `disk` configuratie voor uw toepassing. Wanneer u het kaartje indient, wijs op de vereiste configuratieveranderingen en neem een bijgewerkte versie van uw `.magento.app.yaml` bestand.

## `relationships`

Definieert de servicetoewijzing in de toepassing.

De relatie `name` is beschikbaar voor de toepassing in de `MAGENTO_CLOUD_RELATIONSHIPS` omgevingsvariabele. De `<service-name>:<endpoint-name>` relatie wordt toegewezen aan de naam en typewaarden die zijn gedefinieerd in het dialoogvenster `.magento/services.yaml` bestand.

```yaml
relationships:
    <name>: "<service-name>:<endpoint-name>"
```

Hieronder ziet u een voorbeeld van de standaardrelaties:

```yaml
relationships:
    database: "mysql:mysql"
    redis: "redis:redis"
    opensearch: "opensearch:opensearch"
    rabbitmq: "rabbitmq:rabbitmq"
```

Zie [Services](../services/services-yaml.md) voor een volledige lijst van momenteel gesteunde de diensttypes en eindpunten.

## `mounts`

Een object waarvan de sleutels paden zijn die relatief zijn ten opzichte van de hoofdmap van de toepassing. De koppeling is een beschrijfbaar gebied op de schijf voor bestanden. Het volgende is een standaardlijst van steunen die in worden gevormd `magento.app.yaml` bestand gebruiken met de `volume_id[/subpath]` syntaxis:

```yaml
 # The mounts that will be performed when the package is deployed.
mounts:
    "var": "shared:files/var"
    "app/etc": "shared:files/etc"
    "pub/media": "shared:files/media"
    "pub/static": "shared:files/static"
```

De indeling voor het toevoegen van de hoeveelheid aan deze lijst is als volgt:

```bash
"/public/sites/default/files": "shared:files/files"
```

- `shared`—Deelt een volume tussen uw toepassingen binnen een omgeving.
- `disk`—Definieert de beschikbare grootte voor het gedeelde volume.

>[!NOTE]
>
>Voor Pro Staging- en Productomgevingen moet u [Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om de `mounts` en `disk` configuratie voor uw toepassing. Wanneer u het kaartje indient, wijs op de vereiste configuratieveranderingen en neem een bijgewerkte versie van uw `.magento.app.yaml` bestand.

U kunt het montagekweb toegankelijk maken door het aan de [`web`](web-property.md) blok locaties.

>[!WARNING]
>
>Als uw site gegevens bevat, wijzigt u de `subpath` deel van de koppelingsnaam. Deze waarde is de unieke id voor de `files` gebied. Als u deze naam wijzigt, gaan alle sitegegevens verloren die op de oude locatie zijn opgeslagen.

## `access`

De `access` Het bezit wijst op een minimum niveau van de gebruikersrol dat de toegang van SSH tot de milieu&#39;s wordt verleend. De beschikbare gebruikersrollen zijn:

- `admin`—Kan instellingen wijzigen en acties uitvoeren in de omgeving; heeft _contribuant_ en _viewer_ rechten.
- `contributor`—Kan code naar deze omgeving duwen en de omgeving vertakken; heeft _viewer_ rechten.
- `viewer`—Alleen de omgeving kan worden weergegeven.

De standaardgebruikersrol is `contributor`, die de toegang van SSH van gebruikers slechts met beperkt _viewer_ rechten. U kunt de gebruikersrol wijzigen in `viewer` SSH-toegang alleen toestaan voor gebruikers met _viewer_ rechten:

```yaml
access:
    ssh: viewer
```
