---
title: Testen van het strooisel en de productie
description: Leer hoe u kunt testen in testomgevingen voor Staging en Productie.
exl-id: 5b762d59-04c5-4e89-a637-719141759158
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 0%

---

# Testen van het strooisel en de productie

Nadat de migratie van uw code, bestanden en gegevens naar Staging of Production is voltooid, gebruikt u de omgeving-URL&#39;s om uw sites en winkels te testen. Hieronder vindt u informatie over het controleren van logbestanden, het testen van snelconfiguraties, het testen van gebruikersacceptatie (UAT) en meer.

## Logbestanden

Controleer de logbestanden als er tijdens het testen fouten optreden bij de implementatie of andere problemen. Logbestanden bevinden zich onder de `var/log` directory.

Het plaatsingslogboek is binnen `/var/log/platform/<prodject-ID>/deploy.log`. De waarde van `<project-ID>` is afhankelijk van de project-id en of de omgeving is Staging of Production. Met bijvoorbeeld een project-id van `yw1unoukjcawe`, de gebruiker Staging is `yw1unoukjcawe_stg` en de productiegebruiker `yw1unoukjcawe`.

Wanneer het toegang tot logboeken in de milieu&#39;s van de Productie of van het Staging, gebruik SSH aan login aan elk van de drie knopen om van de logboeken de plaats te bepalen. U kunt ook [New Relic-logbeheer](../monitor/log-management.md) om samengevoegde logboekgegevens van alle knopen te bekijken en te vragen. Zie [Logboeken weergeven](log-locations.md#application-logs).

## De basis van de code controleren

Controleer of de basis van uw code correct is geïmplementeerd in een testomgeving en een productieomgeving. De milieu&#39;s zouden identieke codebasis moeten hebben.

## Configuratieinstellingen controleren

Controleer de configuratie-instellingen via het deelvenster Beheer, waaronder de URL voor basis-beheer, URL voor basisbeheer, instellingen voor meerdere sites en meer. Als u aanvullende wijzigingen moet aanbrengen, voert u alle bewerkingen uit in de lokale Git-vertakking en drukt u op de knop `master` tak in Integratie, het Staging, en Productie.

## Snelle caching controleren

[Snel configureren](../cdn/fastly-configuration.md) vereist zorgvuldige aandacht aan detail: het gebruiken van correcte Snelle identiteitskaart van de Dienst en Fastly API symbolengeloofsbrieven, het uploaden van de Fastly code VCL, het bijwerken van de DNS configuratie, en het toepassen van SSL/TLS certificaten op uw milieu&#39;s. Nadat u deze instellingstaken hebt uitgevoerd, kunt u controleren of het in cache opslaan en maken van bestanden snel is gelukt.

**Om de Fastly de dienstconfiguratie te verifiëren**:

