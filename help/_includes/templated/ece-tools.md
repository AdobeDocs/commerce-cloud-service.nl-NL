---
source-git-commit: 6d8c082d78259f8f7adb0fb7f11ff4fcdb234124
workflow-type: tm+mt
source-wordcount: '4030'
ht-degree: 0%

---
# Gereedschappen

<!-- The template to render with above values -->
**Versie**: 2002.1.18

Deze verwijzing bevat 34 opdrachten die beschikbaar zijn via het opdrachtregelprogramma van `ece-tools` .
De eerste lijst wordt automatisch gegenereerd met de opdracht `ece-tools list` in Adobe Commerce op de cloud-infrastructuur.

>[!NOTE]
>
>Deze verwijzing wordt gegenereerd op basis van de toepassingscodebase. Om de inhoud te veranderen, kunt u de broncode voor de overeenkomstige bevelimplementatie in de [ codebase ](https://github.com/magento/magento-cloud-cli) bewaarplaats bijwerken en uw veranderingen voor overzicht voorleggen. Een andere manier is ons _geven terugkoppelt_ (vind de verbinding bij het hogere recht). Voor bijdragerichtsnoeren, zie {de Bijdragen van de Code 0} ](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).[

## `_complete`

Interne opdracht voor suggesties voor shell-voltooiing

```bash
ece-tools _complete [-s|--shell SHELL] [-i|--input INPUT] [-c|--current CURRENT] [-a|--api-version API-VERSION] [-S|--symfony SYMFONY]
```

### `--shell`, `-s`

Het schelpdiertype (&quot;bash&quot;, &quot;fish&quot;, &quot;zsh&quot;)

- Vereist een waarde

### `--input`, `-i`

Een array van invoertokens (bijvoorbeeld COMP_WORDS of argv)

- Standaard: `[]`
- Vereist een waarde

### `--current`, `-c`

De index van de &quot;input&quot;-array waarin de cursor zich bevindt (bijvoorbeeld COMP_CWORD)

- Vereist een waarde

### `--api-version`, `-a`

De API-versie van het voltooiingsscript

- Vereist een waarde

### `--symfony`, `-S`

verouderd

- Vereist een waarde

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `build`

Builds-toepassing.

```bash
ece-tools build
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `completion`

Het shell-voltooiingsscript dumpen

```bash
ece-tools completion [--debug] [--] [<shell>]
```


### `shell`

Het shell type (bijvoorbeeld &quot;bash&quot;), de waarde van &quot;$SHELL&quot; env var zal worden gebruikt als dit niet wordt gegeven


### `--debug`

Tik op het logbestand voor foutopsporing bij voltooien

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `db-dump`

Maakt databaseback-ups.

```bash
ece-tools db-dump [-d|--remove-definers] [-a|--dump-directory DUMP-DIRECTORY] [--] [<databases>...]
```


### `databases`

Databases voor back-up. Beschikbare Waarden: [ belangrijkste citaatverkoop ]. Als de argumentwaarde niet wordt gespecificeerd, zullen de gegevensbestandsteunen worden gecreeerd gebruikend de geloofsbrieven die in `MAGENTO_CLOUD_RELATIONSHIP` worden opgeslagen omgevingsvariabele of/en het `stage.deploy.DATABASE_CONFIGURATION` bezit van het .magento.env.yaml configuratiedossier.

- Standaard: `[]`

- Array

### `--remove-definers`, `-d`

Verwijder definities uit de gegevensbestandstortplaats

- Standaard: `false`
- Accepteert geen waarde

### `--dump-directory`, `-a`

Alternatieve directory gebruiken voor opslaan van dump

- Vereist een waarde

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `deploy`

Implementeert de toepassing.

```bash
ece-tools deploy
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `help`

Help weergeven voor een opdracht

```bash
ece-tools help [--format FORMAT] [--raw] [--] [<command_name>]
```


### `command_name`

De opdrachtnaam

- Standaard: `help`


### `--format`

De uitvoerindeling (txt, xml, json of md)

- Standaard: `txt`
- Vereist een waarde

### `--raw`

Help bij de opdracht Uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `list`

Lijstopdrachten

```bash
ece-tools list [--raw] [--format FORMAT] [--short] [--] [<namespace>]
```


### `namespace`

De naamruimtenaam


### `--raw`

Naar uitvoer RAW-opdrachtlijst

- Standaard: `false`
- Accepteert geen waarde

### `--format`

De uitvoerindeling (txt, xml, json of md)

- Standaard: `txt`
- Vereist een waarde

### `--short`

Om het beschrijven van de argumenten van bevelen over te slaan

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `patch`

Hiermee past u aangepaste patches toe.

```bash
ece-tools patch
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `post-deploy`

Voert uit na plaatsingsverrichtingen.

```bash
ece-tools post-deploy
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `run`

Voer scenario(s) uit.

```bash
ece-tools run <scenario>...
```


### `scenario`

Scenario(s)

- Standaard: `[]`

- Vereist
- Array

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `backup:list`

Hiermee geeft u de lijst met back-upbestanden weer.

```bash
ece-tools backup:list
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `backup:restore`

Belangrijke configuratiebestanden herstellen. Back-up uitvoeren:lijst met reservekopieën weergeven.

```bash
ece-tools backup:restore [-f|--force] [--file [FILE]]
```

### `--force`, `-f`

Bestaande bestanden overschrijven tijdens het herstellen van een back-up

- Standaard: `false`
- Accepteert geen waarde

### `--file`

Een specifiek pad voor bestandsherstel

- Accepteert een waarde

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `build:generate`

Hiermee worden alle benodigde bestanden gegenereerd voor het samenstellen van het werkgebied.

```bash
ece-tools build:generate
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `build:transfer`

Gegenereerde bestanden worden overgebracht naar de init-map.

```bash
ece-tools build:transfer
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `cloud:config:create`

Maakt een `.magento.env.yaml` -bestand met de opgegeven configuratie van variabelen voor samenstellen, implementeren en achteraf implementeren. Hiermee overschrijft u een bestaand `.magento,.env.yaml` -bestand.

```bash
ece-tools cloud:config:create <configuration>
```


### `configuration`

Configuratie in JSON-indeling

- Vereist

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `cloud:config:update`

Werkt het bestaande `.magento.env.yaml` dossier met de gespecificeerde configuratie bij. Maakt een `.magento.env.yaml` -bestand als dit niet bestaat.

```bash
ece-tools cloud:config:update <configuration>
```


### `configuration`

Configuratie in JSON-indeling

- Vereist

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `cloud:config:validate`

Valideert het configuratiebestand `.magento.env.yaml`

```bash
ece-tools cloud:config:validate
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `config:dump`

Vorm van de pomp voor statische inhoudsplaatsing.

```bash
ece-tools config:dump
```


```bash
ece-tools dump
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `cron:disable`

Schakel alle processen voor het uitsnijden van Magento&#39;s uit en beëindigt alle actieve processen.

```bash
ece-tools cron:disable
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `cron:enable`

Hiermee schakelt u snijprocessen voor Magento&#39;s in.

```bash
ece-tools cron:enable
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `cron:kill`

Beëindigt alle processen van de Magento kruin.

```bash
ece-tools cron:kill
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `cron:unlock`

Ontgrendel de banen van de kroon die in &quot;lopende&quot;staat bleven.

```bash
ece-tools cron:unlock [--job-code [JOB-CODE]]
```

### `--job-code`

Taakcode uitsnijden die moet worden ontgrendeld.

- Standaard: `[]`
- Accepteert meerdere waarden

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `dev:generate:schema-error`

Genereert het bestand dist/error-codes.md uit het bestand schema.error.yaml.

```bash
ece-tools dev:generate:schema-error
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `dev:git:update-composer`

Werkt composer bij voor implementatie vanuit de it.

```bash
ece-tools dev:git:update-composer
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `env:config:show`

Gecodeerde omgevingsvariabelen voor cloudconfiguratie weergeven.

```bash
ece-tools env:config:show [<variable>...]
```


### `variable`

Te tonen omgevingsvariabelen, mogelijke opties: services, routes, variabelen

- Standaard: `[]`

- Array

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `error:show`

Hier wordt informatie weergegeven over fout-id of informatie over alle fouten van de laatste implementatie.

```bash
ece-tools error:show [-j|--json] [--] [<error-code>]
```


### `error-code`

Foutcode: als er geen informatie over de opdrachtweergave wordt doorgegeven over alle fouten van de laatste implementatie


### `--json`, `-j`

Wordt gebruikt voor het ophalen van resultaten in de JSON-indeling

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `module:refresh`

Verfrist de configuratie om nieuw toegevoegde modules toe te laten.

```bash
ece-tools module:refresh
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `schema:generate`

Genereert het schema *.dist-bestand.

```bash
ece-tools schema:generate
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `wizard:ideal-state`

Verifieert ideale staat van configuratie.

```bash
ece-tools wizard:ideal-state
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `wizard:master-slave`

Verifieert master-slave configuratie.

```bash
ece-tools wizard:master-slave
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `wizard:scd-on-build`

Verifieert SCD bij bouwstijlconfiguratie.

```bash
ece-tools wizard:scd-on-build
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `wizard:scd-on-demand`

Verifieert SCD op bestelling configuratie.

```bash
ece-tools wizard:scd-on-demand
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `wizard:scd-on-deploy`

Verifieert SCD bij opstellen configuratie.

```bash
ece-tools wizard:scd-on-deploy
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `wizard:split-db-state`

Controleert de mogelijkheid om DB te splitsen en of DB al gesplitst was of niet.

```bash
ece-tools wizard:split-db-state
```

### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

### `--quiet`, `-q`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde

