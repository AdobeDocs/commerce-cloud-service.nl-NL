---
title: Omleiding
description: Leer hoe u omleidingsregels voor uw Adobe Commerce beheert voor een cloudinfragment.
feature: Cloud, Routes
exl-id: 7089a790-6341-4443-990a-df42091f0680
source-git-commit: 649c11b111aa9c9105e54908bf9c6f48741f10e4
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Omleiding

Het beheren van omleidingsregels is een algemene vereiste voor webtoepassingen, vooral wanneer u inkomende koppelingen die in de loop der tijd zijn gewijzigd of verwijderd, niet wilt verliezen.

Hieronder ziet u hoe u de omleidingsregels voor uw Adobe Commerce kunt beheren voor projecten met cloudinfrastructuur met behulp van de `routes.yaml` configuratiebestand. Als de omleidingsmethodes in dit onderwerp worden besproken niet voor u werken, kunt u caching kopballen gebruiken om het zelfde ding te doen.

{{route-placeholder}}

## Updates voor Pro-omgevingen

{{pro-self-service-warning}}

>[!WARNING]
>
>Voor Adobe Commerce voor projecten met cloudinfrastructuur, kunt u een groot aantal niet-regex-omleidingen configureren en herschrijven in de `routes.yaml` kan prestatieproblemen veroorzaken. Als uw `routes.yaml` bestand is 32 kB of groter, offload de niet-regex omleiding en herschrijft het bestand naar Fastly. Zie [Offload niet-regex herleidt naar Fastly in plaats van Nginx (routes)](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/offload-non-regex-redirects-to-fastly-instead-of-nginx-routes.html) in de _Adobe Commerce Help Center_.

## Hele-routeomleidingen

Gebruikend volledig-routeherleidingen, kunt u eenvoudige routes bepalen gebruikend `routes.yaml` bestand. U kunt bijvoorbeeld van een ex-domein naar een `www` subdomein als volgt:

```yaml
http://{default}/:
    type: redirect
    to: http://www.{default}/
```

## Gedeeltelijke-routeomleidingen

In de `.magento/routes.yaml` bestand, kunt u gedeeltelijke omleidingsregels toevoegen aan bestaande routes die op patroon aanpassing worden gebaseerd:

```yaml
http://{default}/:
    redirects:
        expires: 1d
        paths:
          "/from": { to: "http://example.com/" }
          "/regexp/(.*)/matching": { to: "http://example.com/$1", regexp: true }
```

Gedeeltelijke omleidingen werken met elk type route, inclusief routes die rechtstreeks door de toepassing worden bediend.

Twee toetsen zijn beschikbaar onder `redirects`:

- **verloopt**—Optioneel: hiermee wordt opgegeven hoeveel tijd er nodig is om de omleiding in de browser in de cache op te slaan. Voorbeelden van geldige waarden zijn `3600s`, `1d`, `2w`, `3m`.

