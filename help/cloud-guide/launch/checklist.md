---
title: Checklist starten
description: Controlelijst met items voor het starten van de site weergeven.
exl-id: 4525742e-18c5-40d1-975d-00ba3f3a51a0
source-git-commit: 5b0a691a4355f5eda31d42cd3da9925439dfb510
workflow-type: tm+mt
source-wordcount: '1104'
ht-degree: 0%

---

# Checklist starten

Voordat u de toepassing implementeert in de productieomgeving, downloadt u de [Checklist starten](../../assets/adobe-commerce-cloud-prelaunch-checklist.pdf)en gebruik deze met deze instructies om te bevestigen dat u alle vereiste configuratie en tests hebt uitgevoerd. Bekijk een overzicht van het volledige implementatieproces voor Starter en Pro op [Je winkel implementeren](../deploy/staging-production.md).

## Volledig testen in productie

Zie [Implementatie testen](../test/staging-and-production.md) voor het testen van alle aspecten van uw sites, winkels en omgevingen. Deze tests omvatten het controleren van Fastly, de Tests van de Erkenning van de Gebruiker (UAT), en prestatietests.

## TLS en snel

Adobe biedt een Let&#39;s Encrypt SSL/TLS-certificaat voor elke omgeving. Dit certificaat is vereist om snel veilig verkeer via HTTPS te kunnen uitvoeren.

Om dit certificaat te gebruiken, moet u uw DNS configuratie bijwerken zodat de Adobe domeinbevestiging kan voltooien en het certificaat op uw milieu toepassen. Elke omgeving heeft een uniek certificaat dat de domeinen voor de Adobe Commerce bestrijkt op cloudinframinframites die in die omgeving worden geïmplementeerd. We raden u aan de configuratie-updates tijdens de [Snellere installatie](../cdn/fastly-configuration.md).

## DNS-configuratie bijwerken met productie-instellingen

Wanneer u bereid bent om uw plaats te lanceren, moet u de DNS configuratie bijwerken om verkeer van uw milieu van de Productie door de Snelle dienst te leiden.

**Vereisten:**

