---
title: Verbindingen vormen
description: Leer hoe u de routes definieert voor binnenkomende HTTPS-aanvragen voor de Adobe Commerce in omgevingen met cloudinfrastructuren.
feature: Cloud, Configuration, Routes
exl-id: a33797e5-14cc-45eb-a048-96180b872a4a
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Verbindingen vormen

De `routes.yaml` in het `.magento/routes.yaml` Deze directory definieert routes voor uw Adobe Commerce op omgevingen voor integratie, staging en productie van cloudinfrastructuur. Routes bepalen hoe de toepassing binnenkomende HTTP- en HTTPS-aanvragen verwerkt.

De standaardwaarde `routes.yaml` het dossier specificeert de routesjablonen voor de verwerking van HTTP- verzoeken als HTTPS op projecten die één enkel standaarddomein hebben en op projecten die voor veelvoudige domeinen worden gevormd:

```yaml
"http://{default}/":
    type: upstream
    upstream: "mymagento:http"
"http://{all}/":
    type: upstream
    upstream: "mymagento:http"
```

Gebruik de `magento-cloud` CLI om een lijst van de gevormde routes te bekijken:

```bash
magento-cloud environment:routes

+-------------------+----------+---------------+
| Route             | Type     | To            |
+-------------------+----------+---------------+
| http://{default}/ | upstream | mymagento     |
+-------------------+----------+---------------+
```

## Configuratie-updates voor Pro-omgevingen

{{pro-self-service-warning}}

## Route templates

De `routes.yaml` file is een lijst van getemplated routes en hun configuraties. U kunt de volgende placeholders in routesjablonen gebruiken:

- De `{default}` placeholder vertegenwoordigt de gekwalificeerde domeinnaam die als gebrek voor het project wordt gevormd.

  Bijvoorbeeld een project met het standaarddomein `example.com` en de volgende routesjablonen:

  ```text
  https://www.{default}/
  https://{default}/blog
  ```

  Deze sjablonen verwijzen naar de volgende URL&#39;s in een productieomgeving:

  ```text
  https://www.example.com/
  https://example.com/blog
  ```

- De `{all}` placeholder vertegenwoordigt alle domeinnamen die voor het project worden gevormd.

  Een project met `example.com` en `example1.com` domeinen met de volgende routesjablonen:

  ```text
  https://www.{all}/
  
  https://{all}/blog
  ```

  Deze malplaatjes lossen aan de volgende routes voor alle domeinen in het project op:

  ```text
  https://www.example.com/
  
  https://www.example1.com/
  
  https://example.com/blog
  
  https://example1.com/blog
  ```

  De `{all}` placeholder is nuttig voor projecten die voor veelvoudige domeinen worden gevormd. In een niet-productiesector: `{all}` wordt vervangen met project ID en milieu ID voor elk domein.

  Als een project geen gevormde domeinen heeft, die tijdens ontwikkeling gemeenschappelijk is, `{all}` plaatsaanduiding gedraagt zich op dezelfde manier als de `{default}` plaatsaanduiding.

Adobe Commerce genereert ook routes voor elke actieve integratieomgeving. Voor integratieomgevingen geldt het `{default}` tijdelijke aanduiding wordt vervangen door de volgende domeinnaam:

```text
[branch]-[per-environment-random-string]-[project-id].[region].magentosite.cloud
```

Bijvoorbeeld de `refactorcss` vertakking voor de `mswy7hzcuhcjw` in het `us` cluster heeft het volgende domein:

```text
https://refactorcss-oy3m2pq-mswy7hzcuhcjw.us.magentosite.cloud/
```

>[!NOTE]
>
>Als uw project van de Wolk veelvoudige opslag steunt, volg de instructies van de routerconfiguratie voor [meerdere websites of winkels](../store/multiple-sites.md).

### Sluitslash

