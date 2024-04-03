---
title: Cloud-patches voor handel
description: Zie een lijst met de meest recente verbeteringen in het pakket met cloudpatches.
recommendations: noDisplay, catalog
last-substantial-update: 2024-01-16T00:00:00Z
exl-id: ae6b511b-a37d-4776-9a5e-ad7d9f9f6611
source-git-commit: 1e06545340cb63df483d1db5b2a890499e99e6d3
workflow-type: tm+mt
source-wordcount: '2175'
ht-degree: 0%

---

# Cloud-patches voor handel

De [Cloudpatches](https://github.com/magento/magento-cloud-patches) Dit pakket biedt een aantal vereiste patches die de integratie van alle Adobe Commerce-versies met Cloud-omgevingen verbeteren en snelle levering van kritieke oplossingen ondersteunen.

Het pakket Cloud Patches for Commerce is een afhankelijkheid van het pakket ECE-Tools en wordt geïnstalleerd en bijgewerkt wanneer u het pakket ECE-Tools installeert of bijwerkt. U kunt Cloud Patches voor Handel ook gebruiken en beheren als een zelfstandig pakket om patches toe te passen op een Adobe Commerce-project dat zich niet op het Cloud-platform bevindt. In deze releaseopmerkingen worden de meest recente verbeteringen aan dit pakket beschreven.

>[!TIP]
>
>Als u ervoor wilt zorgen dat uw project alle vereiste patches bevat, moet u de update naar de [nieuwste versie van ece-tools](../dev-tools/update-package.md).

>[!NOTE]
>
>Zie [Patches toepassen](../development/apply-patches.md) voor instructies over het toepassen van flarden op uw projecten.

De `magento/magento-cloud-patches` het pakket gebruikt de volgende versiereeks: `<major>.<minor>.<patch>`

<!--Add release notes below-->

## v1.0.25 {#latest}

Releasedatum: 16 januari 2024

- **Cacheverbeteringen**- Deze patch verbetert de efficiëntie van de lay-outcache, waardoor het geheugengebruik aanzienlijk wordt verminderd, voor Adobe Commerce versie 2.4.4 en hoger.<!-- MCLOUD-11514 -->
- **Verbeteringen van CRON-taken**- Deze patch verhelpt het probleem dat gemiste taken onnodig wachten op tijdelijke taakvergrendeling voor Adobe Commerce versie 2.4.4 en hoger.<!-- MCLOUD-11329 -->

## v1.0.24

Releasedatum: 15 september 2023

- **Prestatieverbetering**-Deze patch verhelpt een probleem dat de prestaties beïnvloedt door het aantal keer dat dezelfde implementatieconfiguraties voor Adobe Commerce 2.4.6 tot 2.4.6-p1 worden belast, te verminderen<!-- MCLOUD-10604 -->

## v1.0.23

Releasedatum: 31 juli 2023

- **De patch MCLOUD-10604 is verwijderd**- Deze patch is verplaatst naar QPT.<!-- MCLOUD-10736 -->

## v1.0.22

Releasedatum: 19 juni 2023

- **Verbeterde wizard QPT CLI/uitvoer**—Toegevoegd een waarschuwing aan de tovenaar/output QPT CLI die u eraan herinnert om flarddetails en vereisten te verifiëren als er gebiedsdelen zijn.<!-- ACP2E-1963 -->
- **Toegevoegde flarden voor Handel 2.4.6:**
   - Vaste het `regexp cache tag` validatie.<!-- MCLOUD-10226 -->
   - Verbeterde prestaties door het aantal keren dat dezelfde implementatieconfiguraties worden geladen te verminderen.<!-- MCLOUD-10604 -->
- **Toegevoegde flarden voor Handel 2.3.7 tot 2.4.6**—Oplossing voor een probleem dat een verhoging met een willekeurige waarde in plaats van een verhoging met 1 voor de `catalog_product_entity_*` tabellen.<!-- MCLOUD-10032 -->
- **Toegevoegde flarden voor Handel 2.4.0 tot 2.4.6**—Oplossing voor een fout die aangeeft dat: `The file can't be deleted. Warning!unlink: No such file or directory`, die optrad bij het leegmaken van de JS/CSS-cache van de Admin.<!-- MCLOUD-10279 -->

## v1.0.21

Releasedatum: 10 maart 2023

- **Verbeterde ondersteuning voor PHP 8.2**—Oplossingen voor compatibiliteitsproblemen met bepaalde PHP 8.2.x-versies ter ondersteuning van Commerce 2.4.6.

## v1.0.20

Releasedatum: 27 oktober 2022

- **Verbeteringspatch voor L2-cache toegevoegd**—Deze patch verhelpt een probleem met het leegmaken van de lokale L2-cache voor Commerce versie 2.4.0 en 2.4.1.<!-- MCLOUD-7845 -->

## v1.0.19

Releasedatum: 13 september 2022

- **Verbeterde ondersteuning voor PHP 8.1**—Oplossing voor compatibiliteitsproblemen met bepaalde PHP 8.1.x-versies.

## v1.0.18

Releasedatum: 11 augustus 2022

Kritieke patch voor Adobe Commerce 2.4.5:

- **Uitgifte van orders met behulp van Braintree betalingen**—Deze patch verhelpt een kritiek probleem dat voorkomt dat beheerders nieuwe orders plaatsen of opnieuw rangschikken.<!-- MCLOUD-9137 -->

Zie [Beheerder kan geen bestelling/herschikking maken wanneer betaling via Braintree is ingeschakeld](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/admin-cant-create-order-reorder-when-braintree-payment-enabled.html).

## v1.0.17

Releasedatum: 24 mei 2022

Vaste beperkingen voor beveiligingspatches in het dialoogvenster `patches.json` bestand.

## v1.0.16

Releasedatum: 31 maart 2022

Kritieke patch voor Adobe Commerce 2.3.3-p1 en latere versies:

Bijgewerkte patches om een **kritisch** kwetsbaarheid die resulteert in de uitvoering van niet-geverifieerde externe code.<!-- MCLOUD-8479 -->

Zie [Adobe Beveiligingsbulletin APSB22-12](https://helpx.adobe.com/security/products/magento/apsb22-12.html).

## v1.0.15

Releasedatum: 10 maart 2022

- **Ondersteuning voor PHP 8.1**—Toegevoegde ondersteuning voor PHP 8.1 en verwijderde ondersteuning voor PHP 7.0 en 7.1.
- **Toegevoegde patch voor Adobe Commerce 2.3.3**—Vaste valutawaarde die wordt weergegeven op de productpagina.

## v1.0.14

Releasedatum: 13 februari 2022

Kritieke patch voor Adobe Commerce 2.3.3-p1 en latere versies:

Een pleister toegevoegd om een **kritisch** kwetsbaarheid die resulteert in de uitvoering van niet-geverifieerde externe code.<!-- MCLOUD-8461 -->

Zie [Adobe Beveiligingsbulletin APSB22-12](https://helpx.adobe.com/security/products/magento/apsb22-12.html).

## v1.0.13

Releasedatum: 25 oktober 2021

- **Monolog bijwerken**—De minimale versie die vereist is voor de `monolog` verpakken naar `^2.3`.<!-- ACMP-1263 -->
- **Incompatibele PHP-methode**—Fixed incompatible PHP method for Adobe Commerce versions 2.4.3 and 2.3.7-p1.<!-- AC-384 -->
- **PHP-fout**—Vast a `PHP error 'Undefined variable: errorMessage' ...` fout die is opgetreden tijdens het toepassen van een patch.<!-- ACP2E-138 -->

## v1.0.12

Releasedatum: 12 augustus 2021

Kritieke patch voor Adobe Commerce 2.4.3 en 2.3.7-p1:

- **Probleem met beperking van API-snelheid**—Deze patch corrigeert een standaard snelheidsgrens die Web APIs verhinderde verzoeken met meer dan 20 punten in een serie te verwerken. Deze patch verhoogt de standaardwaarde van de tariefgrens. Zie de Adobe Commerce [2.4.3 Opmerkingen bij de release](https://devdocs.magento.com/guides/v2.4/release-notes/commerce-2-4-3.html#apply-mc-43048__set_rate_limits__243patch-to-address-issue-with-api-rate-limiting) en de [2.3.7 Opmerkingen bij de release](https://devdocs.magento.com/guides/v2.3/release-notes/2-3-7-p1.html#apply-mc-43048__set_rate_limits__237-p1patch-to-address-issue-with-api-rate-limiting).<!-- MC-43048 -->

## v1.0.11

Releasedatum: 29 juli 2021

- **Probleem verholpen dat werd veroorzaakt door het toepassen van de B2B gelaagde navigatiepatch**—Voor klanten die de B2B Gelaagde navigatiepatch hebben toegepast, lost deze moeilijke situatie een op `Undefined offset` fout die op de zoekpagina wordt weergegeven nadat de winkelweergave is gewijzigd.<!--MCLOUD-5287-->

- **Paypal-uitcheckpatch**—Oplossing voor een Adobe Commerce 2.3.7-probleem met PayPal Express waarbij de eerder geplaatste bestellingsprijs wordt weergegeven.<!--MC-42674-->

- **Ondersteuning voor patchcategorieën**—Toegevoegde ondersteuning voor de verwerking van patchcategorieën en oorspronkelijke bronnen die zijn toegewezen aan Quality Patches. Met de categorieën kunnen klanten filters en sortering gebruiken om sneller patches te zoeken wanneer ze de opdracht [Gereedschap Kwaliteitspatches](https://github.com/magento/quality-patches) en het hulpmiddel van de Analyse voor de hele Plaats (SWAT). <!--MC-38577-->

## v1.0.10

Releasedatum: 10 mei 2021

- **Compatibiliteit met Adobe Commerce 2.3.7**—Conflict met opgeloste composer-afhankelijkheden voor installatie op Adobe Commerce 2.3.7.<!--MC-42131-->
- **Probleem verholpen die werd veroorzaakt door meerdere keren een gebundelde patch toe te passen**—Als u een gebundelde patch (een die andere verouderde patches bevat) meerdere keren toepast, kunt u de meegeleverde verouderde pakketten herstellen. Alle pleisters worden nu slechts eenmaal aangebracht. Wanneer u hetzelfde pakket opnieuw probeert toe te passen, wordt een bericht weergegeven dat de patch al is toegepast.<!--MC-41912-->
- **B2B gelaagd navigatiepatroon**—Oplossing voor een ander probleem dat ervoor zorgde dat bij gelaagde navigatie alle productopties konden worden weergegeven wanneer de gebruiker de B2B-gedeelde catalogus inschakelde.<!--MCLOUD-7742-->

## v1.0.9

Releasedatum: 1 februari 2021

- **B2B gelaagd navigatiepatroon**—Oplossing voor het probleem dat ervoor zorgde dat bij gelaagde navigatie alle productopties konden worden weergegeven wanneer de B2B-gedeelde catalogus was ingeschakeld.<!--MCLOUD-6923-->
- **Compatibiliteit met PHP 7.4**—Oplossing voor een &#39;cloud patches&#39;-compatibiliteitsprobleem met PHP 7.4.<!--MCLOUD-7367-->
- **Verouderde patches worden zichtbaar**—Probleem verholpen waarbij verouderde patches zichtbaar worden in de patchtabel nadat een vervangende patch is toegepast die de volledige inhoud van de vervangen patch bevat. Dit kan gebeuren als u een pleister aanbrengt die verschillende andere pleisters combineerde.<!--MC-40626-->
- **Stille fouten bij het toepassen van patches**—Oplossing voor een &#39;cloud patches&#39;-probleem waarbij de `git apply` in sommige omgevingen kan de opdracht in stilte geen patches worden toegepast.<!--MC-40529-->

## v1.0.8

Releasedatum: 14 oktober 2020

- **Compatibiliteitsupdates voor magento/magento-cloud-patches**—De `symfony` en `semver` versiebeperkingen in de `composer.json` bestand voor compatibiliteit met Adobe Commerce 2.4.1 en latere versies.<!--MCLOUD-7111-->

## v1.0.7

Releasedatum: 14 oktober 2020

- **Redis patches voor Adobe Commerce 2.3.0 tot 2.3.5, 2.4.0**—De Redis-patches zijn bijgewerkt om het toevoegen van producten aan een categorie te ondersteunen bij de implementatie van een Level 2-cache. <!--MCLOUD-6659-->

- **Braintree VBE patch**—Hiermee wordt een fout verholpen die een fout heeft gegenereerd wanneer een beheerder een Braintree Settlement Report probeerde weer te geven. <!--MCLOUD-6684-->

- Nu, `ece-patches apply` gebruiken Unix `patch` gebruiken om patches toe te passen als Git niet beschikbaar is op het hostsysteem. <!--MCLOUD-7069-->

## v1.0.6

Releasedatum:

- **Redis patches voor Adobe Commerce 2.3.0 - 2.3.4**—Communicatie optimaliseren en prestaties verbeteren
   - De omvang van netwerkoverdrachten tussen Redis en Adobe Commerce verkleinen
   - Omgevingsfactoren bij laden en schrijven van Redis verhelpen
   - Basiscacheadapter opnieuw schrijven om fouten af te handelen bij het opslaan
   - Verlaag het CPU-verbruik van Redis<!--MCLOUD-6139-->

- **Redis patches voor Adobe Commerce 2.3.0 - 2.3.5**—Prestaties verbeteren en fouten verhelpen
   - Verbeter de implementatie van het cachevergrendelen om oneindige vergrendelingen te voorkomen
   - Het huidige vergrendelingsmechanisme verbeteren
   - Ondertekende vergrendelingen implementeren om te voorkomen dat parallelle aanvragen worden ontgrendeld
   - Verbeter de volgende fout die bij Redis schrijfbewerking optreedt: `OOM command not allowed when used memory > maxmemory`
   - Verwerking corrigeren voor onbewerkte cache met `cat_p` tag die wordt uitgevoerd tijdens productupdates<!--MCLOUD-6110-->

- Probleem verholpen dat een fout veroorzaakte bij het toepassen van de vereiste `amzn/amazon-pay-module` patch naar Adobe Commerce voor cloud-infrastructuurprojecten met Adobe Commerce v2.2.6 of 2.3.5, die deze module niet bevatten. Het patchproces slaat nu de `amzn/amazon-pay-module` als de module niet is geïnstalleerd.<!--MCLOUD-6588-->

## v1.0.5

Releasedatum: 26 juni 2020

- **Prestatieverbeteringen voor Redis**—Voegt Redis-optimalisatiefuncties toe aan Adobe Commerce versie 2.3.3 en 2.3.4. Deze correcties zijn opgenomen in de Adobe Commerce-versie 2.3.5. Zie [Prestatieverbeteringen](https://devdocs.magento.com/guides/v2.3/release-notes/release-notes-2-3-5-commerce.html#performance-boosts) in de _Opmerkingen bij de release Adobe Commerce 2.3.5_.<!--MCLOUD-5771-->

- **New Relic log enricher**—Voegt de Monolog ProcessorInterface toe die nodig is ter ondersteuning van verbeteringen in New Relic-logboekmogelijkheden die zijn geïntroduceerd in Cloud Components of Commerce versie 1.0.4. Deze patch is vereist voor de implementatie van Adobe Commerce 2.1.x. Als het flard niet wordt toegepast, ontbreekt de bouwstijl tijdens `di:compile` proces.<!--MCLOUD-6029-->

## v1.0.4

Releasedatum: 12 mei 2020

- **Afhandeling via Amazon Betalen**—Hiermee wordt een probleem verholpen met de Amazon Pay-betalingswidget waardoor klanten de betalingsmethode op de _Reviseren en betalen_ stap tijdens het uitcheckproces.<!--MCLOUD-5930-->

- **Productweergave op rubriekpagina**—Hiermee verhelpt u een probleem waardoor producten niet op de categoriepagina kunnen worden weergegeven in _Alle pagina&#39;s tonen_ weergeven.<!--MCLOUD-5684-->

- **Uploaden van afbeelding in Page Builder**—Het interfaceprobleem van de Bouwer van de Pagina wordt verholpen dat soms de volgende fout veroorzaakte wanneer het uploaden van beelden aan de beeldgalerij: `Destination folder is not writable or does not exist`<!--MCLOUD-5837-->

- **Overbodige sitemapgeneratiewaarschuwingen onderdrukken**—Voegt een poging toe om opnieuw te proberen wanneer de fouten tijdens de productie van sitemap voorkomen en slaat klanten e-mailbericht in gevallen over waar de fouten automatisch kunnen worden teruggekregen.<!--MCLOUD-3025-->

- **Verbetering van de prestaties van sites**—Oplossing voor een prestatieprobleem met de `Magento\Framework\App\DeploymentConfig\Reader::load` die periodiek lange laadtijden doormaakten die de prestaties van de site beïnvloedden. <!--MCLOUD-5650-->

- Bijgewerkte patchtoewijzing voor patches voor betalingsmethoden om de betalingsmodules als doel in te stellen in plaats van het basispakket van het Magento (magento/magento2-base), zodat de betalingspatches alleen worden toegepast als de betalingsmodules bestaan.<!--MCLOUD-5666-->

- Bijgewerkte patches voor compatibiliteit met Magento Open Source.<!--MCLOUD-5701-->

## v1.0.3

Releasedatum: 28 april 2020

- Toegevoegde oplossing voor de patch &quot;FPC wordt uitgeschakeld tijdens implementaties&quot; ter ondersteuning van Adobe Commerce 2.3.5.

## v1.0.2

Releasedatum: 27 februari 2020

Deze release bevat de volgende patches en oplossingen voor problemen:

- **Compatibiliteitsupdates voor magento/magento-cloud-patches**

   - De `symfony` en `semver` versiebeperkingen in de `composer.json` bestand voor compatibiliteit met Adobe Commerce 2.4 en latere versies.<!--MAGECLOUD-5127-->

   - Bijgewerkte beperkingen in `composer.json` voor compatibiliteit met `ece-tools` 2002.0.22 en latere versies van 2002.0.x.

- **PayPal Express-afhandeling**—Gepubliceerd op 12 februari 2020 verhelpt deze patch een probleem dat van invloed is op bestellingen die worden geplaatst met PayPal Express Checkout, waarbij het verzendadres voor de bestelling een landgebied opgeeft dat handmatig in het tekstveld is ingevoerd in plaats van te zijn geselecteerd in het vervolgkeuzemenu op de verzendpagina. Zie de volledige patchbeschrijving op de pagina voor het downloaden van de patch.

- **Implementatieoplossing voor toepassingen**—Er is een patch toegevoegd om een probleem op te lossen dat het cachegeheugen van de volledige pagina tijdens het implementatieproces heeft uitgeschakeld. Deze patch is van toepassing op Adobe Commerce 2.3.2 en latere versies.

- **Toepassingsparameter voor Async/Bulk-API**—Deze patch is bijgewerkt om een syntaxisfout in het dialoogvenster `composer.json` bestand. Deze patch is van toepassing op Magento Open Source 2.3.1 en 2.3.2. Zie de volledige patchbeschrijving op de pagina voor het downloaden van de patch.

## v1.0.1

Releasedatum: 6 februari 2020

We hebben alle Magento Open Source 2.x-patches van de downloadpagina voor software opgenomen in de release magento/magento-cloud-patches v1.0.1. Als u eerder patches naar uw project hebt gekopieerd, verwijdert u deze om conflicten te voorkomen.

Deze release bevat de volgende patches en oplossingen voor problemen:

- **Blokkeringen van uitsnijden corrigeren en de vergrendeling van uitsneden verbeteren**—

   - Hiermee wordt een probleem verholpen waarbij bepaalde snijtaken niet worden uitgevoerd vanwege een onjuiste statuswaarde in het dialoogvenster `cron_schedule` tabel. Nu gebruiken we het Adobe Commerce-vergrendelingsframework om de status van een snijtaak te controleren en bij te werken in plaats van de `cron_schedule` tabel. Cron-taken die met een foutstatus zijn geëindigd, worden opnieuw uitgevoerd tijdens de volgende uitsnijding in plaats van 24 uur te wachten.

   - Hiermee voegt u een _opnieuw proberen_ om blokkering te voorkomen tijdens updates van de gegevens in de `cron_schedule` tabel.

- **Bijgewerkt `magento/magento-cloud-patches` om alle beschikbare patches voor Magento Open Source 2.x op te nemen**—Het magento/magento-cloud-patches-pakket is bijgewerkt met alle Magento Open Source 2.x-patches die beschikbaar zijn op de pagina voor softwaredownloads. Als u eerder Magento Open Source-patches naar uw Adobe Commerce hebt gekopieerd voor een cloudinfrastructuurproject, verwijdert u deze om conflicten te voorkomen.<!--MAGECLOUD-4606-->

- **Pagineringscorrectie voor catalogus van Elasticsearch** —Vervangen van de pagineringspatch voor de catalogus van de Elasticsearch die in magento/magento-cloud-patches v1.0 is geleverd met een efficiëntere oplossing.<!--MAGECLOUD-4847-->

- **Patches voor Page Builder**—In Cloud Patches for Commerce 1.0.0 hebben we patches voor Page Builder gebundeld om een bekende RCE-kwetsbaarheid (Remote Code Execution) van Page Builder aan te pakken. De eerste oplossing is gebaseerd op Adobe Commerce 2.3.3. We hebben deze patches bijgewerkt met een stabielere implementatie op basis van Adobe Commerce 2.3.4., die meerdere optimalisaties voor het oplossen van het probleem omvat.<!--MAGECLOUD-4884-->

  Als u het pakket magento/magento-cloud-patches 1.0.0 hebt, bent u nog steeds beschermd tegen de kwetsbaarheidsproblemen met RCE van Page Builder. Als u aan 1.0.1 of later bijwerkt, hebt u een betere implementatie van de zelfde moeilijke situatie.

## v1.0.0

Releasedatum: 14 november 2019

Dit is de eerste release van het [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) een nieuwe afhankelijkheid van de `ece-tools` pakketversie 2002.0.22 of hoger.

Deze release bevat de volgende patches en oplossingen voor problemen:

- **Beveiligingspatches voor 2.3.1.x en 2.3.2.x van Page Builder**—Oplossingen een kwestie in de voorproef van de Bouwer van de Pagina die unauthenticated gebruikers toestaat om tot sommige malplaatjemethodes toegang te hebben die kunnen worden gebruikt om willekeurige codeuitvoering over het netwerk (RCE) te teweegbrengen resulterend in globale informatielekken. Dit probleem kan optreden wanneer niet-ondersteunde versies van Page Builder worden gebruikt met Adobe Commerce versie 2.3.1 en 2.3.2.<!--MAGECLOUD-4649-->

- **MSI-patches**—Hiermee worden problemen verholpen die indexatiefouten en prestatieproblemen hebben veroorzaakt bij het gebruik van standaardinstellingen voor inventarisatie voor het beheer van voorraden.<!--MAGECLOUD-4428-->

- **Achterwaartse Verenigbaarheid van nieuwe Interfaces van de Post**-Oplossing voor een probleem met achterwaartse incompatibiliteit dat wordt veroorzaakt door de `Magento\Framework\Mail\EmailMessageInterface` PHP interface created in Adobe Commerce v2.3.3. In het bereik van deze patch worden de nieuwe `EmailMessageInterface` erft van de oude `MessageInterface`en Adobe Commerce-kernmodules zijn weer afhankelijk van `MessageInterface`.<!--MAGECLOUD-4422-->

- **Paginering van catalogi werkt niet op Elasticsearch 6.x**—Hiermee verhelpt u een kritiek probleem met de paginering van zoekresultaten dat gevolgen heeft voor klanten die Elasticsearch 6.x als zoekprogramma voor catalogi gebruiken.<!--MAGECLOUD-4448-->
