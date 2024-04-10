---
source-git-commit: 99272d08a11f850a79e8e24857b7072d1946f374
workflow-type: tm+mt
source-wordcount: '21442'
ht-degree: 0%

---
# magento-cloud (Adobe Commerce op cloudinfrastructuur)

<!-- The template to render with above values -->
**Versie**: 1.46.1

Deze verwijzing bevat 119 bevelen beschikbaar door `magento-cloud` opdrachtregelprogramma.
De eerste lijst wordt automatisch gegenereerd met de opdracht `magento-cloud list` in Adobe Commerce op cloudinfrastructuur.

>[!NOTE]
>
>Deze verwijzing wordt gegenereerd op basis van de toepassingscodebase. Als u de inhoud wilt wijzigen, kunt u de broncode voor de corresponderende opdrachtimplementatie bijwerken in het dialoogvenster [codebase](https://github.com/magento/magento-cloud-cli) opslaan en uw wijzigingen ter controle verzenden. Een andere manier is om _Feedback geven_ (zoek de koppeling in de rechterbovenhoek). Zie voor richtsnoeren voor bijdragen [Codebijdragen](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).

## `clear-cache`

De CLI-cache wissen

```bash
magento-cloud cc
```

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `decode`

Een gecodeerde tekenreeks decoderen, zoals MAGENTO_CLOUD_VARIABLES

```bash
magento-cloud decode [-P|--property PROPERTY] [--] <value>
```


### `value`

De te decoderen variabele

- Vereist

### `--property`, `-P`

De eigenschap die binnen de variabele moet worden weergegeven

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `docs`

De onlinedocumentatie openen

```bash
magento-cloud docs [--browser BROWSER] [--pipe] [--] [<search>]...
```


### `search`

Zoekterm(en)

- Standaard: `[]`

- Array

### `--browser`

De browser waarmee de URL moet worden geopend. Stel 0 in voor geen.

- Vereist een waarde

### `--pipe`

Voer de URL uit die u wilt stopzetten.

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `help`

Hiermee geeft u Help voor een opdracht weer

```bash
magento-cloud help [--format FORMAT] [--raw] [--] [<command_name>]
```


### `command_name`

De opdrachtnaam

- Standaard: `help`


### `--format`

De uitvoerindeling (txt, json of md)

- Standaard: `txt`
- Vereist een waarde

### `--raw`

Help bij de opdracht Uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `list`

Lijsten, opdrachten

```bash
magento-cloud list [--raw] [--format FORMAT] [--all] [--] [<namespace>]
```


### `command`

De uit te voeren opdracht

- Vereist

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

### `--all`

Alle opdrachten tonen, inclusief verborgen opdrachten

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `multi`

Voer een bevel op veelvoudige projecten uit

```bash
magento-cloud multi [-p|--projects PROJECTS] [--continue] [--sort SORT] [--reverse] [--] <cmd> (<cmd>)...
```


### `cmd`

De uit te voeren opdracht

- Standaard: `[]`

- Vereist
- Array

### `--projects`, `-p`

Een lijst met project-id&#39;s, gescheiden door komma&#39;s en/of witruimte

- Vereist een waarde

### `--continue`

Doorgaan met opdrachten, zelfs als een uitzondering wordt aangetroffen

- Standaard: `false`
- Accepteert geen waarde

### `--sort`

Een eigenschap waarmee de lijst met projectopties moet worden gesorteerd

- Standaard: `title`
- Vereist een waarde

### `--reverse`

De volgorde van projectopties omkeren

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `web`

Open het project in het Web UI

```bash
magento-cloud web [--browser BROWSER] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--browser`

De browser waarmee de URL moet worden geopend. Stel 0 in voor geen.

- Vereist een waarde

### `--pipe`

Voer de URL uit die u wilt stopzetten.

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `activity:cancel`

Een activiteit annuleren

```bash
magento-cloud activity:cancel [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

De activiteit-id. Wordt standaard ingesteld op de meest recente annuleerbare activiteit.


### `--type`, `-t`

Filteren op type (wanneer u een standaardactiviteit selecteert). Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte. De tekens % of * kunnen worden gebruikt als jokerteken voor het type, bijvoorbeeld &#39;%var%&#39; om activiteiten met betrekking tot variabelen te selecteren.

- Standaard: `[]`
- Vereist een waarde

### `--exclude-type`, `-x`

Uitsluiten op type (bij het selecteren van een standaardactiviteit). Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte. De tekens % of * kunnen worden gebruikt als jokerteken om typen uit te sluiten.

- Standaard: `[]`
- Vereist een waarde

### `--all`, `-a`

Recente activiteiten in alle omgevingen controleren (bij het selecteren van een standaardactiviteit)

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `activity:get`

Gedetailleerde informatie over één activiteit weergeven

```bash
magento-cloud activity:get [-P|--property PROPERTY] [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<id>]
```


### `id`

De activiteit-id. Heeft als standaardwaarde de meest recente activiteit.


### `--property`, `-P`

De eigenschap die moet worden weergegeven

- Vereist een waarde

### `--type`, `-t`

Filteren op type (wanneer u een standaardactiviteit selecteert). Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte. De tekens % of * kunnen worden gebruikt als jokerteken voor het type, bijvoorbeeld &#39;%var%&#39; om activiteiten met betrekking tot variabelen te selecteren.

- Standaard: `[]`
- Vereist een waarde

### `--exclude-type`, `-x`

Uitsluiten op type (bij het selecteren van een standaardactiviteit). Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte. De tekens % of * kunnen worden gebruikt als jokerteken om typen uit te sluiten.

- Standaard: `[]`
- Vereist een waarde

### `--state`

Filteren op status (wanneer u een standaardactiviteit selecteert): in_progress, in behandeling, voltooid of geannuleerd. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--result`

Filteren op resultaat (bij het selecteren van een standaardactiviteit): geslaagd of mislukt

- Vereist een waarde

### `--incomplete`, `-i`

Alleen onvolledige activiteiten opnemen (bij het selecteren van een standaardactiviteit). Dit is een korte versie van \&lt;info>—state=in_progress,pending\&lt;/info>

- Standaard: `false`
- Accepteert geen waarde

### `--all`, `-a`

Recente activiteiten in alle omgevingen controleren (bij het selecteren van een standaardactiviteit)

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `activity:list`

Een lijst met activiteiten voor een omgeving of project ophalen

```bash
magento-cloud activities [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--type`, `-t`

Filteractiviteiten op type Waarden kunnen worden gesplitst met komma&#39;s (bijvoorbeeld &quot;a,b,c&quot;) en/of witruimte. Het eerste deel van de naam van de activiteit kan worden weggelaten, bijvoorbeeld &#39;cron&#39; kan &#39;environment.cron&#39;-activiteiten selecteren. De tekens % of * kunnen worden gebruikt als jokerteken, bijvoorbeeld &#39;%var%&#39; om activiteiten met betrekking tot variabelen te selecteren.

- Standaard: `[]`
- Vereist een waarde

### `--exclude-type`, `-x`

Activiteiten uitsluiten op basis van type. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte. Het eerste deel van de naam van de activiteit kan worden weggelaten, bijvoorbeeld &#39;cron&#39; kan &#39;environment.cron&#39;-activiteiten uitsluiten. De tekens % of * kunnen worden gebruikt als jokerteken om typen uit te sluiten.

- Standaard: `[]`
- Vereist een waarde

### `--limit`

Beperk het aantal weergegeven resultaten

- Standaard: `10`
- Vereist een waarde

### `--start`

Alleen activiteiten die vóór deze datum zijn gemaakt, worden vermeld

- Vereist een waarde

### `--state`

Activiteiten filteren op status: in_progress, in behandeling, voltooid of geannuleerd. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--result`

Activiteiten filteren op resultaat: geslaagd of mislukt

- Vereist een waarde

### `--incomplete`, `-i`

Alleen onvolledige activiteiten weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--all`, `-a`

Activiteiten weergeven in alle omgevingen

- Standaard: `false`
- Accepteert geen waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: id*, created*, description*, progress*, state*, result*, completed, environment, type (* = default columns). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `activity:log`

Logboek weergeven voor een activiteit

```bash
magento-cloud activity:log [--refresh REFRESH] [-t|--timestamps] [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

De activiteit-id. Heeft als standaardwaarde de meest recente activiteit.


### `--refresh`

Vernieuwingsinterval voor activiteit (seconden). Stel de waarde in op 0 om vernieuwen uit te schakelen.

- Standaard: `3`
- Vereist een waarde

### `--timestamps`, `-t`

Een tijdstempel naast elk bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--type`

Filteren op type (wanneer u een standaardactiviteit selecteert). Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte. De tekens % of * kunnen worden gebruikt als jokerteken voor het type, bijvoorbeeld &#39;%var%&#39; om activiteiten met betrekking tot variabelen te selecteren.

- Standaard: `[]`
- Vereist een waarde

### `--exclude-type`, `-x`

Uitsluiten op type (bij het selecteren van een standaardactiviteit). Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte. De tekens % of * kunnen worden gebruikt als jokerteken om typen uit te sluiten.

- Standaard: `[]`
- Vereist een waarde

### `--state`

Filteren op status (wanneer u een standaardactiviteit selecteert): in_progress, in behandeling, voltooid of geannuleerd. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--result`

Filteren op resultaat (bij het selecteren van een standaardactiviteit): geslaagd of mislukt

- Vereist een waarde

### `--incomplete`, `-i`

Alleen onvolledige activiteiten opnemen (bij het selecteren van een standaardactiviteit). Dit is een korte versie van \&lt;info>—state=in_progress,pending\&lt;/info>

- Standaard: `false`
- Accepteert geen waarde

### `--all`, `-a`

Recente activiteiten in alle omgevingen controleren (bij het selecteren van een standaardactiviteit)

- Standaard: `false`
- Accepteert geen waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `app:config-get`

De configuratie van een app weergeven

```bash
magento-cloud app:config-get [-P|--property PROPERTY] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE]
```

### `--property`, `-P`

Het configuratiebezit aan mening

- Vereist een waarde

### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--identity-file`, `-i`

[Vervangen optie, niet meer gebruikt]

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `app:list`

Apps weergeven in het project