De definities van de route bevatten een het slepen schuine streep om op een omslag of een folder te wijzen; nochtans, kan de zelfde inhoud met of zonder een het slepen schuine streep worden gediend. De volgende URL&#39;s zijn hetzelfde, maar kunnen worden geïnterpreteerd als _twee verschillende_ URL&#39;s:

```text
https://www.example.com/blog/

https://www.example.com/blog
```

>[!TIP]
>
>Het is aan te raden een slash voor mappen te gebruiken, maar de methode die u kiest, is belangrijk om **consistent blijven** om het genereren van twee locaties te voorkomen.

## Routeprotocollen

Alle omgevingen ondersteunen automatisch HTTP en HTTPS.

- Als de configuratie alleen de HTTP-route opgeeft, worden automatisch HTTPS-routes gemaakt, zodat de site vanuit zowel HTTP als HTTPS kan worden bediend zonder dat omleidingen nodig zijn.

  Bijvoorbeeld een project met het standaarddomein `example.com` en het volgende routesjabloon:

  ```text
  http://{default}/
  ```

  Deze sjabloon verhelpt naar de volgende URL&#39;s:

  ```text
  http://example.com/
  
  https://example.com/
  ```

- Als de configuratie alleen de HTTPS-route opgeeft, leiden alle HTTP-aanvragen om naar HTTPS.

  Bijvoorbeeld een project met het standaarddomein `example.com` met het volgende routesjabloon:

  ```text
  https://{default}/
  ```

  Deze sjabloon wordt omgezet naar de volgende URL:

  ```text
  https://example.com/
  ```

  Het verwerkt ook de volgende omleiding:

  `http://example.com/` ==> `https://example.com/`

Geef alle pagina&#39;s weer via TLS. Voor deze configuratie, moet u redirects voor al unencrypted verzoek aan het equivalent TLS vormen gebruikend één van de volgende methodes:

- Wijzig het protocol in HTTPS in het dialoogvenster `routes.yaml` bestand.

  ```yaml
  "https://{default}/":
      type: upstream
      upstream: "mymagento:http"
  "https://{all}/":
      type: upstream
      upstream: "mymagento:http"
  ```

- Schakel voor Staging- en Productomgevingen de optie [TLS snel forceren](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/redirect-http-to-https-for-all-pages-on-cloud-force-tls.html) van de interface van Admin. Wanneer u deze optie gebruikt, handelt u snel de omleiding naar HTTPS af, zodat u niet de `routes.yaml` configuratie.

## Routopties

Vorm elke route afzonderlijk gebruikend de volgende eigenschappen:

| Eigenschap | Beschrijving |
| ---------------- | ----------- |
| `type: upstream` | Dient een toepassing uit. Het heeft ook een `upstream` eigenschap die de naam van de toepassing opgeeft (zoals gedefinieerd in `.magento.app.yaml`) gevolgd door de `:http` eindpunt. |
| `type: redirect` | Omleidt aan een andere route. Het wordt gevolgd door de `to` eigenschap, die een HTTP-omleiding is naar een andere route die door de sjabloon ervan wordt aangegeven. |
| `cache:` | Besturingselementen [caching voor de route](caching.md). |
| `redirects:` | Besturingselementen [omleidingsregels](redirects.md). |
| `ssi:` | Besturingselementen die [Include-bestanden op de server](server-side-includes.md). |

## Eenvoudige routes

In de volgende voorbeelden, leidt de routeconfiguratie het apex domein en `www` subdomein voor de `mymagento` toepassing. Deze route leidt HTTPS- verzoeken niet om.

**Voorbeeld 1:**

```yaml
"http://{default}/":
    type: upstream
    upstream: "mymagento:http"

"http://www.{default}/":
    type: redirect
    to: "http://{default}/"
```

In dit voorbeeld, volgt het verzoek die deze regels verplettert:

- De server reageert rechtstreeks op aanvragen met het volgende URL-patroon:

  ```text
  http://example.com/path
  ```