- [Stel uw ontwikkelomgeving in en test deze snel](../cdn/fastly-configuration.md#)

- Configuratie van productieomgeving is bijgewerkt met alle vereiste domeinen

  Gewoonlijk werkt u met uw technische adviseur van de Klant om alle domeinen en subdomeinen op hoofdniveau toe te voegen die voor uw opslag worden vereist. Om de domeinen voor uw milieu van de Productie toe te voegen of te veranderen, [Een Adobe Commerce-ondersteuningsticket verzenden](https://support.magento.com/hc/en-us/articles/360019088251). Wacht op bevestiging dat uw projectconfiguratie is bijgewerkt.

  Voor de projecten van de Aanzet, moet u de domeinen aan uw project toevoegen. Zie [Domeinen beheren](../cdn/fastly-custom-cache-configuration.md#manage-domains).

- SSL/TLS-certificaat dat is ingericht voor uw productieomgeving.

  Als u de ACME uitdagingsverslagen voor uw domeinen van de Productie tijdens het Fastly opstellingsproces toevoegde, uploadt de Adobe het SSL/TLS certificaat aan uw milieu van de Productie automatisch wanneer u de DNS configuratie aan routeverkeer aan de Fastly dienst bijwerkt. Als u het certificaat niet vooraf hebt verstrekt, of als u uw domeinen bijwerkte, moet de Adobe domeinbevestiging voltooien en levering het certificaat, dat tot 12 uren kan vergen.

### DNS-configuratie bijwerken voor het starten van de site:

1. Werk de volgende DNS configuratie voor uw plaats van de Productie bij:

   - Alle benodigde omleidingen instellen, vooral als u van een bestaande site migreert

   - Plaats het verslag van het wortelmiddel van de streek om hostname te richten

   - Verlaag de waarde voor Tijd-aan-Levende (TTL) om DNS informatie te verfrissen om klanten aan de correcte opslag van de Productie te richten

     Wij adviseren een beduidend lagere waarde van TTL wanneer het schakelen van het DNS verslag. Deze waarde vertelt DNS hoe lang om het DNS verslag in het voorgeheugen onder te brengen. Wanneer verkort, verfrist het sneller DNS. U kunt bijvoorbeeld de TTL-waarde wijzigen van drie dagen in tien minuten wanneer u uw site bijwerkt. Houd er rekening mee dat het verkorten van de TTL-waarde het laden van de DNS-infrastructuur toevoegt. Herstel de vorige, hogere waarde na de lancering van de plaats.


1. Voeg CNAME verslagen toe om subdomeinen voor uw milieu van de Productie aan de Snelle dienst te richten `prod.magentocloud.map.fastly.net`, bijvoorbeeld:

   | Domein of Subdomein | CNAME |
   | ----------------------- | -------------------------------- |
   | `www.<domain-name>.com` | prod.magentocloud.map.fastly.net |
   | `mystore.<domain-name>.com` | prod.magentocloud.map.fastly.net |

1. Voeg zo nodig A-records toe om het apex-domein toe te wijzen (`<domain-name>.com`) aan de volgende Snelle IP adressen:

   | Apex-domein | ANAME |
   | --------------- | ----------------- |
   | `<domain-name>.com` | `151.101.1.124` |
   | `<domain-name>.com` | `151.101.65.124` |
   | `<domain-name>.com` | `151.101.129.124` |
   | `<domain-name>.com` | `151.101.193.124` |

>[!IMPORTANT]
>
>De DNS-instructies in [RFC1034](https://www.rfc-editor.org/rfc/rfc1912) (**punt 2.4**) vermelden dat:
>_Een CNAME-record mag niet naast andere gegevens bestaan. Met andere woorden, als suzy.podunk.xx een alias voor use.podunk.xx is, kunt u niet ook een MX- verslag voor suzy.podunk.edu, of een verslag van A, of zelfs een verslag van TXT hebben._
>
>Daarom moeten DNS-records van het type zijn `CNAME` voor subdomeinen en type `A` voor apex-domeinen (hoofddomeinen). Het verwerpen van deze regel kan in verstoringen aan uw postdienst of DNS propagatie resulteren omdat u de capaciteit verliest om andere verslagen, zoals MX of NS toe te voegen. Sommige DNS leveranciers kunnen dit door interne aanpassingen te gebruiken omzeilen, maar het volgen van de norm verzekert stabiliteit en flexibiliteit (zoals verandering van de DNS leverancier).

1. Werk de basis-URL bij.

   - Gebruik SSH om u aan te melden bij de productieomgeving.

     ```bash
     magento-cloud ssh -e production
     ```

   - Gebruik CLI om de basis URL voor uw opslag te veranderen.

     ```bash
     php bin/magento setup:store-config:set --base-url="https://www.<domain-name>.com/"
     ```

   **OPMERKING**: U kunt de basis-URL ook bijwerken via Beheer. Zie [URL&#39;s opslaan](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-urls.html) in de _Handleiding voor Adobe Commerce-winkels en -aankopen_.

1. Wacht een paar minuten totdat de site is bijgewerkt.

1. Test uw site.

## Productieconfiguratie verifiëren

Maak een definitieve pas om de configuratie van de Productie voor één of meerdere opslag te bevestigen. U kunt de configuratie bijwerken in de productieomgeving. Als de montages read-only zijn, kunt u een verbinding van SSH moeten openen en CLI bevelen gebruiken om de configuratie te veranderen, of configuratieveranderingen in uw lokale milieu aan te brengen. Nadat u de updates hebt voltooid, kunt u de wijzigingen implementeren in de omgeving van Staging en Productie.

Hieronder vindt u aanbevolen wijzigingen en controles:

- [Uitgaande e-mailtests voltooid](../project/outgoing-emails.md)

- [Beveiligde configuratie voor beheerdersreferenties en Basis Admin URL](https://docs.magento.com/user-guide/stores/security-admin.html)

- [Alle afbeeldingen voor het web optimaliseren](../cdn/fastly-image-optimization.md)

- [Minimalisatie-instellingen controleren voor HTML, JavaScript en CSS](../deploy/static-content.md)

## Snelle caching controleren

- Test en verifieer dat het snel in cache plaatsen correct op de plaats van de Productie werkt. Voor gedetailleerde tests en controles, zie [Snelle tests](../test/staging-and-production.md#check-fastly-caching).

- [Zorg ervoor dat de recentste versie van de FastlyCDN Module voor Handel in uw milieu van de Productie wordt geïnstalleerd](../cdn/fastly-configuration.md#upgrade-the-fastly-module)

- [Controleer of de meest actuele versie van de VCL-code snel is geüpload](../cdn/fastly-configuration.md#upload-vcl-to-fastly)

## Prestatietests

We raden u aan de [Prestatiewerkset](https://github.com/magento/magento2/tree/2.4/setup/performance-toolkit) -opties als onderdeel van het gereedheidsproces voorafgaand aan de start.

U kunt ook testen met de volgende opties van derden:

- [Siege](https://www.joedog.org/siege-home/): Verkeersvormings- en testsoftware om uw winkel tot het maximale uit te breiden. Plaats uw site met een configureerbaar aantal gesimuleerde clients. Siege ondersteunt basisverificatie, cookies, HTTP-, HTTPS- en FTP-protocollen.

- [Jmeter](https://jmeter.apache.org/): Uitstekende ladingstest om prestaties voor verrijkt verkeer, zoals voor flitsverkoop te meten. Aangepaste tests maken die op uw site worden uitgevoerd.

- [New Relic](https://support.newrelic.com/s/) (Opgegeven): Helpt processen en gebieden van de plaats te bepalen die langzame prestaties met bijgehouden tijd veroorzaken doorbracht per actie zoals het overbrengen van gegevens, vragen, Redis, en meer.

- [WebPageTest](https://www.webpagetest.org/) en [VK](https://www.pingdom.com/): Real-time analyse van uw sitepagina&#39;s laadt tijd met verschillende oorspronkelijke locaties. Het koninkrijk kan een vergoeding kosten. WebPageTest is een gratis hulpmiddel.

## Beveiligingsconfiguratie

- [Beveiligingsscan instellen](overview.md#set-up-the-security-scan-tool)

- [Beveiligde configuratie voor Admin-gebruiker](https://docs.magento.com/user-guide/stores/security-admin.html)

- [Beveiligde configuratie voor URL van beheerder](https://docs.magento.com/user-guide/stores/store-urls-custom-admin.html)

- [Gebruikers die zich niet meer op de Adobe Commerce bevinden, verwijderen uit het infrastructuurproject voor de cloud](../project/user-access.md)

- [2-factor verificatie configureren](https://devdocs.magento.com/guides/v2.4/security/two-factor-authentication.html)

## Prestatiebewaking

U kunt New Relic-services gebruiken voor prestatiebewaking in Pro- en Starter-omgevingen. Op Pro-planaccounts bieden we de Beheerde waarschuwingen voor het Adobe Commerce-waarschuwingsbeleid om de prestaties van toepassingen en infrastructuren te controleren met behulp van New Relic APM en Infrastructure-agents. Zie voor meer informatie over het gebruik van deze services [Prestaties bewaken met beheerde waarschuwingen](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts).

### Volgende stap

[Stappen starten](steps.md)
