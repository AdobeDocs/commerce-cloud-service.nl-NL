---
title: Meerdere websites of winkels instellen
description: Leer hoe u meerdere websites of winkels voor Adobe Commerce configureert op cloudinfrastructuur.
feature: Cloud, Configuration, Routes, Site Navigation
exl-id: 16e932ef-f083-44d7-977f-0c78899e151a
source-git-commit: 85aa54af10e7ea44adde5403b69ff03d4a0c622f
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 0%

---

# Meerdere websites of winkels instellen

U kunt Adobe Commerce zo configureren dat er meerdere websites of winkels zijn, zoals een Engelse winkel, een Franse winkel en een Duitse winkel. Zie [Werken met websites, winkels en winkelweergaven](best-practices.md#store-views).

>[!WARNING]
>
>De gegevens van de catalogus worden uitgebreid aangezien u het aantal websites en opslag verhoogt. Afhankelijk van uw projectarchitectuur, kunnen de extra opslag tot een langer indexerend proces en langzamere reactietijden voor niet caching cataloguspagina&#39;s leiden. Adobe raadt u aan de prestaties van de site nauwlettend te volgen.

Het proces voor het instellen van meerdere winkels hangt af van het feit of u ervoor kiest unieke of gedeelde domeinen te gebruiken.

Meerdere opslagruimten met unieke domeinen:

```terminal
https://first.store.com/
https://second.store.com/
```

Meerdere opslagruimten met hetzelfde domein:

```terminal
https://store.com/first/
https://store.com/second/
```

>[!TIP]
>
>Als u een opslagweergave wilt toevoegen aan de basis-URL van de site, hoeft u geen meerdere mappen te maken. Zie [De code van de winkel toevoegen aan de basis-URL](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-admin.html) in de _Configuratiegids_.

## Domeinen toevoegen

Aangepaste domeinen kunnen worden toegevoegd aan Pro Staging en elke productieomgeving. Ze kunnen niet worden toegevoegd aan integratieomgevingen.

Het proces om een domein toe te voegen hangt af van het type Cloud-account:

- Voor Pro Staging en Productie

  Het nieuwe domein snel toevoegen, zie [Domeinen beheren](../cdn/fastly-custom-cache-configuration.md#manage-domains)of een ondersteuningsticket openen om hulp aan te vragen. Bovendien moet u [Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om nieuwe domeinen aan te vragen om aan een cluster worden toegevoegd.

- Alleen voor startproductie

  Het nieuwe domein snel toevoegen, zie [Domeinen beheren](../cdn/fastly-custom-cache-configuration.md#manage-domains), of [Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om bijstand te verzoeken. Daarnaast moet u het nieuwe domein toevoegen aan de **Domeinen** in de [!DNL Cloud Console]: `https://<zone>.magento.cloud/projects/<project-ID>/edit`

## Lokale installatie configureren

Om uw lokale installatie te vormen om veelvoudige opslag te gebruiken, zie [Meerdere websites of winkels][config-multiweb] in de _Configuratiegids_.

Nadat u de lokale installatie hebt gemaakt en getest om meerdere winkels te kunnen gebruiken, moet u de integratieomgeving voorbereiden:

1. **Vorm routes of plaatsen**—specificeer hoe de inkomende URLs door Adobe Commerce wordt behandeld

   - [Routes voor afzonderlijke domeinen](#configure-routes-for-separate-domains)
   - [Locaties voor gedeelde domeinen](#configure-locations-for-shared-domains)

1. **Websites, winkels en winkels instellen**—configureren met de gebruikersinterface van Adobe Commerce Admin
1. **Variabelen wijzigen**—specificeer de waarden van `MAGE_RUN_TYPE` en `MAGE_RUN_CODE` variabelen in de `magento-vars.php` file
1. **Implementeer- en testomgevingen**—implementeren en testen `integration` vertakking

>[!TIP]
>
>U kunt een lokale omgeving gebruiken om meerdere websites of winkels in te stellen. Zie de instructies van Cloud Docker voor [Meerdere websites of winkels instellen](https://developer.adobe.com/commerce/cloud-tools/docker/configure/multiple-sites/).

### Configuratie-updates voor Pro-omgevingen

{{pro-self-service-warning}}

### Vorm routes voor afzonderlijke domeinen

Routes bepalen hoe binnenkomende URLs wordt verwerkt. Voor meerdere opslagruimten met unieke domeinen moet u elk domein in het dialoogvenster `routes.yaml` bestand. De manier u routes vormt hangt van af hoe u uw plaats wilt werken.

**Om routes in een integratiemilieu te vormen**:

1. Open op uw lokale werkstation de `.magento/routes.yaml` in een teksteditor.

1. Definieer het domein en de subdomeinen. De `mymagento` De upstream-waarde is dezelfde waarde als de name-eigenschap in de `.magento.app.yaml` bestand.

   ```yaml
   "http://{default}/":
       type: upstream
       upstream: "mymagento:http"
   
   "http://<second-site>.{default}/":
       type: upstream
       upstream: "mymagento:http"
   ```

1. Sla uw wijzigingen op in het dialoogvenster `routes.yaml` bestand.

1. Doorgaan naar [Websites, winkels en winkels instellen](#set-up-websites-stores-and-store-views).

### Locaties voor gedeelde domeinen configureren

Waar de routeneconfiguratie bepaalt hoe URLs wordt verwerkt, `web` eigenschap in de `.magento.app.yaml` bepaalt hoe uw toepassing aan het Web wordt blootgesteld. Web _locaties_ meer granulariteit toestaan voor inkomende verzoeken. Als uw domein bijvoorbeeld `store.com`kunt u `/first` (standaardsite) en `/second` voor aanvragen naar twee verschillende winkels die een domein delen.

**Een nieuwe weblocatie configureren**:

1. Een alias voor het hoofdknooppunt maken (`/`). In dit voorbeeld is de alias `&app` op regel 3.

   ```yaml
   web:
       locations:
           "/": &app
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
   ```

1. Een pass-through voor de website maken (`/website`) en verwijst u naar de hoofdmap met de alias van de vorige stap.

   De alias staat toe `website` om toegang te krijgen tot waarden van de hoofdlocatie. In dit voorbeeld wordt de website `passthru` staat op regel 21.

   ```yaml
   web:
       locations:
           "/": &app
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/media":
               root: "pub/media"
               ...
           "/static":
               root: "pub/static"
               allow: true
               scripts: false
               passthru: "/front-static.php"
               rules:
                   ^/static/version\d+/(?<resource>.*)$:
                       passthru: "/static/$resource"
           "/<website>": *app
             ...
   ```

**Een locatie configureren met een andere map**:

1. Een alias voor het hoofdknooppunt maken (`/`) en voor de statische (`/static`) locaties.

   ```yaml
   web:
       locations:
           "/": &root
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/static": &static
               root: "pub/static"
   ```

1. Een submap maken voor de website onder het dialoogvenster `pub` map: `pub/<website>`

1. De `pub/index.php` in het bestand `pub/<website>` en werk de map bij `bootstrap` pad (`/../../app/bootstrap.php`).

   ```
   try {
       require __DIR__ . '/../../app/bootstrap.php';
   } catch (\Exception $e) { 
   ```

1. Een pass-through-bewerking maken voor de `index.php` bestand.

   ```yaml
   web:
       locations:
           "/": &root
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/media":
               root: "pub/media"
               ...
           "/static": &static
               root: "pub/static"
               allow: true
               scripts: false
               passthru: "/front-static.php"
               rules:
                   ^/static/version\d+/(?<resource>.*)$:
                       passthru: "/static/$resource"
           "/<website>":
               <<: *root
               passthru: "<website>/index.php"
           "/<website>/static": *static
             ...
   ```

1. Leg de gewijzigde bestanden vast en duw erop.

   - `pub/<website>/index.php` (Als dit bestand zich in `.gitignore`de drukknop de krachtoptie nodig heeft.)
   - `.magento.app.yaml`

### Websites, winkels en winkels instellen

In de _Gebruikersinterface van beheerder_, Adobe Commerce instellen **Websites**, **Winkels**, en **Winkelweergaven**. Zie [Meerdere websites instellen, weergaven opslaan en opslaan in de beheerfunctie](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-admin.html) in de _Configuratiegids_.

Het is belangrijk om dezelfde naam en code van uw websites te gebruiken, en meningen van uw Admin op te slaan wanneer u opstelling uw lokale installatie. U hebt deze waarden nodig wanneer u de `magento-vars.php` bestand.

### Variabelen wijzigen

In plaats van een virtuele NGINX-host te configureren, geeft u de `MAGE_RUN_CODE` en `MAGE_RUN_TYPE` variabelen die de `magento-vars.php` in uw hoofdmap van het project.

**Variabelen doorgeven met de opdracht `magento-vars.php` file**:

1. Open de `magento-vars.php` in een teksteditor.

   De [default `magento-vars.php` file](https://github.com/magento/magento-cloud/blob/master/magento-vars.php) zou als het volgende moeten kijken:

   ```php
   <?php
   // enable, adjust and copy this code for each store you run
   // Store #0, default one
   //if (isHttpHost("example.com")) {
   //    $_SERVER["MAGE_RUN_CODE"] = "default";
   //    $_SERVER["MAGE_RUN_TYPE"] = "store";
   //}
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
           return false;
       }
       return $_SERVER['HTTP_HOST'] === $host;
   }
   ```

1. De opmerkingen verplaatsen `if` blokkeren zodat het _na_ de `function` en heeft geen commentaar meer.

   ```php
   <?php
   // enable, adjust and copy this code for each store you run
   // Store #0, default one
   
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
           return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("example.com")) {
       $_SERVER["MAGE_RUN_CODE"] = "default";
       $_SERVER["MAGE_RUN_TYPE"] = "store";
   }
   ```

1. Vervang de volgende waarden in het dialoogvenster `if (isHttpHost("example.com"))` blok:
   - `example.com`—met de basis-URL van uw _website_
   - `default`—met de unieke CODE voor uw _website_ of _winkelweergave_
   - `store`—met een van de volgende waarden:
      - `website`—laad de _website_ in de winkel
      - `store`—load a _winkelweergave_ in de winkel

   Voor meerdere sites die unieke domeinen gebruiken:

   ```php
   <?php
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
       return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("second.store.com")) {
       $_SERVER["MAGE_RUN_CODE"] = "<second-site>";
       $_SERVER["MAGE_RUN_TYPE"] = "website";
   }elseif (isHttpHost("store.com")){
       $_SERVER["MAGE_RUN_CODE"] = "base";
       $_SERVER["MAGE_RUN_TYPE"] = "website";
   }
   ```

   Voor meerdere sites met hetzelfde domein moet u de opdracht _host_ en de _URI_:

   ```php
   <?php
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
       return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("store.com")) {
      $code = "base";
      $type = "website";
   
      $uri = explode('/', $_SERVER['REQUEST_URI']);
      if (isset($uri[1]) && $uri[1] == 'second') {
        $code = '<second-site>';
        $type = 'website';
      }
      $_SERVER["MAGE_RUN_CODE"] = $code;
      $_SERVER["MAGE_RUN_TYPE"] = $type;
   }
   ```

1. Sla uw wijzigingen op in het dialoogvenster `magento-vars.php` bestand.

### Implementeren en testen op de integratieserver

Breng uw wijzigingen aan in uw Adobe Commerce op de integratieomgeving van de cloudinfrastructuur en test uw site.

1. Wijzigingen in de externe vertakking toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add -A && git commit -m "Implement multiple sites" && git push origin <branch-name>
   ```

1. Wacht tot de implementatie is voltooid.

1. Na de implementatie opent u de URL van je winkel in een webbrowser.

   Met een uniek domein, gebruik het formaat: `http://<magento-run-code>.<site-URL>`

   Bijvoorbeeld: `http://french.master-name-projectID.us.magentosite.cloud/`

   Gebruik de indeling bij een gedeeld domein: `http://<site-URL>/<magento-run-code>`

   Bijvoorbeeld: `http://master-name-projectID.us.magentosite.cloud/french/`

1. Test uw site grondig en voeg de code samen met de `integration` vertakking voor verdere implementatie.

## Distribueren naar Staging en Productie

Volg het implementatieproces voor [implementatie naar Staging en Productie](../deploy/staging-production.md). Voor Starter- en Pro-omgevingen gebruikt u de [!DNL Cloud Console] om code door milieu&#39;s te duwen.

Adobe beveelt aan om volledig te testen in de testomgeving voordat naar de productieomgeving wordt geduwd. Breng codeveranderingen in het integratiemilieu aan en begin het proces om over milieu&#39;s opnieuw op te stellen.

<!-- link definitions -->

[config-multiweb]: https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-overview.html