- **paden**—Één of meerdere zeer belangrijk-waardeparen die de configuratie voor gedeeltelijk-routeomleidingsregels specificeren.

  Voor elke omleidingsregel is de sleutel een expressie om aanvraagpaden voor omleiding te filteren. De waarde is een object dat de doelbestemming voor de omleiding en opties voor de verwerking van de omleiding aangeeft.

  Het object value heeft de volgende eigenschappen:

  | Eigenschap | Beschrijving |
  | ---------- | ----------- |
  | `to` | Vereist, een gedeeltelijk absolute weg, URL met protocol en gastheer, of een patroon dat de doelbestemming voor de omleidingsregel specificeert. |
  | `regexp` | Optioneel, standaardinstellingen `false`. Geeft aan of de padsleutel moet worden geïnterpreteerd als een reguliere PCRE-expressie. |
  | `prefix` | Hiermee geeft u aan of de omleiding van toepassing is op zowel het pad als alle onderliggende paden, of alleen op het pad zelf. Standaardwaarden: `true`. Deze waarde wordt niet ondersteund als `regexp` is `true`. |
  | `append_suffix` | Hiermee bepaalt u of het achtervoegsel wordt overgedragen met de omleiding. Standaardwaarden: `true`. Deze waarde wordt niet ondersteund als de `regexp` key is `true` of* als de `prefix` key is `false`. |
  | `code` | Geeft de HTTP-statuscode op. Geldige statuscodes zijn [`301` (Permanent verplaatst)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.2), [`302`](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.3), [`307`](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.8), en [`308`](https://www.rfc-editor.org/rfc/rfc7238). Standaardwaarden: `302`. |
  | `expires` | Optioneel: hiermee geeft u aan hoeveel tijd u de omleiding in de browser in de cache wilt plaatsen. Wordt standaard ingesteld op `expires` waarde die rechtstreeks onder de `redirects` sleutel, maar op dit niveau kunt u de geheim voorgeheugenvervalsing voor individuele gedeeltelijke omleiding verfijnen. |

## Voorbeelden van gedeeltelijke-routeomleidingen

De volgende voorbeelden tonen hoe te om gedeeltelijk-route te specificeren richt in `routes.yaml` bestand met behulp van diverse `paths` configuratieopties.

### Standaardovereenkomend expressiepatroon

Gebruik het volgende formaat om verzoeken te vormen die van de omleiding op een regelmatige uitdrukking worden gebaseerd.

```yaml
http://{default}/:
    type: upstream
    redirects:
    paths:
        "/regexp/(.*)/match": { to: "http://example.com/$1", regexp: true }
```

Met deze configuratiefilters worden paden aangevraagd tegen een reguliere expressie en worden overeenkomstige aanvragen omgeleid naar `https://example.com`. Bijvoorbeeld een verzoek om `https://example.com/regexp/a/b/c/match` omleiding naar `https://example.com/a/b/c`.

### Overeenkomende patroon voorvoegsel

Gebruik de volgende indeling om aanvragen voor paden die met een opgegeven voorvoegselpatroon beginnen, om te leiden.

```yaml
http://{default}/:
    type: upstream
    redirects:
    paths:
        "/from": { to: "https://{default}/to", prefix: true }
```

Deze configuratie werkt als volgt:

- Hiermee worden aanvragen omgeleid die overeenkomen met het patroon `/from` naar het pad `http://{default}/to`.

- Hiermee worden aanvragen omgeleid die overeenkomen met het patroon `/from/another/path` tot `https://{default}/to/another/path`.

- Als u de `prefix` eigenschap aan `false`, aanvragen die overeenkomen met de `/from` patroon leidt tot omleiding, maar aanvragen die overeenkomen met de `/from/another/path` patroon niet.

### Overeenkomende patroon achtervoegsel

Gebruik het volgende formaat om omleidingsverzoeken te vormen die het wegachtervoegsel van het verzoek aan de doelbestemming toevoegen:

```yaml
http://{default}/:
    type: upstream
    redirects:
    paths: "/from": { to: "https://{default}/to", append_suffix: false }
```

Deze configuratie werkt als volgt:

- Hiermee worden aanvragen omgeleid die overeenkomen met het patroon `/from/path/suffix` naar het pad `https://{default}/to`.

- Als u de `append_suffix` eigenschap aan `true`, dan verzoeken die aanpassen `/from/path/suffix`  omleiden naar het pad `https://{default}/to/path/suffix`.

### Padspecifieke cacheconfiguratie

Gebruik de volgende notatie om de tijd aan te passen om een omleiding van een specifiek pad in de cache op te slaan:

```yaml
http://{default}/:
    type: upstream
    redirects:
    expires: 1d
    paths:
        "/from": { to: "https://example.com/" }
        "/here": { to: "https://example.com/there", expires: "2w" }
```

Deze configuratie werkt als volgt:

- Omleiding vanaf het eerste pad (`/from`) gedurende één dag in cache worden geplaatst.

- Omleiding vanaf het tweede pad (`/here`) gedurende twee weken in cache worden opgeslagen.
