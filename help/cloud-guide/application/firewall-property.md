---
title: Firewall, eigenschap
description: Zie voorbeelden op hoe te om het firewallbezit in het dossier van de de toepassingsconfiguratie van de Handel te vormen.
feature: Cloud, Configuration, Security
exl-id: f169c008-c62a-41b7-a98d-cccd81c7291a
source-git-commit: 74d88560db3b65294673a1e1827f9cea098d707a
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---

# Firewall, eigenschap

>[!IMPORTANT]
>
>Alleen starter-projecten

Voor de projecten van de Aanzet, `firewall` eigenschap voegt een _uitgaand_ aan de toepassing. Deze firewall heeft geen effect op binnenkomende aanvragen. Hiermee wordt gedefinieerd welke `tcp` uitgaande verzoeken kunnen _verlaten_ een Adobe Commerce-site. Dit wordt egress-filtering genoemd. De uitgaande firewall filtert wat kan binnendringen-weg of uw plaats ontsnappen. Door te beperken wat er kan ontsnappen, wordt een krachtig beveiligingsprogramma aan de server toegevoegd.

## Standaardbeperkingsbeleid

De firewall verstrekt twee standaardbeleid om uitgaand verkeer te controleren: `allow` en `deny`. De `allow` beleid _toestaat_ al uitgaand verkeer door gebrek. En de `deny` beleid _ontzegging_ al uitgaand verkeer door gebrek. Maar wanneer u een regel toevoegt, wordt het standaardbeleid met voeten getreden, en de firewallblokken **alles** het uitgaande verkeer niet toegestaan door de regel.

Voor de plannen van de Aanzet, wordt het standaardbeleid geplaatst aan `allow`. Dit het plaatsen zorgt ervoor dat al uw huidige uitgaande verkeer unlocked blijft tot u uw uitgang-filtrerende regels toevoegt. Het standaardbeleid kan worden ingesteld op `deny` op verzoek.

**Uw standaardbeleid controleren**:

```bash
magento-cloud p:curl --project PROJECT_ID /settings | grep -i outbound
```

Tenzij u `deny` voor uw beleid, zou het bevel uw beleid moeten tonen dat aan wordt geplaatst `allow`:

```terminal
"outbound_restrictions_default_policy": "allow"
```

>[!NOTE]
>
>**Key taaway**: Wanneer u een uitgaande regel toevoegt, blokkeert u al uitgaand verkeer behalve de domeinen, IP adressen, of havens u aan de regel toevoegt. Het is dus belangrijk dat er een volledige uitgaande lijst wordt gedefinieerd en getest voordat deze aan uw productiesite wordt toegevoegd.

## Firewall-opties

De volgende voorbeeldconfiguratie in de `.magento.app.yaml` het dossier toont al `firewall` opties die u kunt gebruiken om regels voor het filtreren van de uitgang toe te voegen.

```yaml
firewall:
    outbound:
        - # Common accessed domains
            domains:
                - newrelic.com
                - fastly.com
                - magento.com
                - magentocommerce.com
                - google.com
            ports:
                - 80
                - 443
            protocol: tcp # Can be omitted from rules.

        - # Adobe Stock integration
            domains:
                - account.adobe.com
                - stock.adobe.com
                - console.adobe.io
            ports:
                - 80
                - 443

        - # Payment services
            domains:
                - braintreepayments.com
                - paypal.com
            ports:
                - 80
                - 443

        - # Shipping services
            domains:
                - ups.com
                - usps.com
                - fedex.com
                - dhl.com
            ports:
                - 80
                - 443

        - # Vertex Integrated Address Cleansing
            domains:
                - mgcsconnect.vertexsmb.com
            ports:
                - 80
                - 443

        - # New Relic networks
            ips:
                - 162.247.240.0/22 # US region accounts
                - 185.221.84.0/22 # EU region accounts
            ports:
                - 443

        - # New Relic endpoints
            domains:
                - collector.newrelic.com, # US region accounts
                - collector.eu01.nr-data.net # EU region accounts
            ports:
                - 443

        - # Fastly IP ranges
            ips:
                - 23.235.32.0/20
                - 43.249.72.0/22
                - 103.244.50.0/24
                - 103.245.222.0/23
                - 103.245.224.0/24
                - 104.156.80.0/20
                - 146.75.0.0/16
                - 151.101.0.0/16
                - 157.52.64.0/18
                - 167.82.0.0/17
                - 167.82.128.0/20
                - 167.82.160.0/20
                - 167.82.224.0/20
                - 172.111.64.0/18
                - 185.31.16.0/22
                - 199.27.72.0/21
                - 199.232.0.0/16
            ports:
                - 80
                - 443
```

## Filterregels voor eieren

De uitgaande firewallconfiguraties worden samengesteld uit regels. U kunt zoveel regels definiëren als u nodig hebt. De voorschriften zijn als volgt.

**Elke regel:**

- Moet beginnen met een afbreekstreepje (`-`). Als u een opmerking op dezelfde regel toevoegt, kunt u de ene regel beter documenteren en visueel van de volgende regel scheiden.
- U moet ten minste een van de volgende opties definiëren: `domains`, `ips`, of `ports`.
- Moet de `tcp` protocol. Omdat dit het standaardprotocol voor alle regels is, kunt u het van de regel weglaten.
- Kan definiëren `domains` of `ips`, maar niet beide in dezelfde regel.
- Kan omvatten `yaml` opmerkingen (`#`) en regeleinden om de toegestane domeinen, IP-adressen en poorten in te delen.