```bash
magento-cloud apps [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

### `--pipe`

Alleen een lijst met toepassingsnamen uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: naam*, type*, schijf, pad, grootte (* = standaardkolommen). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `auth:api-token-login`

Aanmelden bij Magento Cloud met een API-token

```bash
magento-cloud auth:api-token-login
```

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `auth:browser-login`

Aanmelden bij Magento Cloud via een browser

```bash
magento-cloud login [-f|--force] [--browser BROWSER] [--pipe]
```

### `--force`, `-f`

Meld u opnieuw aan, zelfs als u zich al hebt aangemeld

- Standaard: `false`
- Accepteert geen waarde

### `--browser`

De browser waarmee de URL moet worden geopend. Stel 0 in voor geen.

- Vereist een waarde

### `--pipe`

Voer de URL uit die u wilt stopzetten.

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `auth:info`

Geef uw accountgegevens weer

```bash
magento-cloud auth:info [--no-auto-login] [-P|--property PROPERTY] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--] [<property>]
```


### `property`

De accounteigenschap die moet worden weergegeven


### `--no-auto-login`

Hiermee slaat u de automatische aanmelding over. Niets zal output worden als het programma geopend niet, en de uitgangscode zal 0 zijn, veronderstellend geen andere fouten.

- Standaard: `false`
- Accepteert geen waarde

### `--property`, `-P`

De accounteigenschap die moet worden weergegeven (alternatieve syntaxis)

- Vereist een waarde

### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `auth:logout`

Afmelden bij Magento Cloud

```bash
magento-cloud logout [-a|--all] [--other]
```

### `--all`, `-a`

Afmelden bij alle lokale sessies

- Standaard: `false`
- Accepteert geen waarde

### `--other`

Afmelden bij andere lokale sessies

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `blackfire:setup`

De integratie van Blackfire.io van de opstelling voor het project

```bash
magento-cloud blackfire:setup [--server_id SERVER_ID] [--server_token SERVER_TOKEN] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

### `--server_id`

De server-id

- Vereist een waarde

### `--server_token`

Het servertoken

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `certificate:add`

Een SSL-certificaat toevoegen aan het project

```bash
magento-cloud certificate:add [--cert CERT] [--key KEY] [--chain CHAIN] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

### `--cert`

Het pad naar het certificaatbestand

- Vereist een waarde

### `--key`

Het pad naar het persoonlijke sleutelbestand van het certificaat

- Vereist een waarde

### `--chain`

Het pad naar het certificaatkettingbestand

- Standaard: `[]`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `certificate:delete`

Een certificaat verwijderen uit het project

```bash
magento-cloud certificate:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] <id>
```


### `id`

De certificaat-id (of het begin ervan)

- Vereist

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `certificate:get`

Een certificaat weergeven

```bash
magento-cloud certificate:get [-P|--property PROPERTY] [--date-fmt DATE-FMT] [-p|--project PROJECT] [--] <id>
```


### `id`

De certificaat-id (of het begin ervan)

- Vereist

### `--property`, `-P`

De certificaateigenschap die moet worden weergegeven

- Vereist een waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `certificate:list`

Projectcertificaten weergeven

```bash
magento-cloud certificates [--domain DOMAIN] [--exclude-domain EXCLUDE-DOMAIN] [--issuer ISSUER] [--only-auto] [--no-auto] [--ignore-expiry] [--only-expired] [--no-expired] [--pipe-domains] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--domain`

Filteren op domeinnaam (niet-hoofdlettergevoelige zoekopdracht)

- Vereist een waarde

### `--exclude-domain`

Certificaten uitsluiten, overeenkomend op domeinnaam (niet-hoofdlettergevoelige zoekopdracht)

- Vereist een waarde

### `--issuer`

Filteren op uitgever

- Vereist een waarde

### `--only-auto`

Alleen certificaten met automatische provisioning weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--no-auto`

Alleen handmatig toegevoegde certificaten weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--ignore-expiry`

Verlopen en niet-verlopen certificaten weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--only-expired`

Alleen verlopen certificaten tonen

- Standaard: `false`
- Accepteert geen waarde

### `--no-expired`

Alleen niet-verlopen certificaten tonen (standaard)

- Standaard: `false`
- Accepteert geen waarde

### `--pipe-domains`

Retourneer alleen een lijst met domeinnamen die door de certificaten worden gedekt

- Standaard: `false`
- Accepteert geen waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: gemaakt, domeinen, verloopt, id, uitgever. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `commit:get`

Vastleggingsdetails tonen

```bash
magento-cloud commit:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--date-fmt DATE-FMT] [--] [<commit>]
```


### `commit`

De commit SHA. Dit kan ook achtervoegsels &quot;HEAD&quot;, en invoegpunt (^) of tilde (~) accepteren voor bovenliggende hoofditems.

- Standaard: `HEAD`


### `--property`, `-P`

De eigenschap commit die moet worden weergegeven.

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `commit:list`

Lijstopdrachten

```bash
magento-cloud commits [--limit LIMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<commit>]
```


### `commit`

De beginstand past SHA toe. Dit kan ook achtervoegsels &quot;HEAD&quot;, en invoegpunt (^) of tilde (~) accepteren voor bovenliggende hoofditems.


### `--limit`

Het aantal verplichtingen dat moet worden weergegeven.

- Standaard: `10`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: auteur, date, sha, summary. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `db:dump`

Creeer een lokale stortplaats van het verre gegevensbestand

```bash
magento-cloud db:dump [--schema SCHEMA] [-f|--file FILE] [-d|--directory DIRECTORY] [-z|--gzip] [-t|--timestamp] [-o|--stdout] [--table TABLE] [--exclude-table EXCLUDE-TABLE] [--schema-only] [--charset CHARSET] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE]
```

### `--schema`

Het te dumpen schema. Laat weg om het standaardschema (gewoonlijk &quot;hoofd&quot;) te gebruiken.

- Vereist een waarde

### `--file`, `-f`

Een aangepaste bestandsnaam voor de dump

- Vereist een waarde

### `--directory`, `-d`

Een aangepaste map voor de stortplaats

- Vereist een waarde

### `--gzip`, `-z`

De stortplaats comprimeren met gzip

- Standaard: `false`
- Accepteert geen waarde

### `--timestamp`, `-t`

Een tijdstempel toevoegen aan de naam van het stortplaatje

- Standaard: `false`
- Accepteert geen waarde

### `--stdout`, `-o`

Uitvoeren naar STDOUT in plaats van een bestand

- Standaard: `false`
- Accepteert geen waarde

### `--table`

Op te nemen tabel(len)

- Standaard: `[]`
- Vereist een waarde

### `--exclude-table`

Uit te sluiten tabel(len)

- Standaard: `[]`
- Vereist een waarde

### `--schema-only`

Alleen schema&#39;s dumpen, geen gegevens

- Standaard: `false`
- Accepteert geen waarde

### `--charset`

De tekensetcodering voor de dump

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--relationship`, `-r`

De de dienstverhouding om te gebruiken

- Vereist een waarde

### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `db:size`

Schatting van het schijfgebruik van een gegevensbestand

```bash
magento-cloud db:size [-B|--bytes] [-C|--cleanup] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-i|--identity-file IDENTITY-FILE]
```

### `--bytes`, `-B`

Grootte in bytes weergeven.

- Standaard: `false`
- Accepteert geen waarde

### `--cleanup`, `-C`

Controleer of tabellen kunnen worden opgeschoond en geef me aanbevelingen (alleen InnoDb).

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--relationship`, `-r`

De de dienstverhouding om te gebruiken

- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: max, percent_used, used. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `db:sql`

SQL uitvoeren op de externe database

```bash
magento-cloud sql [--raw] [--schema SCHEMA] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [--] [<query>]
```


### `query`

Een SQL-instructie die moet worden uitgevoerd


### `--raw`

Onbewerkte, niet-tabelvormige uitvoer produceren

- Standaard: `false`
- Accepteert geen waarde

### `--schema`

Het te gebruiken schema. Laat weg om het standaardschema (gewoonlijk &quot;hoofd&quot;) te gebruiken. Geef een lege tekenreeks door als u geen schema wilt gebruiken.

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--relationship`, `-r`

De de dienstverhouding om te gebruiken

- Vereist een waarde

### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `domain:add`

Een nieuw domein toevoegen aan het project

```bash
magento-cloud domain:add [--cert CERT] [--key KEY] [--chain CHAIN] [--attach ATTACH] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

De domeinnaam

- Vereist

### `--cert`

Het pad naar het certificaatbestand voor dit domein

- Vereist een waarde

### `--key`

Het pad naar het bestand met de persoonlijke sleutel voor het opgegeven certificaat.

- Vereist een waarde

### `--chain`

Het pad naar het certificaatkettingbestand of de certificaatbestanden voor het opgegeven certificaat

- Standaard: `[]`
- Vereist een waarde

### `--attach`

Het productiedomein dat deze vervangt in de routes van het milieu. Vereist voor niet-productieomgevingsdomeinen.

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `domain:delete`

Een domein verwijderen uit het project

```bash
magento-cloud domain:delete [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

De domeinnaam

- Vereist

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `domain:get`

Gedetailleerde informatie voor een domein weergeven

```bash
magento-cloud domain:get [-P|--property PROPERTY] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<name>]
```


### `name`

De domeinnaam


### `--property`, `-P`

De eigenschap domain die moet worden weergegeven

- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `domain:list`

Een lijst met alle domeinen ophalen

```bash
magento-cloud domains [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: name*, ssl*, created_at*, registered_name, replacement_for, type, updated_at (* = default columns). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `domain:update`

Een domein bijwerken

```bash
magento-cloud domain:update [--cert CERT] [--key KEY] [--chain CHAIN] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

De domeinnaam

- Vereist

### `--cert`

Het pad naar het certificaatbestand voor dit domein

- Vereist een waarde

### `--key`

Het pad naar het bestand met de persoonlijke sleutel voor het opgegeven certificaat.

- Vereist een waarde

### `--chain`

Het pad naar het certificaatkettingbestand of de certificaatbestanden voor het opgegeven certificaat

- Standaard: `[]`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:activate`

Een omgeving activeren

```bash
magento-cloud environment:activate [--parent PARENT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]...
```


### `environment`

Te activeren omgeving(en)

- Standaard: `[]`

- Array

### `--parent`

Een bovenliggende omgeving instellen voordat een omgeving wordt geactiveerd

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:branch`

Een omgeving vertakken

```bash
magento-cloud branch [--title TITLE] [--type TYPE] [--no-clone-parent] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<id>] [<parent>]
```


### `id`

De id (vertakkingsnaam) van de nieuwe omgeving


### `parent`

De bovenliggende omgeving van de nieuwe omgeving


### `--title`

De titel van de nieuwe omgeving

- Vereist een waarde

### `--type`

Het type nieuwe omgeving

- Vereist een waarde

### `--no-clone-parent`

De gegevens van de bovenliggende omgeving niet klonen

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:checkout`