- De server geeft een _301 omleiding_ voor aanvragen met het volgende URL-patroon:

  ```text
  http://www.example.com/mypath
  ```

  Deze verzoeken worden bijvoorbeeld omgeleid naar het ex-domein:

  ```text
  http://example.com/mypath
  ```

In het volgende voorbeeld, richt de routeconfiguratie geen URLs van het www domein aan het apex domein. In plaats daarvan, worden de verzoeken gediend van zowel www als apex domein.

**Voorbeeld 2:**

```yaml
"http://{default}/":
    type: upstream
    upstream: "mymagento:http"

"http://www.{default}/":
    type: upstream
    upstream: "mymagento:http"
```

## Jokerroutes

Adobe Commerce op cloudinfrastructuur ondersteunt jokertekenroutes, zodat u meerdere subdomeinen aan dezelfde toepassing kunt toewijzen. Dit werkt voor omleiding en stroomopwaartse routes. U voegt een sterretje (\*) toe aan de route. Met de volgende routes naar bijvoorbeeld dezelfde toepassing:

- `*.example.com`
- `www.example.com`
- `blog.example.com`
- `us.example.com`

Dit werkt als een &#39;catch-all&#39;-domein in een live omgeving.

### Het verpletteren van een niet in kaart gebracht domein

U kunt met een punt naar een systeem leiden dat niet is toegewezen aan een domein (`.`) om het subdomein te scheiden.

**Voorbeeld:**

Een project met een `add-theme` vertakking leidt naar volgende URL:

```text
http://add-theme-projectID.us.magento.com/
```

Als u het volgende routesjabloon definieert:

```text
http://www.{default}/
```

De route lost aan volgende URL op:

```text
http://www.add-theme-projectID.us.magento.com/
```

U kunt elk subdomein invoegen voordat de punt en de route worden omgezet.

**Voorbeeld:**

Bepaal het volgende routesjabloon:

```text
http://*.{default}/
```

Deze sjabloon verhelpt beide volgende URL&#39;s:

```text
http://foo.add-theme-projectID.us.magentosite.cloud/
http://bar.add-theme-projectID.us.magentosite.cloud/
```

U kunt het routepatroon voor niet in kaart gebrachte domeinen bekijken door een verbinding van SSH aan het milieu te vestigen, en het gebruiken van `magento-cloud` CLI om van de routes een lijst te maken:

```terminal
web@mymagento.0:~$ vendor/bin/ece-tools env:config:show routes

Magento Cloud Routes:
+------------------------------------------+--------------------------------------------------------------+
| Route configuration                      | Value                                                        |
+------------------------------------------+--------------------------------------------------------------+
| http://www.add-theme-projectID.us.magento.com/:                                                         |
+------------------------------------------+--------------------------------------------------------------+
| primary                                  | false                                                        |
| id                                       | null                                                         |
| attributes                               |                                                              |
| type                                     | upstream                                                     |
| to                                       | mymagento                                                    |
| original_url                             | https:/{default}/                                            |
+------------------------------------------+--------------------------------------------------------------+
| https://*.add-theme-projectID.us.magentosite.cloud/:                                                    |
+------------------------------------------+--------------------------------------------------------------+
| primary                                  | false                                                        |
| id                                       | null                                                         |
| attributes                               |                                                              |
| type                                     | upstream                                                     |
| to                                       | mymagento                                                    |
| original_url                             | https://*.{default}/                                         |
+------------------------------------------+--------------------------------------------------------------+
```

## Omleiding en caching

Meer in detail besproken [Omleiding](redirects.md)kunt u complexe omleidingsregels beheren, zoals _gedeeltelijke omleiding_, en specificeer regels voor op route-gebaseerd [caching](caching.md):

```yaml
https://www.{default}/:
    type: redirect
    to: https://{default}/
https://{default}/:
    cache:
        cookies: [""]
        default_ttl: 0
        enabled: true
        headers:
            - Accept
            - Accept-Language
    ssi:
        enabled: false
    type: upstream
    upstream: mymagento:http
```