1. Meld u met de URL met `/admin`of de [bijgewerkte Admin-URL](../environment/variables-admin.md#admin-url).

1. Navigeren naar **Winkels** > **Instellingen** > **Configuratie** > **Geavanceerd** > **Systeem**. Schuiven en klikken **Volledige paginacache**.

1. Zorg ervoor dat de **Caching-toepassing** waarde is ingesteld op _Fastly CDN_ .

1. Test de snelreferenties.

   - Klikken **Snelle configuratie**.

   - Verifieer dat de waarden voor Fastly identiteitskaart van de Dienst en Fastly API symbolische geloofsbrieven. Zie [Snelle gebruikersgegevens ophalen](/help/cloud-guide/cdn/fastly-configuration.md#get-fastly-credentials).

   - Klikken **Referenties testen**.

   >[!WARNING]
   >
   >Zorg ervoor dat u de juiste Fastly identiteitskaart van de Dienst en API teken in uw het Opvoeren en milieu&#39;s van de Productie inging. Snelle geloofsbrieven worden gecreeerd en in kaart gebracht per de dienstmilieu. Als u het Opvoeren geloofsbrieven in uw milieu van de Productie ingaat, kunt u uw fragmenten niet uploaden VCL, het in cache plaatsen werkt correct niet, en uw caching configuratie richt aan de verkeerde server en opslag.

**Het gedrag Snel in cache plaatsen controleren**:

1. Controleren op kopteksten met de opdracht `dig` bevel-lijn nut om informatie over de plaatsconfiguratie te krijgen.

   U kunt elke URL gebruiken met de `dig` gebruiken. In de volgende voorbeelden worden Pro-URL&#39;s gebruikt:

   - Staging: `dig https://mcstaging.<your-domain>.com`
   - Productie: `dig https://mcprod.<your-domain>.com`

   Voor extra `dig` testen, zie Fastly&#39;s [Testen voordat DNS wordt gewijzigd](https://docs.fastly.com/en/guides/working-with-domains).

1. Gebruiken `cURL` om de informatie van de reactiekopbal te verifiëren.

   ```bash
   curl https://mcstaging.<your-domain>.com -H "host: mcstaging.<your-domain.com>" -k -vo /dev/null -H Fastly-Debug:1
   ```

   Zie [Reactiekoppen controleren](../cdn/fastly-troubleshooting.md#check-cache-hit-and-miss-response-headers) voor meer informatie over het controleren van de kopteksten.

1. Wanneer u live bent, gebruikt u `cURL` om uw livesite te controleren.

   ```bash
   curl https://<your-domain> -k -vo /dev/null -H Fastly-Debug:1
   ```

## Volledige UAT-test

Complete User Acceptance Testing (UAT) on Staging and Production. De volgende tests zijn een snelle lijst van mogelijke taken en gebieden om als Merchant en Klant te testen. Uw lijst kan langer zijn en extra tests voor douanemodules, uitbreidingen, en derdesintegratie omvatten. Gebruik bij het testen desktops, laptops en mobiele apparaten.

Als u problemen ondervindt, slaat u de reproductiestappen, foutberichten, vreemde schermvastleggingen en koppelingen op. Gebruik deze informatie om kwesties in de code en configuraties van de integratieomgeving of milieu montages te onderzoeken en te bevestigen.

<table>
<tr>
<td style="width:150px">Gebruikersbeheer</td>
<td>
<ul>
<li>Customer accounts maken en bewerken, e-mails controleren</li>
<li>Beheerdersrollen maken voor verkopers</li>
<li>Zakelijke accounts maken met specifieke rollen</li>
<li>Toegang tot zakelijke account testen per rol</li>
</ul>
</td>
</tr>
<tr>
<td>Catalogi en producten</td>
<td>
<ul>
<li>Een catalogus maken met gekoppelde producten</li>
<li>Maak producten voor uw winkel, inclusief alle producttypen: eenvoudig, configureerbaar, gebundeld</li>
<li>Afbeeldingen, stalen, video's en andere mediaopties toevoegen</li>
<li>Prijs, kortingen, prijsregels configureren </li>
<li>Geavanceerde functies configureren, zoals prijsbereiken, aanbevolen producten, beschikbaarheidsdatums</li>
<li>De inventarisatie wijzigen en controleren of correcte waarden worden weergegeven en gewijzigd per verhoging en voltooide aankoop</li>
</ul>
</td>
</tr>
<tr>
<td>Houtskaarten en afhandeling</td>
<td>
<ul>
<li>Zoeken naar producten en filteropties selecteren</li>
<li>Producten uit zoekresultaten, categoriepagina's en productpagina's aan het winkelwagentje toevoegen</li>
<li>Alle producttypen testen</li>
<li>De winkelwagentje weergeven en de inhoud wijzigen door hoeveelheden te verwijderen of te wijzigen </li>
<li>Ga door het afrekenen om de bestelbedragen te verifiëren met behulp van de kar en productinformatie</li>
<li>Controleren of de belasting correct wordt berekend voor de winkelwagen</li>
<li>Een aankoop voltooien met andere opties: voeg een coupon toe, selecteer Verzending, voer de verzend- en factureringsgegevens en betalingsgegevens in</li>
<li>Betalingsgateways en -opties controleren tijdens het afrekenen</li>
<li>Controleren op meldingen op het scherm, bestellingen die worden vermeld in de klantenaccount en e-mailmeldingen</li>
<li>Uitchecken van gasten en klanten testen</li>
</ul>
</td>
</tr>
<tr>
<td>Orderbeheer</td>
<td>
<ul>
<li>Een bestelling voor een klant maken</li>
<li>Zoeken naar bestellingen en deze weergeven</li>
<li>Een bestelling wijzigen door producten toe te voegen en te verwijderen, bedragen te wijzigen, verzendgegevens en factureringsgegevens te wijzigen</li>
<li>Een restitutie afhandelen</li>
<li>Een bestelling annuleren</li>
<li>couponcodes en kortingen toepassen</li>
</ul>
</td>
</tr>
<tr>
<td>Site-inhoud</td>
<td>
<ul>
<li>Controleer of alle thema's en elementen correct zijn geladen</li>
<li>Controleren of CSS correct wordt weergegeven, inclusief responsieve mediaformaten</li>
<li>Bepalingen en voorwaarden controleren, restitutiebeleid en andere beleidsinformatie</li>
<li>Controleer contactgegevens, koppelingen en meer over uw bedrijf</li>
<li>Zoeken naar producten en inhoud, filteren van resultaten controleren</li>
<li>Verifieer de voettekstblok en de bovenste navigatieblokken</li>
<li>De 404- en onderhoudspagina's testen</li>
</ul>
</td>
</tr>
<tr>
<td>Extensies</td>
<td>
<ul>
<li>Controleer alle extensie-instellingen, met name voor alle fiscale modules, verzendings- en betalingsmodules (bijvoorbeeld: bestelling verzonden naar een entrepot en een systeem voor financieel beheer)</li>
<li>Alle aangepaste module- en geïnstalleerde extensieinteracties testen</li>
<li>Gegevens controleren op alle interacties die moeten worden voltooid (betalingen, bestellingen, e-mailmeldingen)</li>
<li>Configuraties per omgeving controleren op uw extensies</li>
<li>Verifieer gebiedsdelen tussen modules en uitbreidingswerk</li>
<li>Alle handelingen als handelaar en klant controleren</li>
</ul>
</td>
</tr>
<tr>
<td>Integraties van derden</td>
<td>
<ul>
<li>Controleren of gegevens correct worden opgeslagen in Adobe Commerce en worden geëxporteerd, geduwd of toegankelijk zijn voor de service van derden (bijvoorbeeld: bestellingen worden weergegeven in een orderbeheersysteem van derden)</li>
<li>Configuraties en interacties per integratie controleren</li>
<li>Rondleiding uitvoeren vanuit Adobe Commerce en uw service van derden</li>
<li>Controleren of verificatie is voltooid</li>
<li>Controleren op eventuele geregistreerde problemen om de integratie van code of foutberichten in besturingsdeelvensters bij te werken</li>
</ul>
</td>
</tr>
<tr>
<td>Testen op achtergrond</td>
<td>
<ul>
<li>Cache testen en wissen </li>
<li>Herindexen uitvoeren en resultaten verifiëren</li>
<li>Cron-taken controleren, op fouten cron_planning controleren</li>
<li>Controleren en controleren op problemen met shell-scripts</li>
<li>Controleren op eventuele geregistreerde problemen: toepassingslogboeken, PHP-logboeken, MySQL-logbestanden, e-maillogbestanden</li>
</ul>
</td>
</tr>
</table>

## Belasting- en stresstests

Voordat u de toepassing start, kunt u het beste uitgebreide verkeers- en prestatietests uitvoeren op uw testomgeving en productieomgeving. Overweeg prestatietests voor uw front-end en backend processen.

Voordat u begint te testen, voert u een ticket in met ondersteuning voor de omgevingen die u test, welke gereedschappen u gebruikt en het tijdframe. Werk het kaartje met resultaten en informatie bij om prestaties te volgen. Wanneer u klaar bent met testen, voegt u de bijgewerkte resultaten toe en noteert u dat de kaarttest is voltooid met een datum- en tijdstempel.

Controleer de [Prestatiewerkset](https://github.com/magento/magento2/tree/2.4/setup/performance-toolkit) -opties als onderdeel van het gereedheidsproces voorafgaand aan de start.

Gebruik de volgende gereedschappen voor de beste resultaten:

- [Toepassingsprestatie](../environment/variables-post-deploy.md#ttfb_tested_pages)—Test de toepassingsprestaties door te vormen `TTFB_TESTED_PAGES` omgevingsvariabele voor de responstijd van de testsite.
- [Siege](https://www.joedog.org/siege-home/)—Verkeersvormende en testende software om uw winkel tot het uiterste te duwen. Plaats uw site met een configureerbaar aantal gesimuleerde clients. Siege ondersteunt basisverificatie, cookies, HTTP-, HTTPS- en FTP-protocollen.
- [Jmeter](https://jmeter.apache.org)—Uitstekende ladingstests om prestaties voor verrijkt verkeer, zoals voor flitsverkoop te helpen meten. Aangepaste tests maken die op uw site worden uitgevoerd.
- [New Relic](../monitor/new-relic-service.md) (verstrekt) - Helpt van processen en gebieden van de plaats de plaats te bepalen die langzame prestaties veroorzaken met bijgehouden tijd die per actie zoals het overbrengen van gegevens, vragen, Redis, en meer wordt doorgebracht.
- [WebPageTest](https://www.webpagetest.org) en [VK](https://www.pingdom.com)—In real time analyse van uw plaatspagina&#39;s laadt tijd met verschillende oorsprongplaatsen. Het koninkrijk kan een vergoeding vragen. WebPageTest is een gratis hulpmiddel.

## Functionele tests

Met het MFTF (Magento Functional Testing Framework) kunt u functionele tests voor Adobe Commerce uitvoeren vanuit de Cloud Docker-omgeving. Zie [Toepassingen testen](https://developer.adobe.com/commerce/cloud-tools/docker/test/application-testing/) in de _Handleiding Cloud Docker voor handel_.

## Het gereedschap Beveiligingsscan instellen

Er is een gratis hulpprogramma voor beveiligingsscan voor uw sites. Als u uw sites wilt toevoegen en het gereedschap wilt uitvoeren, raadpleegt u [Beveiligingsscan](../launch/overview.md#set-up-the-security-scan-tool).