Een omgeving controleren

```bash
magento-cloud checkout [-i|--identity-file IDENTITY-FILE] [--] [<id>]
```


### `id`

De id van de omgeving die moet worden uitgecheckt. Bijvoorbeeld: &quot;sprint2&quot;


### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:delete`

Een of meer omgevingen verwijderen

```bash
magento-cloud environment:delete [--delete-branch] [--no-delete-branch] [--type TYPE] [-t|--only-type ONLY-TYPE] [--exclude EXCLUDE] [--exclude-type EXCLUDE-TYPE] [--inactive] [--merged] [--allow-delete-parent] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]...
```


### `environment`

The environment(s) to delete. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`

- Array

### `--delete-branch`

Git-vertakking(en) verwijderen voor inactieve omgevingen, zonder bevestiging

- Standaard: `false`
- Accepteert geen waarde

### `--no-delete-branch`

Git-vertakking(en) niet verwijderen (niet-actieve omgevingen)

- Standaard: `false`
- Accepteert geen waarde

### `--type`

Verwijder alle omgevingen van een type (en voeg deze toe aan andere geselecteerde omgevingen) Waarden kunnen worden gesplitst met komma&#39;s (bijv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--only-type`, `-t`

Alleen verwijderomgevingen van een specifiek type Waarden kunnen worden gesplitst in komma&#39;s (bijvoorbeeld &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--exclude`

Omgeving(en) niet te verwijderen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--exclude-type`

Omgevingstype(n) waarvan de waarden niet mogen worden verwijderd, mogen worden opgesplitst in komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--inactive`

Alle niet-actieve omgevingen verwijderen (toevoegen aan andere geselecteerde omgevingen)

- Standaard: `false`
- Accepteert geen waarde

### `--merged`

Alle samengevoegde omgevingen verwijderen (aan geselecteerde omgevingen toevoegen)

- Standaard: `false`
- Accepteert geen waarde

### `--allow-delete-parent`

Toestaan dat omgevingen met onderliggende items worden verwijderd

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:http-access`

De HTTP-toegangsinstellingen voor een omgeving bijwerken

```bash
magento-cloud httpaccess [--access ACCESS] [--auth AUTH] [--enabled ENABLED] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--access`

Toegangsbeperking in de notatie &quot;permission:address&quot;. Gebruik 0 om alle adressen te wissen.

- Standaard: `[]`
- Vereist een waarde

### `--auth`

HTTP Basic auth credentials in the format &quot;username:password&quot;. Gebruik 0 om alle gegevens te wissen.

- Standaard: `[]`
- Vereist een waarde

### `--enabled`

Of toegangsbeheer zou moeten worden toegelaten: 1 om toe te laten, 0 om onbruikbaar te maken

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:info`

Eigenschappen voor een omgeving lezen of instellen

```bash
magento-cloud environment:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```


### `property`

De naam van de eigenschap


### `value`

Een nieuwe waarde voor de eigenschap instellen


### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:init`

Een omgeving initialiseren vanuit een openbare Git-opslagplaats

```bash
magento-cloud environment:init [--profile PROFILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <url>
```


### `url`

Een URL naar een Git-opslagplaats

- Vereist

### `--profile`

De naam van het profiel

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:list`

Een lijst met omgevingen ophalen

```bash
magento-cloud environments [-I|--no-inactive] [--pipe] [--refresh REFRESH] [--sort SORT] [--reverse] [--type TYPE] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--no-inactive`, `-I`

Niet-actieve omgevingen tonen

- Standaard: `false`
- Accepteert geen waarde

### `--pipe`

Een eenvoudige lijst met milieu-id&#39;s uitvoeren.

- Standaard: `false`
- Accepteert geen waarde

### `--refresh`

Of de lijst moet worden vernieuwd.

- Standaard: `1`
- Vereist een waarde

### `--sort`

Een eigenschap waarop u wilt sorteren

- Standaard: `title`
- Vereist een waarde

### `--reverse`

Omgekeerde (aflopende) volgorde sorteren

- Standaard: `false`
- Accepteert geen waarde

### `--type`

Filter de lijst op omgevingstype(n). Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: id*, title*, status*, type*, gemaakt, machine_naam, bijgewerkt (* = standaardkolommen). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:logs`

De logboeken van een omgeving lezen

```bash
magento-cloud log [--lines LINES] [--tail] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [--] [<type>]
```


### `type`

Het logtype, bijvoorbeeld &quot;access&quot; of &quot;error&quot;


### `--lines`

Het aantal regels dat moet worden weergegeven

- Standaard: `100`
- Vereist een waarde

### `--tail`

Het logboek continu staart

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--worker`

De naam van een worker

- Vereist een waarde

### `--instance`, `-I`

Instantie-id

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:merge`

Een omgeving samenvoegen

```bash
magento-cloud merge [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]
```


### `environment`

De omgeving die moet worden samengevoegd


### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:pause`

Een omgeving onderbreken

```bash
magento-cloud environment:pause [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:push`

Code naar een omgeving duwen

```bash
magento-cloud push [--target TARGET] [-f|--force] [--force-with-lease] [-u|--set-upstream] [--activate] [--parent PARENT] [--type TYPE] [--no-clone-parent] [-W|--no-wait] [--wait] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-i|--identity-file IDENTITY-FILE] [--] [<source>]
```


### `source`

De bron ref: een taknaam of begaat knoeiboel

- Standaard: `HEAD`


### `--target`

De naam van de doelvertakking. Wordt standaard ingesteld op de huidige vertakking.

- Vereist een waarde

### `--force`, `-f`

Niet-snelle updates toestaan

- Standaard: `false`
- Accepteert geen waarde

### `--force-with-lease`

Niet-snelle updates toestaan, als de verafgelegen-volgende tak bijgewerkt is

- Standaard: `false`
- Accepteert geen waarde

### `--set-upstream`, `-u`

Stel de doelomgeving in als de upstream voor de bronvertakking. Dit zal ook het doelproject als ver voor de lokale bewaarplaats plaatsen.

- Standaard: `false`
- Accepteert geen waarde

### `--activate`

De omgeving activeren voordat wordt gedrukt

- Standaard: `false`
- Accepteert geen waarde

### `--parent`

De bovenliggende nieuwe omgeving instellen (alleen gebruikt met —activate)

- Vereist een waarde

### `--type`

Het omgevingstype instellen (alleen gebruikt met —activate)

- Vereist een waarde

### `--no-clone-parent`

De gegevens van de bovenliggende vertakking niet klonen (alleen gebruikt met —activate)

- Standaard: `false`
- Accepteert geen waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:redeploy`

Een omgeving opnieuw implementeren

```bash
magento-cloud redeploy [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:relationships`

Relaties van een omgeving tonen

```bash
magento-cloud relationships [-P|--property PROPERTY] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE] [--] [<environment>]
```


### `environment`

Het milieu


### `--property`, `-P`

De relatie-eigenschap die moet worden weergegeven

- Vereist een waarde

### `--refresh`

Of de relaties moeten worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:resume`

Een gepauzeerde omgeving hervatten

```bash
magento-cloud environment:resume [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:scp`

Bestanden kopiëren van en naar een omgeving met behulp van scp

```bash
magento-cloud scp [-r|--recursive] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE] [--] [<files>]...
```


### `files`

Te kopiëren bestanden. Gebruik het voorvoegsel &#39;remote&#39;: om externe locaties te definiëren.

- Standaard: `[]`

- Array

### `--recursive`, `-r`

Gehele mappen recursief kopiëren

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--worker`

De naam van een worker

- Vereist een waarde

### `--instance`, `-I`

Instantie-id

- Vereist een waarde

### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:ssh`

SSH in de huidige omgeving

```bash
magento-cloud ssh [--pipe] [--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE] [--] [<cmd>]...
```


### `cmd`

Een opdracht die op de omgeving moet worden uitgevoerd.

- Standaard: `[]`

- Array

### `--pipe`

Alleen de SSH-URL uitvoeren.

- Standaard: `false`
- Accepteert geen waarde

### `--all`

Voer alle SSH-URL&#39;s uit (voor elke app).

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--worker`

De naam van een worker

- Vereist een waarde

### `--instance`, `-I`

Instantie-id

- Vereist een waarde

### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:synchronize`

De code en/of gegevens van een omgeving synchroniseren vanuit het bovenliggende element

```bash
magento-cloud sync [--rebase] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<synchronize>]...
```


### `synchronize`

Wat moet u synchroniseren: &quot;code&quot;, &quot;gegevens&quot; of beide

- Standaard: `[]`

- Array

### `--rebase`

