---
title: Web, eigenschap
description: Zie voorbeelden over hoe u de webeigenschap kunt configureren in de [!DNL Commerce] toepassingsconfiguratiebestand.
feature: Cloud, Configuration
exl-id: 2ca94908-6fe1-42fd-bc3b-ef2dd473f1bb
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Web, eigenschap

De `web` eigenschap definieert hoe uw toepassing aan het web (in HTTP) wordt blootgesteld, bepaalt hoe de webtoepassing inhoud dient en bepaalt hoe de toepassingscontainer op binnenkomende aanvragen reageert door regels in te stellen op elke locatie _blok_. Een blok vertegenwoordigt een absoluut pad met een slash (`/`).

```yaml
web:
    locations:
        "/":
            # The public directory of the app, relative to its root.
```

U kunt uw `locations` configuratie die de volgende zeer belangrijke waarden voor elk gebruikt `locations` blok:

| Kenmerk | Beschrijving |
| :--- | :--- |
| `allow` | Serveer bestanden die niet overeenkomen met de regels. Standaardwaarde = `true` |
| `expires` | Stel het aantal seconden in dat u inhoud in de browser in de cache wilt plaatsen. Met deze toets wordt de `cache-control` en `expires` kopteksten voor statische inhoud. Als deze waarde niet is ingesteld, wordt `expires` instructies en de resulterende kopteksten worden niet opgenomen wanneer het dienen van statische inhoudsdossiers. Een negatief 1 (`-1`) resulteert niet in caching en is de standaardwaarde. U kunt tijdwaarde met de volgende eenheden uitdrukken:  `ms` (milliseconden), `s` (seconden), `m` (minuten), `h` (uren), `d` (dagen), `w` (weken), `M` (maanden, 30d), of `y` (jaren, 365 quinquies) |
| `headers` | Aangepaste koppen instellen, zoals `X-Frame-Options`, voor statische inhoud die vanaf deze locatie wordt aangeboden. |
| `index` | Maak een lijst van de statische dossiers om uw toepassing te dienen, zoals `index.html` bestand. Deze sleutel verwacht een inzameling. Dit werkt alleen als toegang tot het bestand of de bestanden door de `allow` of `rules` sleutel voor deze locatie. |
| `rules` | Geef overschrijvingen voor een locatie op. Gebruik een reguliere expressie die overeenkomt met een aanvraag. Als een inkomend verzoek de regel aanpast, dan wordt de regelmatige behandeling van het verzoek met voeten getreden door de sleutels die in de regel worden gebruikt. |
| `passthru` | Stel de URL in die wordt gebruikt voor het geval dat een statisch bestand of PHP-bestand niet wordt gevonden. Deze URL is doorgaans de voorste controller voor uw toepassingen, zoals `/index.php` of `/app.php`. |
| `root` | Stel het pad in ten opzichte van de hoofdmap van de toepassing die op het web wordt weergegeven. De openbare map (locatie &quot;/&quot;) voor een Cloud-project is standaard ingesteld op &quot;pub&quot;. |
| `scripts` | Het laden van scripts op deze locatie toestaan. Stel de waarde in op `true` om scripts toe te staan. |

De standaardconfiguratie staat het volgende toe:

- Van het wortel (`/`) pad, alleen web en media kunnen worden geopend
- Van de `~/pub/static` en `~/pub/media` paden, bestanden die u kunt openen

In het volgende voorbeeld wordt de standaardconfiguratie getoond in de `.magento.app.yaml` bestand voor een set webtoegankelijke locaties die aan een item in het dialoogvenster  [`mounts` eigenschap](properties.md#mounts):

```yaml
 # The configuration of app when it is exposed to the web.
web:
    locations:
        "/":
            # The public directory of the app, relative to its root.
            root: "pub"
            # The front-controller script to send non-static requests to.
            passthru: "/index.php"
            index:
                - index.php
            expires: -1
            scripts: true
            allow: false
            rules:
                \.(css|js|map|hbs|gif|jpe?g|png|tiff|wbmp|ico|jng|bmp|svgz|midi?|mp?ga|mp2|mp3|m4a|ra|weba|3gpp?|mp4|mpe?g|mpe|ogv|mov|webm|flv|mng|asx|asf|wmv|avi|ogx|swf|jar|ttf|eot|woff|otf|html?)$:
                    allow: true
                ^/sitemap(.*)\.xml$:
                    passthru: "/media/sitemap$1.xml"
        "/media":
            root: "pub/media"
            allow: true
            scripts: false
            expires: 1y
            passthru: "/get.php"
        "/static":
            root: "pub/static"
            allow: true
            scripts: false
            expires: 1y
            passthru: "/front-static.php"
            rules:
                ^/static/version\d+/(?<resource>.*)$:
                    passthru: "/static/$resource"
```

>[!NOTE]
>
>Dit voorbeeld toont de standaardWebconfiguratie voor een project van de Wolk dat wordt gevormd om één enkel domein te steunen. Voor een project dat ondersteuning voor meerdere websites of winkels vereist, `web` de configuratie moet opstelling zijn om gedeelde domeinen te steunen. Zie [Locaties voor gedeelde domeinen configureren](../store/multiple-sites.md#configure-locations-for-shared-domains).
