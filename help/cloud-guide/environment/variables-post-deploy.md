---
title: Variabelen na implementatie
description: Zie de lijst met omgevingsvariabelen die de acties in de Adobe Commerce na de implementatiefase van de cloudinfrastructuur besturen.
feature: Cloud, Configuration, Cache
recommendations: noDisplay, catalog
role: Developer
exl-id: e460335f-cd2b-4c98-b1ff-32504599b33d
source-git-commit: 8b02757591c4e8f607e936de4eda74d76953d9b7
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# Variabelen na implementatie

Het volgende _na implementatie_ variabelen besturen acties in de post-implementatiefase en kunnen waarden overnemen en overschrijven van de [Algemene variabelen](variables-global.md). Deze variabelen invoegen in het dialoogvenster `post-deploy` stadium van de `.magento.env.yaml` bestand:

```yaml
stage:
  post-deploy:
    POST-DEPLOY_VARIABLE_NAME: value
```

Voor meer informatie over het aanpassen van het bouwstijl en opstellen proces:

- [Implementatieconfiguratie](configure-env-yaml.md)
- [Implementatieproces](../deploy/process.md)

## `TTFB_TESTED_PAGES`

- **Standaard**— `[]` (een lege array)
- **Versie**—Adobe Commerce 2.1.4 en hoger

Configureren _Tijd naar eerste byte_ (TTFB) testen op opgegeven pagina&#39;s om de prestaties van uw site te testen. Geef een absolute padverwijzing op, of een URL met protocol en host, voor elke pagina waarvoor de test nodig is.

```yaml
stage:
  post-deploy:
    TTFB_TESTED_PAGES:
       - "index.php"
       - "index.php/customer/account/create"
       - "https://example.com/catalog/some-category"
```

Nadat u de pagina&#39;s hebt opgegeven die u wilt testen en doorvoeren, _Tijd naar eerste byte_ de test wordt uitgevoerd tijdens de fase na de implementatie en de resultaten worden voor elk pad naar het cloudlog gepubliceerd:

```terminal
[2019-06-20 20:42:22] INFO: TTFB test result: 0.313s {"url":"https://staging-tkyicst-xkmwgjkwmwfuk.us-4.magentosite.cloud/customer/account/create","status":200}
[2019-06-20 20:42:22] INFO: TTFB test result: 0.408s {"url":"https://staging-tkyicst-xkmwgjkwmwfuk.us-4.magentosite.cloud/checkout/cart","status":200}
```

Voor omgeleide wegen, meldt het logboek de weg van het omleidingsdoel in plaats van die in de omgevingsvariabele wordt gevormd. Als u een ongeldig pad opgeeft, wordt in het logbestand een waarschuwingsbericht weergegeven.

## `WARM_UP_CONCURRENCY`

- **Standaard**—_Niet ingesteld_
- **Versie**—Adobe Commerce 2.1.4 en hoger

Geef de limiet op voor gelijktijdige verzoeken om tijdens opwarmbewerkingen in het cachegeheugen te verzenden om de serverlading te verminderen. Deze waarde beperkt het aantal parallelle verbindingen en is nuttig voor omgevingsconfiguraties waarbij de `WARM_UP_PAGES` post-implementatievariabele specificeert verscheidene pagina&#39;s voor geheim voorladen geheim voorgeheugen.

```yaml
stage:
  post-deploy:
    WARM_UP_CONCURRENCY: 4
```

## `WARM_UP_PAGES`

- **Standaard**— `index.php`
- **Versie**—Adobe Commerce 2.1.4 en hoger

De lijst met pagina&#39;s aanpassen die worden gebruikt om de cache vooraf te laden in het dialoogvenster `post_deploy` in het werkgebied. U moet de post-opstellen haak vormen. Zie de [sectie haken](../application/hooks-property.md) van de `.magento.app.yaml` bestand.

- **enkele pagina&#39;s**—Geef één pagina op die u aan de cache wilt toevoegen. U hoeft de standaard basis-URL niet aan te geven. In het volgende voorbeeld wordt het `BASE_URL/index.php` pagina:

  ```yaml
  stage:
    post-deploy:
      WARM_UP_PAGES:
        - "index.php"
  ```

- **meerdere domeinen**—Meerdere URL&#39;s weergeven. In het volgende voorbeeld worden pagina&#39;s van twee domeinen in cache opgeslagen:

  ```yaml
  stage:
    post-deploy:
      WARM_UP_PAGES:
        - 'http://example1.com/test'
        - 'http://example2.com/test'
  ```

- **meerdere pagina&#39;s**—Gebruik de volgende indeling om meerdere pagina&#39;s in cache te plaatsen volgens een specifiek regulier expressiepatroon:

  ```terminal
  <entity_type>:<pattern|url|product_sku>:<store_id|store_code>
  ```

   - `entity_type`: Mogelijke varianten `category`, `cms-page`, `product`, `store-page`
   - `pattern|url|product_sku`: Een `regexp` patroon of exacte overeenkomst `url` om de URL&#39;s te filteren of een sterretje (\*) te gebruiken voor alle pagina&#39;s. ProductSKU gebruiken voor de `product` entiteitstype
   - `store_id|store_code`: Gebruik de id of de code van de winkel of een sterretje (\*) voor alle winkels. U kunt meerdere winkel-id&#39;s of codes doorgeven die zijn gescheiden met `|`

  In het volgende voorbeeld wordt in cache geplaatst voor `category` en `cms-page` op deze criteria gebaseerde typen entiteiten:
   - alle rubriekpagina&#39;s voor opslag met ID `1`
   - alle categoriepagina&#39;s voor winkels met code `store1` en `store2`
   - rubriekspagina `cars` voor opslag met code `store_en`
   - cms-pagina `contact` voor alle winkels
   - cms-pagina `contact` voor winkels met id `1` en `2`
   - een categoriepagina die `car_` en eindigt met `html` voor opslag met ID 2
   - een categoriepagina die `tires_` voor opslag met code `store_gb`

     ```yaml
     stage:
       post-deploy:
         WARM_UP_PAGES:
           - "category:*:1"
           - "category:*:store1|store2"
           - "category:cars:store_en"
           - "cms-page:contact:*"
           - "cms-page:contact:1|2"
           - "category:|car_.*?\\.html$|:2"
           - "category:|tires_.*|:store_gb"
     ```

  In het volgende voorbeeld wordt de cache voor de `product` op basis van deze criteria:
   - alle producten voor alle opslag (programmatically beperkt tot 100 per opslag om prestatieskwesties te vermijden)
   - alle producten in de opslagplaats `store1`
   - producten met `sku1` voor alle winkels
   - producten met `sku1` voor winkels met code `store1` en `store2`
   - producten met `sku1`, `sku2` en `sku3` voor winkels met code `store1` en `store2`

     ```yaml
     stage:
       post-deploy:
         WARM_UP_PAGES:
           - "product:*:*"
           - "product:*:store1"
           - "product:sku1:*"
           - "product:sku1:store1|store2"
           - "product:sku1|sku2|sku3:store1|store2"
     ```

  In het volgende voorbeeld wordt de cache voor de `store-page` op basis van deze criteria:
   - page `/contact-us` voor alle winkels
   - page `/contact-us` voor opslag met id `1`
   - page `/contact-us` voor winkels met code `code1` en `code2`

  ```yaml
        stage:
          post-deploy:
            WARM_UP_PAGES:
              - "store-page:/contact-us:*"
              - "store-page:/contact-us:1"
              - "store-page:/contact-us:code1|code2"
  ```