Code synchroniseren door opnieuw te baseren in plaats van samen te voegen

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:url`

De openbare URL&#39;s van een omgeving ophalen

```bash
magento-cloud url [-1|--primary] [--browser BROWSER] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--primary`, `-1`

Retourneert alleen de URL voor de primaire route

- Standaard: `false`
- Accepteert geen waarde

### `--browser`

De browser waarmee de URL moet worden geopend. Stel 0 in voor geen.

- Vereist een waarde

### `--pipe`

Voer de URL uit die u wilt stopzetten.

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `environment:xdebug`

Een tunnel openen voor Xdebug in de omgeving

```bash
magento-cloud xdebug [--port PORT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--port`

De lokale poort

- Standaard: `9000`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--worker`

De naam van een worker

- Vereist een waarde

### `--instance`, `-I`

Instantie-id

- Vereist een waarde

### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `integration:activity:get`

Gedetailleerde informatie weergeven over één integratieactiviteit

```bash
magento-cloud integration:activity:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<integration>] [<activity>]
```


### `integration`

Een integratie-id. Laat leeg om uit een lijst te kiezen.


### `activity`

De activiteit-id. Wordt standaard ingesteld op de meest recente integratieactiviteit.


### `--property`, `-P`

De eigenschap die moet worden weergegeven

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

[Vervangen optie, niet gebruikt]

- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `integration:activity:list`

Een lijst met activiteiten voor integratie ophalen

```bash
magento-cloud int:act [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

Een integratie-id. Laat leeg om uit een lijst te kiezen.


### `--type`

Filteractiviteiten op type. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--exclude-type`, `-x`

Activiteiten uitsluiten op basis van type. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte. De tekens % of * kunnen worden gebruikt als jokerteken om typen uit te sluiten.

- Standaard: `[]`
- Vereist een waarde

### `--limit`

Beperk het aantal weergegeven resultaten

- Standaard: `10`
- Vereist een waarde

### `--start`

Alleen activiteiten die vóór deze datum zijn gemaakt, worden vermeld

- Vereist een waarde

### `--state`

Filteractiviteiten op status. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--result`

Activiteiten filteren op resultaat

- Vereist een waarde

### `--incomplete`, `-i`

Alleen onvolledige activiteiten weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: id*, created*, description*, type*, state*, result*, completed (* = default columns). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

[Vervangen optie, niet gebruikt]

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `integration:activity:log`

Logboek weergeven voor een integratieactiviteit

```bash
magento-cloud integration:activity:log [-t|--timestamps] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<integration>] [<activity>]
```


### `integration`

Een integratie-id. Laat leeg om uit een lijst te kiezen.


### `activity`

De activiteit-id. Wordt standaard ingesteld op de meest recente integratieactiviteit.


### `--timestamps`, `-t`

Een tijdstempel naast elk bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

[Vervangen optie, niet gebruikt]

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `integration:add`

Integratie toevoegen aan het project

```bash
magento-cloud integration:add [--type TYPE] [--base-url BASE-URL] [--bitbucket-url BITBUCKET-URL] [--username USERNAME] [--token TOKEN] [--key KEY] [--secret SECRET] [--license-key LICENSE-KEY] [--server-project SERVER-PROJECT] [--repository REPOSITORY] [--build-merge-requests BUILD-MERGE-REQUESTS] [--build-pull-requests BUILD-PULL-REQUESTS] [--build-draft-pull-requests BUILD-DRAFT-PULL-REQUESTS] [--build-pull-requests-post-merge BUILD-PULL-REQUESTS-POST-MERGE] [--build-wip-merge-requests BUILD-WIP-MERGE-REQUESTS] [--merge-requests-clone-parent-data MERGE-REQUESTS-CLONE-PARENT-DATA] [--pull-requests-clone-parent-data PULL-REQUESTS-CLONE-PARENT-DATA] [--resync-pull-requests RESYNC-PULL-REQUESTS] [--fetch-branches FETCH-BRANCHES] [--prune-branches PRUNE-BRANCHES] [--resources-init RESOURCES-INIT] [--url URL] [--shared-key SHARED-KEY] [--file FILE] [--events EVENTS] [--states STATES] [--environments ENVIRONMENTS] [--excluded-environments EXCLUDED-ENVIRONMENTS] [--from-address FROM-ADDRESS] [--recipients RECIPIENTS] [--channel CHANNEL] [--routing-key ROUTING-KEY] [--category CATEGORY] [--index INDEX] [--sourcetype SOURCETYPE] [--protocol PROTOCOL] [--syslog-host SYSLOG-HOST] [--syslog-port SYSLOG-PORT] [--facility FACILITY] [--message-format MESSAGE-FORMAT] [--auth-mode AUTH-MODE] [--auth-token AUTH-TOKEN] [--verify-tls VERIFY-TLS] [--header HEADER] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

### `--type`