Elke regel gebruikt de volgende eigenschappen:

### `domains`

De `domains` optie staat een lijst van volledig - gekwalificeerde domeinnamen (FQDN) toe.

Als een regel definieert `domains` maar niet `ports`, staat de firewall domeinverzoeken op om het even welke haven toe.

### `ips`

De `ips` optie staat een lijst van IP adressen in de aantekening CIDR toe. U kunt enige IP adressen of waaiers van IP adressen specificeren.

Om één enkel IP adres te specificeren, voeg toe `/32` CIDR prefix aan het eind van uw IP adres:

```terminal
172.217.11.174/32  # google.com
```

Om een waaier van IP adressen te specificeren, gebruik [IP Waaier aan CIDR.](https://ipaddressguide.com/cidr) rekenmachine.

Als een regel definieert `ips` maar niet `ports`, staat de firewall IP verzoeken op om het even welke haven toe.

### `ports`

De `ports` optie staat een lijst van havens van 1 tot 65535 toe. Voor de meeste regels in het voorbeeld, havens `80` en `443` staan zowel HTTP- als HTTPS-aanvragen toe. Maar voor New Relic staan de regels alleen toegang toe tot domeinen en IP-adressen op de poort `443`, zoals aanbevolen in de documentatie van New Relic op [Netwerkverkeer](https://docs.newrelic.com/docs/new-relic-solutions/get-started/networks/#agents).

Als een regel alleen definieert `ports`, verleent de firewall toegang tot alle domeinen en IP adressen voor de bepaalde havens.

>[!NOTE]
>
>Poort `25`, wordt de SMTP-poort die e-mail moet verzenden altijd geblokkeerd, zonder uitzondering.

### `protocol`

Zoals vermeld, is TCP het gebrek en slechts protocol toegestaan voor regels. UDP en zijn havens worden niet toegestaan. Daarom kunt u de opdracht `protocol` van alle regels. Als u deze toch wilt opnemen, moet u de waarde instellen op `tcp`, zoals in de eerste regel van het voorbeeld wordt getoond.

## Domeinnamen zoeken die zijn toegestaan

Om u te helpen de domeinen identificeren om in uw uitgang-filtreren regels te omvatten, gebruik het volgende bevel om uw server te ontleden `dns.log` een lijst weergeven van alle DNS-verzoeken die uw site heeft geregistreerd:

```shell
awk '($5 ~/query/)' /var/log/dns.log | awk '{print $6}' | sort | uniq -c | sort -rn
```

Dit bevel toont ook DNS verzoeken die door uw uitgang-filtrerende regels werden gemaakt maar geblokkeerd. De uitvoer geeft niet aan welke domeinen zijn geblokkeerd, alleen dat er aanvragen zijn ingediend. De output toont geen verzoeken die gebruikend een IP adres worden gemaakt.

```terminal
Example output:

97 magento.com
93 magentocommerce.com
88 google.com
70 metadata.google.internal.0
70 metadata.google.internal
65 newrelic.com
56 fastly.com
17 mcprod-0vunku5xn24ip.ap-4.magentosite.cloud
6 advancedreporting.rjmetrics.com
```

Domeinen, in tegenstelling tot IP-adressen, zijn doorgaans specifieker en veiliger voor egress-filtering. Bijvoorbeeld, als u een IP adres voor de dienst toevoegt die een CDN gebruikt, staat u het IP adres voor CDN toe, die door honderden of duizenden andere domeinen kan worden gebruikt. Met één IP adres, kon u uitgaande toegang tot duizenden andere servers toestaan.

## Regels voor egress-filtering testen

Na het verzamelen van en het vormen van toegangsregels voor de domeinen en IP richt uw plaatsbehoeften, is het tijd om te duwen en te testen.

Om uw uitgang-filtrerende regels te testen:

1. Een shellscript maken van `curl` bevelen om tot de domeinen en IP adressen in uw regels toegang te hebben. Omvat bevelen die toegang tot domeinen en IP adressen testen die zouden moeten worden geblokkeerd.

1. Een `post_deploy` haak in uw `.magento.app.yaml` bestand om het script uit te voeren.

1. Druk op `firewall` configuratie en uw testmanuscript aan uw `integration` vertakking.

1. Onderzoek de `post_deploy` uitvoer van uw `curl` opdrachten.

1. Verfijn uw `firewall` regels, update uw `curl` script, commit, push en repeat.

### `curl` scriptvoorbeeld

```shell
# curl-tests-for-egress-filtering.sh

# Use the -v option to display connection details

# Check domain access
curl -v newrelic.com
curl -v fastly.com
curl -v magento.com
curl -v magentocommerce.com
curl -v google.com
curl -v account.adobe.com
curl -v stock.adobe.com
curl -v console.adobe.io
curl -v braintreepayments.com
curl -v paypal.com
curl -v ups.com
curl -v usps.com
curl -v fedex.com
curl -v dhl.com
curl -v devdocs.magento.com

# Check domain denials
curl -v amazon.com
curl -v facebook.com
curl -v twitter.com

# IP address access
...

# IP address denials
...
```

### `post_deploy` voorbeeld

```yaml
hooks:
    build: |
        set -e
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    deploy: "php ./vendor/bin/ece-tools run scenario/deploy.xml\n"
    post_deploy: |
        set -e
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
        echo "[$(date)] post-deploy hook end"
        ./curl-tests-for-egress-filtering.sh
        echo "[$(date)] curl finished"
```
