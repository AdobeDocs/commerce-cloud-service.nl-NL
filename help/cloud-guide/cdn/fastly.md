---
title: Overzicht van snelle services
description: Leer hoe u met de snelste services die bij Adobe Commerce worden geleverd via de cloudinfrastructuur de levering van inhoud voor uw Adobe Commerce-sites kunt optimaliseren en beveiligen.
feature: Cloud, Configuration, Iaas, Paas, Cache, Security, Services
exl-id: dc4500bf-f037-47f0-b7ec-5cd1291f73a1
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1392'
ht-degree: 0%

---

# Overzicht van snelle services

>[!WARNING]
>
>Als u de PCI-compatibiliteit wilt behouden voor Adobe Commerce-sites die op het Cloud-platform worden geïmplementeerd, stelt u snel in op uw Starter-hoofdvertakking, Pro Production en Pro Staging-omgevingen. Als u Adobe Commerce in een headless plaatsing gebruikt, adviseren wij hoogst dat u snel gebruikt om de reacties van GraphQL in het voorgeheugen onder te brengen. Zie [In cache plaatsen met snel](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/#caching-with-fastly) in de *GraphQL Developer Guide*.

In Fastly worden de volgende services geleverd voor het optimaliseren en beveiligen van de levering van inhoud voor Adobe Commerce voor infrastructuurprojecten in de cloud. Deze services worden zonder extra kosten meegeleverd bij Adobe Commerce op cloudinfrastructuur.

- **Content Delivery Network (CDN)**—Verscheidene service waarmee uw sitepagina&#39;s, elementen, CSS en meer in door u ingestelde back-enddatacenters in het cachegeheugen worden opgeslagen. Wanneer klanten toegang krijgen tot uw site en winkels, kunnen ze sneller in cache geplaatste pagina&#39;s laden. De CDN-service biedt de volgende functies:

- **Cachebeheer**—Plaats uw sitepagina&#39;s, elementen, CSS en meer in back-end datacenters die u instelt om de bandbreedtebelasting en -kosten te verminderen

   - Gebruiken [Snelle aangepaste VCL-fragmenten](fastly-vcl-custom-snippets.md) (Volgzaam Varnish 2.1) om te wijzigen hoe het in cache plaatsen aan verzoeken beantwoordt

   - Instellen [Ondersteuning voor GeoIP-services](fastly-custom-cache-configuration.md#configure-geoip-handling)

   - [Niet-gecodeerde aanvragen forceren naar TLS](fastly-custom-cache-configuration.md#force-tls)

   - [Snelle time-out aanpassen](fastly-custom-cache-configuration.md#extend-fastly-timeout) instellingen om 503 reacties op verzoeken om bulkbewerkingen te voorkomen

   - Maken [aangepaste antwoordpagina&#39;s voor fouten](fastly-custom-response.md)

- **Beveiliging**—Nadat u de Snelle diensten voor de plaatsen van Adobe Commerce toelaat, zijn de extra veiligheidseigenschappen beschikbaar om uw plaatsen en netwerk te beschermen:

   - [Web Application Firewall](fastly-waf-service.md) (WAF) - De beheerde dienst van de de firewalldienst van de Webtoepassing die PCI-Volgzame bescherming biedt om kwaadwillig verkeer te blokkeren alvorens het uw productie Adobe Commerce op de plaatsen en het netwerk van de wolkeninfrastructuur kan beschadigen. De WAF-service is alleen beschikbaar in Pro- en Starter Production-omgevingen.

   - [Distributed Denial of Service (DDoS)-bescherming](#ddos-protection)—Ingebouwde DDoS bescherming tegen gemeenschappelijke aanvallen zoals Ping van Dood, Smurf aanvallen, en andere op ICMP-Gebaseerde overstromingsaanvallen.

   - [SSL/TLS-certificaten](fastly-configuration.md#provision-ssltls-certificates)—De sneldienst vereist een SSL/TLS-certificaat om veilig verkeer via HTTPS te kunnen uitvoeren.

     Adobe Commerce biedt een door een domein gevalideerd SSL/TLS-certificaat voor elke staging- en productieomgeving. Adobe Commerce voltooit domeinvalidatie en certificaatprovisioning tijdens het installatieproces van Snel.

- **Oorspronkelijke opmaak**—Verhindert verkeer om Fastly WAF te mijden en de IP adressen van uw oorsprongservers te verbergen om hen tegen directe toegang en aanvallen te beschermen DDoS.

  Oorspronkelijke camouflage is standaard ingeschakeld in Adobe Commerce op cloudinfrastructuur Pro Production-projecten. Om de oorsprongsbescherming in Adobe Commerce mogelijk te maken voor Starter Productieprojecten in de cloud-infrastructuur, dient u een [Adobe Commerce-ondersteuningsticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). Als u verkeer hebt dat geen caching vereist, kunt u de Fastly de dienstconfiguratie aanpassen om verzoeken toe te staan om [de snelcache omzeilen](fastly-vcl-bypass-to-origin.md).

- **[Optimalisatie van afbeeldingen](fastly-image-optimization.md)**—Verschuift de beeldverwerking en het resizing lading aan de Snelle dienst zodat de servers bestellingen en omzettingen efficiënter kunnen verwerken.

- **[Fastly CDN and WAF logs](../monitor/new-relic-service.md#new-relic-log-management)**—Voor Adobe Commerce op de Pro-projecten van de cloudinfrastructuur kunt u de New Relic Logs-service gebruiken om snel CDN- en WAF-loggegevens te bekijken en te analyseren.

## Snelle CDN-module voor Magento 2

Snelle services voor Adobe Commerce op cloudinfrastructuur gebruiken de [Snelle CDN-module voor Magento 2] geïnstalleerd in de volgende omgevingen: Pro Staging and Production, Starter Production (`master` vertakking).

Bij eerste levering of upgrade van uw Adobe Commerce-project installeert Adobe de nieuwste versie van de Fastly CDN-module in uw staging- en productieomgeving. Als u de updates van de module Fastly loslaat, ontvangt u meldingen in Admin voor uw omgevingen. Adobe raadt u aan uw omgevingen bij te werken om de nieuwste versie te gebruiken. Zie [Snelle upgrade uitvoeren](fastly-configuration.md#upgrade-the-fastly-module).

## Snelle de dienstrekening en geloofsbrieven

Voor opmerkingen over Adobe van projecten met cloudinfrastructuur is geen speciale Fastly-account of accounteigenaar vereist. In plaats daarvan heeft elke omgeving voor Staging en Productie unieke snelle referenties (API-token en service-id) voor het configureren en beheren van snelle services van de beheerder. U hebt ook de aanmeldingsgegevens nodig om snel API-aanvragen in te dienen.

Tijdens projectlevering, voegt de Adobe uw project aan de Fastly de dienstrekening voor Adobe Commerce op wolkeninfrastructuur toe en voegt de Fastly geloofsbrieven aan de configuratie voor de het Opvoeren en milieu&#39;s van de Productie toe. Zie [Snelle gebruikersgegevens ophalen](fastly-configuration.md#get-fastly-credentials).

### Fastly API-token wijzigen

Verzend een Adobe Commerce Support-ticket om de Fastly API-tokenreferentie te wijzigen. Wanneer u het nieuwe token ontvangt, werkt u de omgeving voor Staging of Productie bij om het nieuwe token te gebruiken.

**De functie voor snelle API-tokenreferentie wijzigen**:

1. [Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) aanvragen van nieuwe Fastly API-referenties.

   Neem uw Adobe Commerce op in de projectid van de cloud-infrastructuur en de omgevingen die een nieuwe referentie vereisen.

1. Nadat u het nieuwe API-token hebt ontvangen, werkt u de waarde van het API-token bij in het dialoogvenster [Configuratie van snelle referenties](fastly-configuration.md#test-the-fastly-credentials) in de Admin of van de [[!DNL Cloud Console] omgevingsvariabelen](../project/overview.md#configure-environment).

1. [De nieuwe referentie testen](fastly-configuration.md#test-the-fastly-credentials).

1. Nadat u de referentie hebt bijgewerkt, verzendt u een Adobe Commerce-ondersteuningsticket om de oude API-token te verwijderen.

### Meerdere snelaccounts en toegewezen domeinen

U kunt snel alleen een apex-domein en de bijbehorende subdomeinen toewijzen aan één Fastly-service en -account. Als u een bestaande snelaccount hebt waarmee dezelfde map en subdomeinen die voor uw Adobe Commerce-site worden gebruikt, worden gekoppeld, hebt u de volgende opties:

- Verwijder de apex- en subdomeinen van het bestaande account voordat u de Fastly-servicegegevens aanvraagt voor uw Adobe Commerce in een cloud-infrastructuurprojectomgeving. Zie [Werken met domeinen] in de Fastly documentatie.

  Gebruik deze optie om het apex-domein en alle subdomeinen te koppelen aan het Fastly-serviceaccount voor Adobe Commerce op cloudinfrastructuur.

- Verzend een Adobe Commerce-ondersteuningsticket om domeindelegatie aan te vragen, zodat apex en subdomeinen aan verschillende accounts kunnen worden gekoppeld.

  Gebruik deze optie als u een ex-domein hebt met meerdere subdomeinen voor Adobe Commerce- en niet-Adobe Commerce-sites en u deze subdomeinen wilt koppelen aan verschillende snelaccounts.

#### Domeindelegatie aanvragen

*Scenario 1*

Het apex-domein (`testweb.com` en `www.testweb.com`) is gekoppeld aan een bestaande snelaccount. U hebt een Adobe Commerce op het project van de wolkeninfrastructuur dat met volgende subdomeinen wordt gevormd: `mcstaging.testweb.com` en `mcprod.testweb.com`. U wilt het apex-domein niet verplaatsen naar het Fastly-serviceaccount voor Adobe Commerce op cloudinfrastructuur.

Een [Kaart voor snelle ondersteuning] verzoeken dat de subdomeinen worden gedelegeerd van de bestaande Fastly-account naar de Fastly-account voor Adobe Commerce op cloud-infrastructuur. Neem uw Adobe Commerce-project-id op in het ticket.

Nadat de delegatie is voltooid, kunnen uw projectsubdomeinen aan de Fastly de dienstrekening voor Adobe Commerce op wolkeninfrastructuur worden toegevoegd. Zie [Snelle gebruikersgegevens ophalen](fastly-configuration.md#get-fastly-credentials).

*Scenario 2*

Het apex-domein (`testweb.com` en `www.testweb.com`) is gekoppeld aan de Adobe Commerce op de Fastly-serviceaccount voor cloudinfrastructuur. U wilt de snelservices beheren voor de `service.testweb.com` en `product-updates.testweb.com` subdomeinen van een andere Fastly-account.

Verzend een Adobe Commerce Support-ticket met het verzoek om de subdomeinen van de Adobe Commerce te delegeren naar de Fastly-account voor cloudinfrastructuur. Neem de service-id voor de snelaccount op in het ticket.

## DoS-beveiliging

DDOS-beveiliging is ingebouwd in de Fastly CDN-service. Zodra u de Snelle diensten voor uw plaatsen van Adobe Commerce hebt toegelaten, filters snel al Web en admin verkeer om potentiële aanvallen te ontdekken en te blokkeren.

- Voor aanvallen gericht op laag 3 of 4, filtert de Snelle dienst uit verkeer dat op haven en protocol wordt gebaseerd, die slechts HTTP of HTTPS verzoeken inspecteren. ICMP, UDP, en andere netwerk-in werking gestelde aanvallen worden gelaten vallen bij onze netwerkrand. Dit omvat bezinning en versterkingsaanvallen, die de diensten UDP zoals SSDP of NTP gebruiken. Door dit niveau van bescherming te bieden, blokkeren we effectief meerdere gemeenschappelijke aanvallen zoals Ping of Death, Smurf-aanvallen en andere op ICMP gebaseerde overstromingen.

  Beheert snel de vlakke aanvallen van TCP bij de geheim voorgeheugenlaag. Deze strategie verstrekt de noodzakelijke schaal en de context per cliënt om een de overstromingsaanval van SYN en zijn vele varianten, met inbegrip van de stapel van TCP, middelaanvallen, en de aanvallen van TLS binnen Fastly systemen te behandelen.

- Verstrekt snel ook bescherming tegen Laag 7 aanvallen. Als er prestatieproblemen optreden in uw winkel en u vermoedt dat er een Layer 7 DDoS-aanval plaatsvindt, stuurt u een Adobe Commerce Support-ticket naar u. De Adobe kan douaneregels tot stand brengen en toepassen op de Snelle dienst om kwaadwillige verzoeken te inspecteren en uit te filtreren die op kopbal, lading, of een combinatie attributen worden gebaseerd die het aanvalsverkeer identificeren. Zie [Controleren op DDoS-aanvallen] en [Hoe te om kwaadwillig verkeer te blokkeren] in de *Adobe Commerce Help Center*.

<!--Link definitions-->

[Caching with Fastly]: https://developer.adobe.com/commerce/webapi/graphql/usage/caching/#caching-with-fastly

[Controleren op DDoS-aanvallen]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/checking-for-ddos-attack-from-cli.html

[Snelle CDN-module voor Magento 2]: https://github.com/fastly/fastly-magento2

[Kaart voor snelle ondersteuning]: https://docs.fastly.com/products/support-description-and-sla#support-requests

[Hoe te om kwaadwillig verkeer te blokkeren]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/block-malicious-traffic-for-magento-commerce-on-fastly-level.html

[Werken met domeinen]: https://docs.fastly.com/en/guides/working-with-domains