Het integratietype (&#39;bitbucket&#39;, &#39;bitbucket_server&#39;, &#39;github&#39;, &#39;gitlab&#39;, &#39;webhaakje&#39;, &#39;health.email&#39;, &#39;health.pagerduty&#39;, &#39;health.slack&#39;, &#39;health.webhaakje&#39;, &#39;httplog&#39;, &#39;script&#39;, &#39;newrelic&#39;, &#39;splunk&#39;, &#39;sumologic&#39;, &#39;syslog&#39;)

- Vereist een waarde

### `--base-url`

De basis-URL van de serverinstallatie

- Vereist een waarde

### `--bitbucket-url`

De basis-URL van de Bitmap Server-installatie

- Vereist een waarde

### `--username`

De gebruikersnaam van de Bitmap-server

- Vereist een waarde

### `--token`

Een verificatie- of toegangstoken voor de integratie

- Vereist een waarde

### `--key`

Een OAuth-toets voor bitemmers

- Vereist een waarde

### `--secret`

Een Bitbucket OAuth-consumentengeheim

- Vereist een waarde

### `--license-key`

De licentiecode voor New Relic Logs

- Vereist een waarde

### `--server-project`

Het project (bijvoorbeeld &#39;namespace/repo&#39;)

- Vereist een waarde

### `--repository`

De opslagplaats die moet worden getraceerd (bv. &quot;eigenaar/opslagplaats&quot;)

- Vereist een waarde

### `--build-merge-requests`

GitLab: samenvoegverzoeken als omgevingen samenstellen

- Standaard: `true`
- Vereist een waarde

### `--build-pull-requests`

Bouw elk trekkingsverzoek als milieu

- Standaard: `true`
- Vereist een waarde

### `--build-draft-pull-requests`

Ontwerp-aanroepverzoeken samenstellen

- Standaard: `true`
- Vereist een waarde

### `--build-pull-requests-post-merge`

Trek verzoeken bouwen die op hun post-fusiestatus worden gebaseerd

- Standaard: `false`
- Vereist een waarde

### `--build-wip-merge-requests`

GitLab: aanvragen voor WIP-samenvoeging samenstellen

- Standaard: `true`
- Vereist een waarde

### `--merge-requests-clone-parent-data`

GitLab: gegevens klonen voor samenvoegverzoeken

- Standaard: `true`
- Vereist een waarde

### `--pull-requests-clone-parent-data`

De gegevens van de bovenliggende omgeving klonen voor pull-aanvragen

- Standaard: `true`
- Vereist een waarde

### `--resync-pull-requests`

Hersynchroniseer de gegevens van het trekkingsverzoek op elke bouwstijl

- Standaard: `false`
- Vereist een waarde

### `--fetch-branches`

Alle vertakkingen ophalen van de externe server (als inactieve omgevingen)

- Standaard: `true`
- Vereist een waarde

### `--prune-branches`

Vertakkingen verwijderen die niet bestaan op de externe server

- Standaard: `true`
- Vereist een waarde

### `--resources-init`

De bronnen die moeten worden gebruikt bij het initialiseren van een nieuwe service (&#39;minimum&#39;, &#39;default&#39;, &#39;manual&#39;, &#39;parent&#39;)

- Vereist een waarde

### `--url`

Het URL- of API-eindpunt voor de integratie

- Vereist een waarde

### `--shared-key`

Webhaak: de gedeelde sleutel voor JWS

- Vereist een waarde

### `--file`

De naam van een lokaal bestand dat het te uploaden script bevat

- Vereist een waarde

### `--events`

Een lijst met gebeurtenissen waarop moet worden gereageerd, bijvoorbeeld environment.push

- Standaard: `*`
- Vereist een waarde

### `--states`

Een lijst met staten waar moet worden opgetreden, bijv. pending, in_progress, complete

- Standaard: `complete`
- Vereist een waarde

### `--environments`

De milieu-id&#39;s die moeten worden opgenomen

- Standaard: `*`
- Vereist een waarde

### `--excluded-environments`

De milieu-id&#39;s om uit te sluiten

- Standaard: `[]`
- Vereist een waarde

### `--from-address`

[Optioneel] Aangepast van adres voor e-mailberichten met een waarschuwing

- Vereist een waarde

### `--recipients`

E-mailadres(sen) van ontvanger

- Standaard: `[]`
- Vereist een waarde

### `--channel`

Het kanaal Slack

- Vereist een waarde

### `--routing-key`

De PagerDuty-routeringssleutel

- Vereist een waarde

### `--category`

De Sumo Logic-categorie, gebruikt voor filteren

- Vereist een waarde

### `--index`

De segmentindex

- Vereist een waarde

### `--sourcetype`

Het brontype van de Splunk-gebeurtenis

- Vereist een waarde

### `--protocol`

Vervoersprotocol van Syslog (&quot;tcp&quot;, &quot;udp&quot;, &quot;tls&quot;)

- Standaard: `tls`
- Vereist een waarde

### `--syslog-host`

Syslog relais/inzamelaargastheer

- Vereist een waarde

### `--syslog-port`

Syslog relais/inzamelingspoort

- Vereist een waarde

### `--facility`

Syslog-faciliteit

- Standaard: `1`
- Vereist een waarde

### `--message-format`

Syslog-berichtindeling (&#39;rfc3164&#39; of &#39;rfc5424&#39;)

- Standaard: `rfc5424`
- Vereist een waarde

### `--auth-mode`

Verificatiemodus (&#39;prefix&#39; of &#39;gestructureerde_data&#39;)

- Standaard: `prefix`
- Vereist een waarde

### `--auth-token`

Verificatietoken

- Vereist een waarde

### `--verify-tls`

Of HTTPS-certificaatverificatie moet worden ingeschakeld (aanbevolen)

- Standaard: `true`
- Vereist een waarde

### `--header`

HTTP-header(s) die moet worden gebruikt in POST-aanvragen. Scheid namen en waarden met een dubbele punt (:).

- Standaard: `[]`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `integration:delete`

Integratie uit een project verwijderen

```bash
magento-cloud integration:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

De integratie-id. Laat leeg om uit een lijst te kiezen.


### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `integration:get`

Details van een integratie weergeven

```bash
magento-cloud integration:get [-P|--property [PROPERTY]] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<id>]
```


### `id`

Een integratie-id. Laat leeg om uit een lijst te kiezen.


### `--property`, `-P`

De integratieeigenschap die moet worden weergegeven

- Accepteert een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `integration:list`

Een lijst met projectintegratie(s) weergeven

```bash
magento-cloud integrations [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: id, summary, type. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `integration:update`

Integratie bijwerken

```bash
magento-cloud integration:update [--type TYPE] [--base-url BASE-URL] [--bitbucket-url BITBUCKET-URL] [--username USERNAME] [--token TOKEN] [--key KEY] [--secret SECRET] [--license-key LICENSE-KEY] [--server-project SERVER-PROJECT] [--repository REPOSITORY] [--build-merge-requests BUILD-MERGE-REQUESTS] [--build-pull-requests BUILD-PULL-REQUESTS] [--build-draft-pull-requests BUILD-DRAFT-PULL-REQUESTS] [--build-pull-requests-post-merge BUILD-PULL-REQUESTS-POST-MERGE] [--build-wip-merge-requests BUILD-WIP-MERGE-REQUESTS] [--merge-requests-clone-parent-data MERGE-REQUESTS-CLONE-PARENT-DATA] [--pull-requests-clone-parent-data PULL-REQUESTS-CLONE-PARENT-DATA] [--resync-pull-requests RESYNC-PULL-REQUESTS] [--fetch-branches FETCH-BRANCHES] [--prune-branches PRUNE-BRANCHES] [--resources-init RESOURCES-INIT] [--url URL] [--shared-key SHARED-KEY] [--file FILE] [--events EVENTS] [--states STATES] [--environments ENVIRONMENTS] [--excluded-environments EXCLUDED-ENVIRONMENTS] [--from-address FROM-ADDRESS] [--recipients RECIPIENTS] [--channel CHANNEL] [--routing-key ROUTING-KEY] [--category CATEGORY] [--index INDEX] [--sourcetype SOURCETYPE] [--protocol PROTOCOL] [--syslog-host SYSLOG-HOST] [--syslog-port SYSLOG-PORT] [--facility FACILITY] [--message-format MESSAGE-FORMAT] [--auth-mode AUTH-MODE] [--auth-token AUTH-TOKEN] [--verify-tls VERIFY-TLS] [--header HEADER] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

De id van de bij te werken integratie


### `--type`

Het integratietype (&#39;bitbucket&#39;, &#39;bitbucket_server&#39;, &#39;github&#39;, &#39;gitlab&#39;, &#39;webhaakje&#39;, &#39;health.email&#39;, &#39;health.pagerduty&#39;, &#39;health.slack&#39;, &#39;health.webhaakje&#39;, &#39;httplog&#39;, &#39;script&#39;, &#39;newrelic&#39;, &#39;splunk&#39;, &#39;sumologic&#39;, &#39;syslog&#39;)

- Vereist een waarde

### `--base-url`

De basis-URL van de serverinstallatie

- Vereist een waarde

### `--bitbucket-url`

De basis-URL van de Bitmap Server-installatie

- Vereist een waarde

### `--username`

De gebruikersnaam van de Bitmap-server

- Vereist een waarde

### `--token`

Een verificatie- of toegangstoken voor de integratie

- Vereist een waarde

### `--key`

Een OAuth-toets voor bitemmers

- Vereist een waarde

### `--secret`

Een Bitbucket OAuth-consumentengeheim

- Vereist een waarde

### `--license-key`

De licentiecode voor New Relic Logs

- Vereist een waarde

### `--server-project`

Het project (bijvoorbeeld &#39;namespace/repo&#39;)

- Vereist een waarde

### `--repository`

De opslagplaats die moet worden getraceerd (bv. &quot;eigenaar/opslagplaats&quot;)

- Vereist een waarde

### `--build-merge-requests`

GitLab: samenvoegverzoeken als omgevingen samenstellen

- Standaard: `true`
- Vereist een waarde

### `--build-pull-requests`

Bouw elk trekkingsverzoek als milieu

- Standaard: `true`
- Vereist een waarde

### `--build-draft-pull-requests`

Ontwerp-aanroepverzoeken samenstellen

- Standaard: `true`
- Vereist een waarde

### `--build-pull-requests-post-merge`

Trek verzoeken bouwen die op hun post-fusiestatus worden gebaseerd

- Standaard: `false`
- Vereist een waarde

### `--build-wip-merge-requests`

GitLab: aanvragen voor WIP-samenvoeging samenstellen

- Standaard: `true`
- Vereist een waarde

### `--merge-requests-clone-parent-data`

GitLab: gegevens klonen voor samenvoegverzoeken

- Standaard: `true`
- Vereist een waarde

### `--pull-requests-clone-parent-data`

De gegevens van de bovenliggende omgeving klonen voor pull-aanvragen

- Standaard: `true`
- Vereist een waarde

### `--resync-pull-requests`

Hersynchroniseer de gegevens van het trekkingsverzoek op elke bouwstijl

- Standaard: `false`
- Vereist een waarde

### `--fetch-branches`

Alle vertakkingen ophalen van de externe server (als inactieve omgevingen)

- Standaard: `true`
- Vereist een waarde

### `--prune-branches`

Vertakkingen verwijderen die niet bestaan op de externe server

- Standaard: `true`
- Vereist een waarde

### `--resources-init`

De bronnen die moeten worden gebruikt bij het initialiseren van een nieuwe service (&#39;minimum&#39;, &#39;default&#39;, &#39;manual&#39;, &#39;parent&#39;)

- Vereist een waarde

### `--url`

Het URL- of API-eindpunt voor de integratie

- Vereist een waarde

### `--shared-key`

Webhaak: de gedeelde sleutel voor JWS

- Vereist een waarde

### `--file`

De naam van een lokaal bestand dat het te uploaden script bevat

- Vereist een waarde

### `--events`

Een lijst met gebeurtenissen waarop moet worden gereageerd, bijvoorbeeld environment.push

- Standaard: `*`
- Vereist een waarde

### `--states`

Een lijst met staten waar moet worden opgetreden, bijv. pending, in_progress, complete

- Standaard: `complete`
- Vereist een waarde

### `--environments`

De milieu-id&#39;s die moeten worden opgenomen

- Standaard: `*`
- Vereist een waarde

### `--excluded-environments`

De milieu-id&#39;s om uit te sluiten

- Standaard: `[]`
- Vereist een waarde

### `--from-address`

[Optioneel] Aangepast van adres voor e-mailberichten met een waarschuwing

- Vereist een waarde

### `--recipients`

E-mailadres(sen) van ontvanger

- Standaard: `[]`
- Vereist een waarde

### `--channel`

Het kanaal Slack

- Vereist een waarde

### `--routing-key`

De PagerDuty-routeringssleutel

- Vereist een waarde

### `--category`

De Sumo Logic-categorie, gebruikt voor filteren

- Vereist een waarde

### `--index`

De segmentindex

- Vereist een waarde

### `--sourcetype`

Het brontype van de Splunk-gebeurtenis

- Vereist een waarde

### `--protocol`

Vervoersprotocol van Syslog (&quot;tcp&quot;, &quot;udp&quot;, &quot;tls&quot;)

- Standaard: `tls`
- Vereist een waarde

### `--syslog-host`

Syslog relais/inzamelaargastheer

- Vereist een waarde

### `--syslog-port`

Syslog relais/inzamelingspoort

- Vereist een waarde

### `--facility`

Syslog-faciliteit

- Standaard: `1`
- Vereist een waarde

### `--message-format`

Syslog-berichtindeling (&#39;rfc3164&#39; of &#39;rfc5424&#39;)

- Standaard: `rfc5424`
- Vereist een waarde

### `--auth-mode`

Verificatiemodus (&#39;prefix&#39; of &#39;gestructureerde_data&#39;)

- Standaard: `prefix`
- Vereist een waarde

### `--auth-token`

Verificatietoken

- Vereist een waarde

### `--verify-tls`

Of HTTPS-certificaatverificatie moet worden ingeschakeld (aanbevolen)

- Standaard: `true`
- Vereist een waarde

### `--header`

HTTP-header(s) die moet worden gebruikt in POST-aanvragen. Scheid namen en waarden met een dubbele punt (:).

- Standaard: `[]`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `integration:validate`

Een bestaande integratie valideren

```bash
magento-cloud integration:validate [-p|--project PROJECT] [--] [<id>]
```


### `id`

Een integratie-id. Laat leeg om uit een lijst te kiezen.


### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `local:build`

Bouw plaatselijk het huidige project

```bash
magento-cloud build [-a|--abslinks] [-s|--source SOURCE] [-d|--destination DESTINATION] [-c|--copy] [--clone] [--run-deploy-hooks] [--no-clean] [--no-archive] [--no-backup] [--no-cache] [--no-build-hooks] [--no-deps] [--working-copy] [--concurrency CONCURRENCY] [--lock] [--] [<app>]...
```


### `app`

Toepassingen opgeven die moeten worden gemaakt

- Standaard: `[]`

- Array

### `--abslinks`, `-a`

Absolute koppelingen gebruiken

- Standaard: `false`
- Accepteert geen waarde

### `--source`, `-s`

De bronmap. Wordt standaard ingesteld op de huidige projecthoofdmap.

- Vereist een waarde

### `--destination`, `-d`

De bestemming, waaraan de webhoofdmap van elke app wordt gekoppeld. Standaard: _www

- Vereist een waarde

### `--copy`, `-c`

Kopiëren naar een build-directory in plaats van te symboliseren vanaf de bron

- Standaard: `false`
- Accepteert geen waarde

### `--clone`

Gebruik Git om de huidige HEAD naar de bouwstijldirectory te klonen

- Standaard: `false`
- Accepteert geen waarde

### `--run-deploy-hooks`

Implementatie- en/of post_implementatiehaken uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-clean`

Oude builds niet verwijderen

- Standaard: `false`
- Accepteert geen waarde

### `--no-archive`

Maak of gebruik geen build-archief

- Standaard: `false`
- Accepteert geen waarde

### `--no-backup`

Maak geen back-up van de vorige build

- Standaard: `false`
- Accepteert geen waarde

### `--no-cache`

Cache uitschakelen

- Standaard: `false`
- Accepteert geen waarde

### `--no-build-hooks`

Geen haken voor na het bouwen uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--no-deps`

Installeer geen build-afhankelijkheden lokaal

- Standaard: `false`
- Accepteert geen waarde

### `--working-copy`

Duwen: gebruik git om een opslagplaats voor elke Drupal-module te klonen in plaats van gewoon een versie te downloaden

- Standaard: `false`
- Accepteert geen waarde

### `--concurrency`

Duw: stel het aantal gelijktijdige projecten in dat tegelijkertijd wordt verwerkt

- Standaard: `4`
- Vereist een waarde

### `--lock`

Duw: maak of werk een vergrendelingsbestand bij (alleen beschikbaar met Duw versie 7+)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `local:dir`

De lokale hoofdmap van het project zoeken

```bash
magento-cloud dir [<subdir>]
```


### `subdir`

De submap die moet worden gevonden (&#39;local&#39;, &#39;web&#39; of &#39;shared&#39;)


### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `metrics:all`

Cpu-, schijf- en geheugengegevens voor een omgeving weergeven

```bash
magento-cloud metrics [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`, `-B`

Grootte in bytes weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--range`, `-r`

Het tijdbereik. Metriek wordt voor deze duur geladen tot de eindtijd (—to). U kunt eenheden opgeven: uren (h), minuten (m) of seconden (s). Minimum \&lt;comment>5 m&lt;/comment>, maximum \&lt;comment>8 uur&lt;/comment> of meer (afhankelijk van het project), standaard \&lt;comment>10 m&lt;/comment>.

- Vereist een waarde

### `--interval`, `-i`

Het tijdinterval. De standaardwaarde is een verdeling van het bereik. U kunt eenheden opgeven: uren (h), minuten (m) of seconden (s). Minimum \&lt;comment>1 m&lt;/comment>.

- Vereist een waarde

### `--to`

De eindtijd. Tot nu toe is dat standaard het geval.

- Vereist een waarde

### `--latest`, `-1`

Alleen het laatste enkele gegevenspunt weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--service`, `-s`

Filteren op service- of toepassingsnaam De tekens % of * kunnen als jokerteken worden gebruikt.

- Standaard: `[]`
- Vereist een waarde

### `--type`

Filteren op servicetype (indien —service niet opgegeven). De versie is niet vereist. De tekens % of * kunnen als jokerteken worden gebruikt.

- Standaard: `[]`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: tijdstempel*, service*, cpu_percent*, mem_percent*, disk_percent*, tmp_disk_percent*, cpu_limit, cpu_used, disk_limit, disk_used, inodes_limit, inodes_percent, inodes_used, mem_limit, mem_used, tmp_disk_limit, tmp_disk_used_limit, tmp_inodes_percent, tmp_inodes_used, type (* = default columns). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `metrics:cpu`

CPU-gebruik van een omgeving tonen

```bash
magento-cloud cpu [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--range`, `-r`

Het tijdbereik. Metriek wordt voor deze duur geladen tot de eindtijd (—to). U kunt eenheden opgeven: uren (h), minuten (m) of seconden (s). Minimum \&lt;comment>5 m&lt;/comment>, maximum \&lt;comment>8 uur&lt;/comment> of meer (afhankelijk van het project), standaard \&lt;comment>10 m&lt;/comment>.

- Vereist een waarde

### `--interval`, `-i`

Het tijdinterval. De standaardwaarde is een verdeling van het bereik. U kunt eenheden opgeven: uren (h), minuten (m) of seconden (s). Minimum \&lt;comment>1 m&lt;/comment>.

- Vereist een waarde

### `--to`

De eindtijd. Tot nu toe is dat standaard het geval.

- Vereist een waarde

### `--latest`, `-1`

Alleen het laatste enkele gegevenspunt weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--service`, `-s`

Filteren op service- of toepassingsnaam De tekens % of * kunnen als jokerteken worden gebruikt.

- Standaard: `[]`
- Vereist een waarde

### `--type`

Filteren op servicetype (indien —service niet opgegeven). De versie is niet vereist. De tekens % of * kunnen als jokerteken worden gebruikt.

- Standaard: `[]`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: timestamp*, service*, used*, limit*, percent*, type (* = default columns). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `metrics:disk-usage`

Schijfgebruik van een omgeving tonen

```bash
magento-cloud disk [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [--tmp] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`, `-B`

Grootte in bytes weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--range`, `-r`

Het tijdbereik. Metriek wordt voor deze duur geladen tot de eindtijd (—to). U kunt eenheden opgeven: uren (h), minuten (m) of seconden (s). Minimum \&lt;comment>5 m&lt;/comment>, maximum \&lt;comment>8 uur&lt;/comment> of meer (afhankelijk van het project), standaard \&lt;comment>10 m&lt;/comment>.

- Vereist een waarde

### `--interval`, `-i`

Het tijdinterval. De standaardwaarde is een verdeling van het bereik. U kunt eenheden opgeven: uren (h), minuten (m) of seconden (s). Minimum \&lt;comment>1 m&lt;/comment>.

- Vereist een waarde

### `--to`

De eindtijd. Tot nu toe is dat standaard het geval.

- Vereist een waarde

### `--latest`, `-1`

Alleen het laatste enkele gegevenspunt weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--service`, `-s`

Filteren op service- of toepassingsnaam De tekens % of * kunnen als jokerteken worden gebruikt.

- Standaard: `[]`
- Vereist een waarde

### `--type`

Filteren op servicetype (indien —service niet opgegeven). De versie is niet vereist. De tekens % of * kunnen als jokerteken worden gebruikt.

- Standaard: `[]`
- Vereist een waarde

### `--tmp`

Het tijdelijke schijfgebruik van het rapport (toont kolommen: timestamp, de dienst, tmp_used, tmp_limit, tmp_percent, tmp_ipercent)

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: timestamp*, service*, used*, limit*, percent*, ipercent*, tmp_percent*, ilimit, used, tmp_ilimit, tmp_ipercent, tmp_iused, tmp_limit, tmp_limit, tmp_used, type (* = default columns). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `metrics:memory`

Geheugengebruik van een omgeving weergeven

```bash
magento-cloud mem [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`, `-B`

Grootte in bytes weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--range`, `-r`

Het tijdbereik. Metriek wordt voor deze duur geladen tot de eindtijd (—to). U kunt eenheden opgeven: uren (h), minuten (m) of seconden (s). Minimum \&lt;comment>5 m&lt;/comment>, maximum \&lt;comment>8 uur&lt;/comment> of meer (afhankelijk van het project), standaard \&lt;comment>10 m&lt;/comment>.

- Vereist een waarde

### `--interval`, `-i`

Het tijdinterval. De standaardwaarde is een verdeling van het bereik. U kunt eenheden opgeven: uren (h), minuten (m) of seconden (s). Minimum \&lt;comment>1 m&lt;/comment>.

- Vereist een waarde

### `--to`

De eindtijd. Tot nu toe is dat standaard het geval.

- Vereist een waarde

### `--latest`, `-1`

Alleen het laatste enkele gegevenspunt weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--service`, `-s`

Filteren op service- of toepassingsnaam De tekens % of * kunnen als jokerteken worden gebruikt.

- Standaard: `[]`
- Vereist een waarde

### `--type`

Filteren op servicetype (indien —service niet opgegeven). De versie is niet vereist. De tekens % of * kunnen als jokerteken worden gebruikt.

- Standaard: `[]`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: timestamp*, service*, used*, limit*, percent*, type (* = default columns). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `mount:download`

Bestanden downloaden van een berg, via resynchroniseren

```bash
magento-cloud mount:download [-a|--all] [-m|--mount MOUNT] [--target TARGET] [--source-path] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--all`, `-a`

Downloaden vanaf alle locaties

- Standaard: `false`
- Accepteert geen waarde

### `--mount`, `-m`

De koppeling (als een pad dat relatief is ten opzichte van de toepassing)

- Vereist een waarde

### `--target`

De map waarnaar bestanden worden gedownload. Als —all wordt gebruikt, zal de koppelingsweg worden toegevoegd

- Vereist een waarde

### `--source-path`

Gebruik het bronpad van de koppeling (in plaats van het koppelingspad) als submap van het doel, wanneer —alles wordt gebruikt

- Standaard: `false`
- Accepteert geen waarde

### `--delete`

Of vreemde bestanden in de doelmap moeten worden verwijderd

- Standaard: `false`
- Accepteert geen waarde

### `--exclude`

Bestand(en) om uit te sluiten van downloaden (patroon)

- Standaard: `[]`
- Vereist een waarde

### `--include`

Bestand(en) niet uit te sluiten (patroon)

- Standaard: `[]`
- Vereist een waarde

### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--worker`

De naam van een worker

- Vereist een waarde

### `--instance`, `-I`

Instantie-id

- Vereist een waarde

### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `mount:list`

Een lijst met bevestigingen ophalen

```bash
magento-cloud mounts [--paths] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

### `--paths`

Alleen de koppelingspaden uitvoeren (één per regel)

- Standaard: `false`
- Accepteert geen waarde

### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: definitie, pad. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--worker`

De naam van een worker

- Vereist een waarde

### `--instance`, `-I`

Instantie-id

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `mount:size`

Controleer het schijfgebruik van bevestigingen

```bash
magento-cloud mount:size [-B|--bytes] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

### `--bytes`, `-B`

Grootte in bytes weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--refresh`

De cache vernieuwen

- Standaard: `false`
- Accepteert geen waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: beschikbaar, max, monts, percent_used, sizes, used. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--worker`

De naam van een worker

- Vereist een waarde

### `--instance`, `-I`

Instantie-id

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `mount:upload`

Bestanden uploaden naar een koppelingsgebied, via opnieuw synchroniseren

```bash
magento-cloud mount:upload [--source SOURCE] [-m|--mount MOUNT] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--source`

Een map met bestanden die moeten worden geüpload

- Vereist een waarde

### `--mount`, `-m`

De koppeling (als een pad dat relatief is ten opzichte van de toepassing)

- Vereist een waarde

### `--delete`

Of vreemde bestanden in de telling moeten worden verwijderd

- Standaard: `false`
- Accepteert geen waarde

### `--exclude`

Bestand(en) om uit te sluiten van uploaden (patroon)

- Standaard: `[]`
- Vereist een waarde

### `--include`

Bestand(en) niet uit te sluiten (patroon)

- Standaard: `[]`
- Vereist een waarde

### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--worker`

De naam van een worker

- Vereist een waarde

### `--instance`, `-I`

Instantie-id

- Vereist een waarde

### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `operation:list`

Runtimebewerkingen weergeven in een omgeving

```bash
magento-cloud ops [--full] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--full`

Beperk de lengte van de opdracht niet tot de weergave. De standaardlimiet is 24 regels.

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--worker`

De naam van een worker

- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: service*, naam*, start*, rol, stop (* = standaardkolommen). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `operation:run`

Een bewerking uitvoeren op de omgeving

```bash
magento-cloud operation:run [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-W|--no-wait] [--wait] [--] [<operation>]
```


### `operation`

De naam van de bewerking


### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--worker`

De naam van een worker

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `project:clear-build-cache`

De cache voor het samenstellen van projecten wissen

```bash
magento-cloud project:clear-build-cache [-p|--project PROJECT]
```

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `project:get`

Een project lokaal klonen

```bash
magento-cloud get [-e|--environment ENVIRONMENT] [--depth DEPTH] [--build] [-p|--project PROJECT] [-i|--identity-file IDENTITY-FILE] [--] [<project>] [<directory>]
```


### `project`

Project-id


### `directory`

De map waarnaar moet worden gekloond. Wordt standaard ingesteld op de projecttitel


### `--environment`, `-e`

De milieu-id om te klonen. Wordt standaard ingesteld op de standaardinstelling van het project of de eerste beschikbare omgeving

- Vereist een waarde

### `--depth`

Een ondiepe kloon maken: het aantal vastleggingen in de geschiedenis beperken

- Vereist een waarde

### `--build`

Het project na het klonen maken

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `project:info`

Eigenschappen voor een project lezen of instellen

```bash
magento-cloud project:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```


### `property`

De naam van de eigenschap


### `value`

Een nieuwe waarde voor de eigenschap instellen


### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `project:list`

Een lijst met alle actieve projecten ophalen

```bash
magento-cloud projects [--pipe] [--region REGION] [--title TITLE] [--my] [--refresh REFRESH] [--sort SORT] [--reverse] [--page PAGE] [-c|--count COUNT] [--format FORMAT] [--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--pipe`

Een eenvoudige lijst met project-id&#39;s uitvoeren. Hiermee schakelt u paginering uit.

- Standaard: `false`
- Accepteert geen waarde

### `--region`

Filteren op gebied (exact overeenkomend)

- Vereist een waarde

### `--title`

Filteren op titel (niet-hoofdlettergevoelig zoeken)

- Vereist een waarde

### `--my`

Alleen de projecten weergeven die u bezit

- Standaard: `false`
- Accepteert geen waarde

### `--refresh`

Of de lijst moet worden vernieuwd

- Standaard: `1`
- Vereist een waarde

### `--sort`

Een eigenschap waarop u wilt sorteren

- Standaard: `title`
- Vereist een waarde

### `--reverse`

Omgekeerde (aflopende) volgorde sorteren

- Standaard: `false`
- Accepteert geen waarde

### `--page`

Paginanummer Dit laat paginering, ondanks configuratie of —count toe. Genegeerd als —pipe is opgegeven.

- Vereist een waarde

### `--count`, `-c`

Het aantal projecten dat per pagina moet worden weergegeven. Gebruik 0 om paginering uit te schakelen. Genegeerd als —page is gespecificeerd.

- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`

Weer te geven kolommen. Beschikbare kolommen: id*, title*, region*, created_at, organisation_id, organisation_label, organisation_name, status (* = standaardkolommen). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `project:set-remote`

Het externe project instellen voor de huidige Git-opslagplaats

```bash
magento-cloud set-remote [<project>]
```


### `project`

Project-id


### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `repo:cat`

Een bestand lezen in de gegevensopslagruimte van het project

```bash
magento-cloud repo:cat [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] <path>
```


### `path`

Het pad naar het bestand

- Vereist

### `--commit`, `-c`

De commit SHA. Dit kan ook achtervoegsels &quot;HEAD&quot;, en invoegpunt (^) of tilde (~) accepteren voor bovenliggende hoofditems.

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `repo:ls`

Bestanden weergeven in de gegevensopslagruimte van het project

```bash
magento-cloud repo:ls [-d|--directories] [-f|--files] [--git-style] [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<path>]
```


### `path`

Het pad naar een submap


### `--directories`, `-d`

Alleen directory&#39;s tonen

- Standaard: `false`
- Accepteert geen waarde

### `--files`, `-f`

Alleen bestanden tonen

- Standaard: `false`
- Accepteert geen waarde

### `--git-style`

Stijl, uitvoer vergelijkbaar met &#39;git ls-tree&#39;

- Standaard: `false`
- Accepteert geen waarde

### `--commit`, `-c`

De commit SHA. Dit kan ook achtervoegsels &quot;HEAD&quot;, en invoegpunt (^) of tilde (~) accepteren voor bovenliggende hoofditems.

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `repo:read`

Een map of bestand lezen in de projectopslagplaats

```bash
magento-cloud read [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<path>]
```


### `path`

Het pad naar de map of het bestand


### `--commit`, `-c`

De commit SHA. Dit kan ook achtervoegsels &quot;HEAD&quot;, en invoegpunt (^) of tilde (~) accepteren voor bovenliggende hoofditems.

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `route:get`

Gedetailleerde informatie over een route weergeven

```bash
magento-cloud route:get [--id ID] [-1|--primary] [-P|--property PROPERTY] [--refresh] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE] [--] [<route>]
```


### `route`

Originele URL van de route


### `--id`

Een route-id om te selecteren

- Vereist een waarde

### `--primary`, `-1`

Selecteer de primaire route

- Standaard: `false`
- Accepteert geen waarde

### `--property`, `-P`

De weer te geven eigenschap

- Vereist een waarde

### `--refresh`

Het geheime voorgeheugen van routes omzeilen

- Standaard: `false`
- Accepteert geen waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

[Vervangen optie, niet meer gebruikt]

- Vereist een waarde

### `--identity-file`, `-i`

[Vervangen optie, niet meer gebruikt]

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `route:list`

Alle routes weergeven voor een omgeving

```bash
magento-cloud routes [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<environment>]
```


### `environment`

De milieu-id


### `--refresh`

Het geheime voorgeheugen van routes omzeilen

- Standaard: `false`
- Accepteert geen waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: route*, type*, to*, url (* = standaardkolommen). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `self:install`

CLI-configuratiebestanden installeren of bijwerken

```bash
magento-cloud self:install [--shell-type SHELL-TYPE]
```

### `--shell-type`

Het shell-type voor automatisch aanvullen (bash of zsh)

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `self:update`

CLI bijwerken naar de nieuwste versie

```bash
magento-cloud update [--no-major] [--unstable] [--manifest MANIFEST] [--current-version CURRENT-VERSION] [--timeout TIMEOUT]
```

### `--no-major`

Alleen bijwerken tussen kleine versies of patchversies

- Standaard: `false`
- Accepteert geen waarde

### `--unstable`

Bijwerken naar een nieuwe, instabiele versie, indien beschikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--manifest`

De locatie van het manifestbestand overschrijven

- Vereist een waarde

### `--current-version`

De huidige versie overschrijven

- Vereist een waarde

### `--timeout`

Een time-out voor de versiecontrole

- Standaard: `30`
- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `service:list`

De diensten van de lijst in het project

```bash
magento-cloud services [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

### `--pipe`

Alleen een lijst met servicenamen uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: schijf, naam, grootte, type. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `service:mongo:dump`

Een binaire archiefstortplaats maken van gegevens van MongoDB

```bash
magento-cloud mongodump [-c|--collection COLLECTION] [-z|--gzip] [-o|--stdout] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`, `-c`

De inzameling aan stortplaats

- Vereist een waarde

### `--gzip`, `-z`

De stortplaats comprimeren met gzip

- Standaard: `false`
- Accepteert geen waarde

### `--stdout`, `-o`

Uitvoeren naar STDOUT in plaats van een bestand

- Standaard: `false`
- Accepteert geen waarde

### `--relationship`, `-r`

De de dienstverhouding om te gebruiken

- Vereist een waarde

### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `service:mongo:export`

Gegevens exporteren uit MongoDB

```bash
magento-cloud mongoexport [-c|--collection COLLECTION] [--jsonArray] [--type TYPE] [-f|--fields FIELDS] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`, `-c`

De verzameling die u wilt exporteren

- Vereist een waarde

### `--jsonArray`

Gegevens exporteren als één JSON-array

- Standaard: `false`
- Accepteert geen waarde

### `--type`

Het exporttype, bijvoorbeeld &quot;csv&quot;

- Vereist een waarde

### `--fields`, `-f`

De velden die u wilt exporteren

- Standaard: `[]`
- Vereist een waarde

### `--relationship`, `-r`

De de dienstverhouding om te gebruiken

- Vereist een waarde

### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `service:mongo:restore`

Herstel een binaire archiefstortplaats van gegevens in MongoDB

```bash
magento-cloud mongorestore [-c|--collection COLLECTION] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`, `-c`

De te herstellen verzameling

- Vereist een waarde

### `--relationship`, `-r`

De de dienstverhouding om te gebruiken

- Vereist een waarde

### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `service:mongo:shell`

De shell van MongoDB gebruiken

```bash
magento-cloud mongo [--eval EVAL] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--eval`

Een JavaScript-fragment doorgeven aan de shell

- Vereist een waarde

### `--relationship`, `-r`

De de dienstverhouding om te gebruiken

- Vereist een waarde

### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `service:redis-cli`

Toegang tot de CLI van Redis

```bash
magento-cloud redis [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--] [<args>]
```


### `args`

Argumenten die moeten worden toegevoegd aan de opdracht Redis


### `--relationship`, `-r`

De de dienstverhouding om te gebruiken

- Vereist een waarde

### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `snapshot:create`

Een opname maken van een omgeving

```bash
magento-cloud backup [--live] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]
```


### `environment`

Het milieu


### `--live`

Live back-up: stop de omgeving niet. Als deze optie is ingesteld, blijft de omgeving actief en kunnen er verbindingen worden gemaakt tijdens de back-up. Dit vermindert onderbreking, met het risico om gegevens in een inconsistente staat te steunen.

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `snapshot:delete`

Een omgevingsopname verwijderen

```bash
magento-cloud snapshot:delete [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

De id van de momentopname. Vereist in niet-interactieve modus.


### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `snapshot:get`

Een omgevingsmomentopname weergeven

```bash
magento-cloud snapshot:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--date-fmt DATE-FMT] [--] [<id>]
```


### `id`

De id van de momentopname. Wordt standaard ingesteld op de meest recente.


### `--property`, `-P`

De eigenschap die moet worden weergegeven.

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `snapshot:list`

Beschikbare momentopnamen van een omgeving weergeven

```bash
magento-cloud snapshots [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `snapshot:restore`

Een omgevingsmomentopname herstellen

```bash
magento-cloud snapshot:restore [--target TARGET] [--branch-from BRANCH-FROM] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<snapshot>]
```


### `snapshot`

De naam van de opname. Wordt standaard ingesteld op de meest recente


### `--target`

De omgeving die moet worden hersteld. Wordt standaard ingesteld op de huidige omgeving van de momentopname

- Vereist een waarde

### `--branch-from`

Als —target nog niet bestaat, specificeert dit de ouder van het nieuwe milieu

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `source-operation:list`

Bronbewerkingen in een omgeving weergeven

```bash
magento-cloud source-ops [--full] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--full`

Beperk de lengte van de opdracht niet tot de weergave. De standaardlimiet is 24 regels.

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: app, command, operation. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `source-operation:run`

Een bronbewerking uitvoeren

```bash
magento-cloud source-operation:run [--variable VARIABLE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<operation>]
```


### `operation`

De naam van de bewerking


### `--variable`

Een variabele die tijdens de bewerking moet worden ingesteld, in de notatie \&lt;info>type:name=value\&lt;/info>

- Standaard: `[]`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `ssh-cert:load`

Een SSH-certificaat genereren

```bash
magento-cloud ssh-cert:load [--refresh-only] [--new] [--new-key]
```

### `--refresh-only`

Vernieuw slechts het certificaat, indien nodig (schrijf geen SSH config)

- Standaard: `false`
- Accepteert geen waarde

### `--new`

Vernieuwen van certificaat forceren

- Standaard: `false`
- Accepteert geen waarde

### `--new-key`

[Vervangen] Gebruik —nieuw in plaats hiervan

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `ssh-key:add`

Een nieuwe SSH-toets toevoegen

```bash
magento-cloud ssh-key:add [--name NAME] [--] [<path>]
```


### `path`

Het pad naar een bestaande SSH-openbare sleutel


### `--name`

Een naam om de sleutel te identificeren

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `ssh-key:delete`

Een SSH-toets verwijderen

```bash
magento-cloud ssh-key:delete [<id>]
```


### `id`

De id van de SSH-toets die moet worden verwijderd


### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `ssh-key:list`

Een lijst met SSH-sleutels in uw account ophalen

```bash
magento-cloud ssh-keys [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: id*, title*, path*, vingerafdruk (* = standaardkolommen). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `subscription:info`

Abonnementseigenschappen lezen of wijzigen

```bash
magento-cloud subscription:info [-s|--id ID] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<property>] [<value>]
```


### `property`

De naam van de eigenschap


### `value`

Een nieuwe waarde voor de eigenschap instellen


### `--id`, `-s`

Abonnement-id

- Vereist een waarde

### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `tunnel:close`

SSH-tunnels sluiten

```bash
magento-cloud tunnel:close [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--all`, `-a`

Alle tunnels sluiten

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `tunnel:info`

Relatie-informatie voor SSH-tunnels weergeven

```bash
magento-cloud tunnel:info [-P|--property PROPERTY] [-c|--encode] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--property`, `-P`

De relatie-eigenschap die moet worden weergegeven

- Vereist een waarde

### `--encode`, `-c`

Uitvoer als base64-gecodeerde JSON

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `tunnel:list`

Lijst SSH-tunnels

```bash
magento-cloud tunnels [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--all`, `-a`

Alle tunnels weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: poort*, project*, omgeving*, app*, relatie*, url (* = standaardkolommen). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `tunnel:open`

SSH-tunnels openen naar de relaties van een app

```bash
magento-cloud tunnel:open [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE]
```

### `--gateway-ports`, `-g`

Verre gastheren toestaan om met lokale door:sturen havens te verbinden

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `tunnel:single`

Eén SSH-tunnel openen voor een app-relatie

```bash
magento-cloud tunnel:single [--port PORT] [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE]
```

### `--port`

De lokale poort

- Vereist een waarde

### `--gateway-ports`, `-g`

Verre gastheren toestaan om met lokale door:sturen havens te verbinden

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

### `--relationship`, `-r`

De de dienstverhouding om te gebruiken

- Vereist een waarde

### `--identity-file`, `-i`

Een SSH-identiteit (persoonlijke sleutel) die moet worden gebruikt

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `user:add`

Een gebruiker toevoegen aan het project

```bash
magento-cloud user:add [-r|--role ROLE] [--force-invite] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```


### `email`

Het e-mailadres van de gebruiker


### `--role`, `-r`

De projectrol van de gebruiker (&#39;admin&#39; of &#39;viewer&#39;) of de rol van het type omgeving (bijvoorbeeld &#39;staging:contributor&#39; of &#39;production:viewer&#39;). Als u een gebruiker uit een omgevingstype wilt verwijderen, stelt u de rol in op Geen. De tekens % of * kunnen worden gebruikt als een jokerteken voor het omgevingstype, bijvoorbeeld &#39;%:viewer&#39; om de gebruiker de rol &#39;viewer&#39; te geven voor alle typen. De rol kan worden afgekort, bijvoorbeeld &quot;production:v&quot;.

- Standaard: `[]`
- Vereist een waarde

### `--force-invite`

Een uitnodiging verzenden, zelfs als er al een is verzonden

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `user:delete`

Een gebruiker verwijderen uit het project

```bash
magento-cloud user:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] <email>
```


### `email`

Het e-mailadres van de gebruiker

- Vereist

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `user:get`

Rollen van gebruikers weergeven

```bash
magento-cloud user:get [-l|--level LEVEL] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [-r|--role ROLE] [--] [<email>]
```


### `email`

Het e-mailadres van de gebruiker


### `--level`, `-l`

Rolniveau (&#39;project&#39; of &#39;milieu&#39;)

- Vereist een waarde

### `--pipe`

De rol uitvoeren die moet worden stopgezet (nadat eventuele wijzigingen zijn aangebracht)

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--role`, `-r`

[Vervangen: gebruik gebruiker:update om de rol(en) van een gebruiker te wijzigen]

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `user:list`

Projectgebruikers weergeven

```bash
magento-cloud users [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: email*, name*, role*, id*, allowed_at, update_at (* = standaardkolommen). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `user:update`

Gebruikersrol(s) voor een project bijwerken

```bash
magento-cloud user:update [-r|--role ROLE] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```


### `email`

Het e-mailadres van de gebruiker


### `--role`, `-r`

De projectrol van de gebruiker (&#39;admin&#39; of &#39;viewer&#39;) of de rol van het type omgeving (bijvoorbeeld &#39;staging:contributor&#39; of &#39;production:viewer&#39;). Als u een gebruiker uit een omgevingstype wilt verwijderen, stelt u de rol in op Geen. De tekens % of * kunnen worden gebruikt als een jokerteken voor het omgevingstype, bijvoorbeeld &#39;%:viewer&#39; om de gebruiker de rol &#39;viewer&#39; te geven voor alle typen. De rol kan worden afgekort, bijvoorbeeld &quot;production:v&quot;.

- Standaard: `[]`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `variable:create`

Een variabele maken

```bash
magento-cloud variable:create [-u|--update] [-l|--level LEVEL] [--name NAME] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--prefix PREFIX] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<name>]
```


### `name`

De variabelenaam


### `--update`, `-u`

De variabele bijwerken als deze al bestaat

- Standaard: `false`
- Accepteert geen waarde

### `--level`, `-l`

Het niveau waarop de variabele moet worden ingesteld (&#39;project&#39; of &#39;omgeving&#39;)

- Vereist een waarde

### `--name`

De variabelenaam

- Vereist een waarde

### `--value`

De waarde van de variabele

- Vereist een waarde

### `--json`

Geeft aan of de waarde van de variabele JSON-indeling heeft

- Standaard: `false`
- Vereist een waarde

### `--sensitive`

Of de waarde van de variabele gevoelig is

- Standaard: `false`
- Vereist een waarde

### `--prefix`

Het voorvoegsel van de variabelenaam dat het type kan bepalen, bijvoorbeeld &#39;env&#39;. Alleen van toepassing als de naam nog geen voorvoegsel bevat. (bijvoorbeeld &quot;none&quot; of &quot;env:&quot;)

- Standaard: `none`
- Vereist een waarde

### `--enabled`

Of de variabele op het milieu zou moeten worden toegelaten

- Standaard: `true`
- Vereist een waarde

### `--inheritable`

Of de variabele overerfbaar is door onderliggende omgevingen

- Standaard: `true`
- Vereist een waarde

### `--visible-build`

Of de variabele zichtbaar zou moeten zijn in bouwstijltijd

- Vereist een waarde

### `--visible-runtime`

Of de variabele zichtbaar moet zijn bij uitvoering

- Standaard: `true`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `variable:delete`

Een variabele verwijderen

```bash
magento-cloud variable:delete [-l|--level LEVEL] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

De variabelenaam

- Vereist

### `--level`, `-l`

Variabel niveau (&#39;project&#39;, &#39;milieu&#39;, &#39;p&#39; of &#39;e&#39;)

- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `variable:get`

Een variabele weergeven

```bash
magento-cloud vget [-P|--property PROPERTY] [-l|--level LEVEL] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--pipe] [--] [<name>]
```


### `name`

De naam van de variabele


### `--property`, `-P`

Eén variabele-eigenschap weergeven

- Vereist een waarde

### `--level`, `-l`

Variabel niveau (&#39;project&#39;, &#39;milieu&#39;, &#39;p&#39; of &#39;e&#39;)

- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--pipe`

[Vervangen optie] Alleen de waarde van de variabele uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `variable:list`

Lijstvariabelen

```bash
magento-cloud variables [-l|--level LEVEL] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--level`, `-l`

Variabel niveau (&#39;project&#39;, &#39;milieu&#39;, &#39;p&#39; of &#39;e&#39;)

- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: is_enabled, level, name, value. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `variable:update`

Een variabele bijwerken

```bash
magento-cloud variable:update [--allow-no-change] [-l|--level LEVEL] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

De variabelenaam

- Vereist

### `--allow-no-change`

Retourneren geslaagd (nulafsluitcode) als er geen wijzigingen zijn opgegeven

- Standaard: `false`
- Accepteert geen waarde

### `--level`, `-l`

Variabel niveau (&#39;project&#39;, &#39;milieu&#39;, &#39;p&#39; of &#39;e&#39;)

- Vereist een waarde

### `--value`

De waarde van de variabele

- Vereist een waarde

### `--json`

Geeft aan of de waarde van de variabele JSON-indeling heeft

- Standaard: `false`
- Vereist een waarde

### `--sensitive`

Of de waarde van de variabele gevoelig is

- Standaard: `false`
- Vereist een waarde

### `--enabled`

Of de variabele op het milieu zou moeten worden toegelaten

- Standaard: `true`
- Vereist een waarde

### `--inheritable`

Of de variabele overerfbaar is door onderliggende omgevingen

- Standaard: `true`
- Vereist een waarde

### `--visible-build`

Of de variabele zichtbaar zou moeten zijn in bouwstijltijd

- Vereist een waarde

### `--visible-runtime`

Of de variabele zichtbaar moet zijn bij uitvoering

- Standaard: `true`
- Vereist een waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde


## `worker:list`

Een lijst met alle geïmplementeerde workers ophalen

```bash
magento-cloud workers [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

### `--pipe`

Alleen een lijst met namen van workers uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--project`, `-p`

De project-id of URL

- Vereist een waarde

### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: opdrachten, naam, type. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standaard: `false`
- Accepteert geen waarde

