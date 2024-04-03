---
title: Caching
description: Leer hoe u caching inschakelt voor uw Adobe Commerce in omgevingen met cloudinfrastructuren.
feature: Cloud, Cache, Routes
exl-id: 4856aa94-2947-4dc8-b0d1-0960869dc39c
source-git-commit: 7b9c6a4cd17069c25455195bd8f273664b8a29eb
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Caching

U kunt caching in uw het projectmilieu van de wolkeninfrastructuur toelaten. Als u caching uitschakelt, dient Adobe Commerce de bestanden rechtstreeks.

{{route-placeholder}}

## Opslaan in cache instellen

Schakel caching in voor uw toepassing door cacheregels in te stellen in de `.magento/routes.yaml` bestand als volgt:

```yaml
http://{default}/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true
        headers: [ "Accept", "Accept-Language", "X-Language-Locale" ]
        cookies: ["*"]
        default_ttl: 60
```

## Route-based caching

Schakel fijnkorrelige caching in door caching-regels voor verschillende routes afzonderlijk in te stellen, zoals in het volgende voorbeeld wordt getoond:

```yaml
http://{default}/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true

http://{default}/path/:
    type: upstream
    upstream: php:php
    cache:
        enabled: false

http://{default}/path/more/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true
```

In het voorgaande voorbeeld worden de volgende routes in cache opgeslagen:

- `http://{default}/`
- `http://{default}/path/more/`
- `http://{default}/path/more/etc/`

De volgende routes zijn **niet** in cache geplaatst:

- `http://{default}/path/`
- `http://{default}/path/etc/`

>[!NOTE]
>
>Regelmatige expressies in routes zijn **niet** ondersteund.

## Cacheduur

De cacheduur wordt bepaald door de `Cache-Control` responsheader-waarde. Indien niet `Cache-Control` header staat in de reactie, de `default_ttl` key wordt gebruikt.

## Cachesleutel

Om te beslissen hoe u een reactie in de cache plaatst, bouwt Adobe Commerce een cachemoets die afhankelijk is van verschillende factoren en slaat het de reactie op die aan deze toets is gekoppeld. Wanneer een verzoek met de zelfde geheim voorgeheugensleutel komt, wordt de reactie opnieuw gebruikt. Het doel is vergelijkbaar met dat van HTTP [`Vary` header](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.44).

De parameters `headers` en `cookies` kunt u deze cachemoets wijzigen.

De standaardwaarde voor deze toetsen is als volgt:

```yaml
cache:
    enabled: true
    headers: ["Accept-Language", "Accept"]
    cookies: ["*"]
```

## Cachekenmerken

### `enabled`

Wanneer ingesteld op `true`, laat het geheime voorgeheugen voor deze route toe. Wanneer ingesteld op `false`, maak het geheime voorgeheugen voor deze route onbruikbaar.

### `headers`

Definieert op welke waarden de cachetoets moet afhangen.

Als de `headers` key is the following:

```yaml
cache:
    enabled: true
    headers: ["Accept"]
```

Vervolgens plaatst Adobe Commerce een andere reactie in cache voor elke waarde van de `Accept` HTTP-header.

### `cookies`

De `cookies` key bepaalt op welke waarden de geheim voorgeheugensleutel moet afhangen.

Bijvoorbeeld:

```yaml
cache:
    enabled: true
    cookies: ["value"]
```

De cachetoets is afhankelijk van de waarde van de `value` cookie in de aanvraag.

Er bestaat een bijzonder geval als de `cookies` de sleutel heeft de `["*"]` waarde. Deze waarde betekent dat een aanvraag met een cookie de cache overslaat. Dit is de standaardwaarde.

>[!NOTE]
>
>U kunt geen jokertekens gebruiken in de naam van het cookie. Gebruik een exacte naam van een cookie of gebruik een sterretje (`*`). Bijvoorbeeld: `SESS*` of `~SESS` zijn momenteel **niet** geldige waarden.

Cookies hebben de volgende beperkingen:

- U kunt het maximum instellen van **50 cookies** in het systeem. Anders genereert de toepassing een `Unable to send the cookie. Maximum number of cookies would be exceeded` uitzondering.
- Een maximale cookiegrootte is **4096 bytes**. Anders genereert de toepassing een `Unable to send the cookie. Size of '%name' is %size bytes` uitzondering.

### `default_ttl`

Als de reactie geen `Cache-Control` header, de `default_ttl` -toets wordt gebruikt om de duur van de cache in seconden te definiëren. De standaardwaarde is `0`, wat betekent dat er niets in de cache wordt opgeslagen.
