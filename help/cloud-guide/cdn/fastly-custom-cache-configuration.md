---
title: Cacheconfiguratie aanpassen
description: Leer hoe u de instellingen van de cacheconfiguratie kunt controleren en aanpassen nadat de service Fastly is ingesteld.
feature: Cloud, Configuration, Iaas, Cache
exl-id: f1fc85d4-7867-4bb5-9f11-bc8d2d80383b
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 0%

---

# Cacheconfiguratie aanpassen

Nadat u opstelling en de Snelle dienst in uw het Staging en milieu&#39;s van de Productie test, herzie en pas montages van de geheim voorgeheugenconfiguratie aan. U kunt bijvoorbeeld instellingen bijwerken om ervoor te zorgen dat TLS HTTP-aanvragen snel kan doorsturen, instellingen voor leegmaken kan bijwerken en standaardverificatie kan inschakelen om uw site tijdens de ontwikkeling met een wachtwoord te beveiligen.

In de volgende secties vindt u een overzicht en instructies voor het configureren van bepaalde cacheinstellingen. Meer informatie over de beschikbare configuratieopties vindt u in het gedeelte [Fastly CDN Module for Magento 2](https://github.com/fastly/fastly-magento2/tree/master/Documentation) documentatie.

## TLS forceren

Met Fastly krijgt u de _TLS forceren_ optie voor het doorsturen van ongecodeerde aanvragen (HTTP) naar Fastly. Nadat u de staging- of productieomgeving van een [geldig SSL/TLS-certificaat](fastly-configuration.md#provision-ssltls-certificates), kunt u de snelste configuratie voor uw opslag bijwerken om de optie TLS forceren in te schakelen. Zie de snelst [TLS-handleiding forceren](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/FORCE-TLS.md) in de _Fastly CDN Module for Magento 2_ documentatie.

>[!NOTE]
>
>Het inschakelen van de optie TLS forceren is een aanbevolen werkwijze voor Adobe Commerce in de opslag van cloudinfrastructuur.

## Snelle time-out verlengen

In de Fastly-serviceconfiguratie wordt een standaardtime-outperiode van 180 seconden opgegeven voor HTTPS-aanvragen bij de beheerder. Om het even welke verzoekverwerking die de onderbrekingsperiode overschrijdt keert een fout 503 terug. Dientengevolge, kunt u 503 fouten in antwoord op verzoeken ontvangen die lange verwerking vereisen, of wanneer het proberen om bulkverrichtingen uit te voeren.

Voor het voltooien van bulkacties die langer dan 3 minuten duren, wijzigt u de instelling _Time-out beheerpad_ value_ om 503 fouten te voorkomen.

>[!NOTE]
>
>Als u snel time-outparameters wilt uitbreiden voor andere functies dan Admin in de snelkoppelingsinterface, raadpleegt u [Verhoog de time-outs voor lange taken](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-INCREASE-TIMEOUTS-LONG-JOBS.md).

**De snelste time-out voor de beheerder verlengen**:

{{admin-login-step}}

1. Klikken **Winkels** > Instellingen > **Configuratie** > **Geavanceerd** > **Systeem** en uitbreiden **Volledige paginacache**.

1. In de _Snelle configuratie_ sectie, uitvouwen **Geavanceerde configuratie**.

1. Stel de **Time-out beheerpad** waarde in seconden. Deze waarde mag niet langer zijn dan 10 minuten (600 seconden).

1. Klikken **Config opslaan** boven aan de pagina.

1. Nadat de pagina opnieuw is geladen, selecteert u **VCL snel uploaden naar** in de _Snelle configuratie_ sectie.

Hiermee wordt het beheerpad snel opgehaald voor het genereren van het VCL-bestand vanuit het dialoogvenster `app/etc/env.php` configuratiebestand.

## Opties voor leegmaken configureren

Kies deze optie om snel meerdere typen verwijderingsopties op de pagina Cache Management van uw Magento te plaatsen, waaronder opties voor het leegmaken van de productcategorie, de productelementen en de inhoud. Wanneer deze optie is ingeschakeld, zoekt Fastly naar gebeurtenissen om deze cache automatisch leeg te maken. Als u een optie voor leegmaken uitschakelt, kunt u de cache met snelheden handmatig leegmaken nadat de updates via de pagina Cachebeheer zijn voltooid.

De volgende opties voor leegmaken zijn beschikbaar:

- **Leegmaken, categorie**-Hiermee wordt de inhoud van een productcategorie (niet de inhoud van het product) gewist wanneer u één product toevoegt en bijwerkt. U kunt dit uitgeschakeld houden en leegmaken inschakelen, waardoor producten en productcategorieën worden gezuiverd.
- **Product leegmaken**-Hiermee wordt alle inhoud van het product en de productcategorie gewist wanneer één wijziging wordt opgeslagen in een product. Het inschakelen van een zuiveringsproduct kan handig zijn om direct updates aan klanten te krijgen wanneer u een prijs wijzigt, een productoptie toevoegt en wanneer de productvoorraad uit voorraad is.
- **CMS-pagina wissen**-Leegt pagina-inhoud bij het bijwerken en toevoegen van pagina&#39;s aan de Adobe Commerce CMS. U kunt bijvoorbeeld leegmaken bij het bijwerken van de voorwaarden of het retourbeleid. Als u deze wijzigingen zelden aanbrengt, kunt u automatisch leegmaken uitschakelen.
- **Zacht leegmaken**- Hiermee stelt u de gewijzigde inhoud in op schaal en paars volgens de tijdinstelling van de schaal. Naast de schaaltijdinstellingen worden klanten ook verouderde inhoud aangeboden, terwijl de inhoud op de achtergrond snel wordt bijgewerkt.

![Opties voor leegmaken configureren](../../assets/cdn/fastly-purge-options.png)

**Opties voor snel leegmaken configureren**:

1. In de _Snelle configuratie_ sectie, uitvouwen **Geavanceerde configuratie** om de opties voor leegmaken weer te geven.

1. Voor elke optie voor leegmaken selecteert u **Ja** automatisch leegmaken mogelijk te maken, of **Nee** om automatisch leegmaken uit te schakelen.

   Wanneer u een optie voor leegmaken uitschakelt, moet u de cache voor die categorie handmatig wissen vanuit de categorie _Cachebeheer_ pagina.

1. Klikken **Config opslaan** boven aan de pagina.

1. Nadat de pagina opnieuw is geladen, selecteert u **VCL snel uploaden naar** in de _Snelle configuratie_ sectie.

Zie voor meer informatie [de snelste configuratieopties](https://github.com/fastly/fastly-magento2/blob/21b61c8189971275589219d418332798efc7db41/Documentation/CONFIGURATION.md#further-configuration-options).

## GeoIP-afhandeling configureren

De module Snelheid bevat GeoIP-afhandeling om bezoekers automatisch om te leiden of om een lijst met winkels op te geven die overeenkomen met hun landcode. Als u al een extensie gebruikt voor GeoIP-afhandeling, moet u de functies mogelijk controleren met de opties Snelst.

**GeoIp-afhandeling instellen**:

{{admin-login-step}}

1. Klikken **Winkels** > Instellingen > **Configuratie** > **Geavanceerd** > **Systeem** en uitbreiden **Volledige paginacache**.

1. In de _Snelle configuratie_ sectie, uitvouwen **Geavanceerde configuratie**.

1. Omlaag schuiven en selecteren **Ja** tot **GeoIP inschakelen**. Er worden extra configuratieopties weergegeven.

1. Selecteer bij GeoIP-actie of de bezoeker automatisch wordt omgeleid met **Omleiden** of een lijst met winkels die u wilt selecteren **Dialoog**.

1. Voor **Landtoewijzing**, selecteert u **Toevoegen** om een landcode van twee letters in te voeren die u vanuit een lijst wilt koppelen aan een specifieke Adobe Commerce-winkel.

   ![GeoIP-landkaarten toevoegen](/help/assets/cdn/fastly-geo-code.png)

1. Klikken **Config opslaan** boven aan de pagina.

1. Selecteer **VCL snel uploaden naar** in de _Snelle configuratie_ sectie.

>[!NOTE]
>
>De huidige implementatie van de Adobe Commerce Fastly GeoIP-module ondersteunt geen omleidingen tussen meerdere websites.

Met Fastly beschikt u ook over een aantal [VCL-functies die betrekking hebben op geolocatie](https://developer.fastly.com/reference/vcl/variables/geolocation/) voor aangepaste geolocatiecodes.

## Snelrandmodules inschakelen

De snelste Modules van de Rand is een flexibel kader dat definitie van UI componenten en bijbehorende code VCL door een malplaatje toestaat. Deze modules maken het gemakkelijk om de Snelle de dienstconfiguratie door het gebruikersinterface aan te passen en uit te breiden in plaats van het gebruiken van de fragmenten van douaneVCL.

Met Edge-modules kunt u specifieke functionaliteit inschakelen, zoals CORS-headers, Cloud Sitemap herschrijft en integratie configureren tussen uw Adobe Commerce-winkel en andere CMS-systemen of backends.

Om tot het menu van de Modules van de Rand toegang te hebben om, de beschikbare modules te bekijken te vormen en te beheren, zet aan _Snelrandmodules inschakelen_ -optie. Zie [Snelrandmodules](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULES.md) in de Fastly CDN moduledocumentatie.

## Teruguiteinden en afscherming van oorsprong configureren

Back-end-instellingen zorgen voor fijnafstemming voor snelle prestaties met Oorsprong bescherming en time-outs. A _achterste einde_ is een specifieke plaats (IP of domein) met gevormde het schild van de Oorsprong en onderbrekingsmontages voor het controleren van en het verstrekken van caching inhoud.

_Oorspronkelijke afscherming_ leidt alle verzoeken om uw opslag aan een specifiek Punt van Aanwezigheid (POP). Wanneer een verzoek wordt ontvangen, controleert POP caching inhoud en verstrekt het. Als de inhoud niet in de cache wordt opgeslagen, gaat deze verder naar de POP Shield en vervolgens naar de server Origin die de inhoud in de cache plaatst. De schilden verminderen direct verkeer aan de oorsprong.

De standaard VCL-code met snelheden geeft standaardwaarden op voor Oorspronkelijke beveiliging en time-outs voor uw Adobe Commerce op cloudinframesites. In sommige gevallen moet u mogelijk de standaardwaarden wijzigen. Bijvoorbeeld, als u Tijd aan Eerste fouten van de Byte (TTFB) krijgt, zou u kunnen moeten aanpassen _time-out eerste byte_ waarde.

>[!NOTE]
>
>Als uw site functioneel moet worden geleverd via een back-endintegratie, zoals [Wordpress](fastly-vcl-wordpress.md), kunt u uw Fastly-serviceconfiguratie aanpassen om de back-end toe te voegen en omleidingen van uw Adobe Commerce-winkel naar Wordpress te beheren. Zie voor meer informatie [Snelrandmodules - Overige CMS/Backend-integratie](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-OTHER-CMS-INTEGRATION.md) in de documentatie van de module Snelheid.

**De configuratie van de achterste instellingen bekijken**:

{{admin-login-step}}

1. Klikken **Winkels** > Instellingen > **Configuratie** > **Geavanceerd** > **Systeem** en uitbreiden **Volledige paginacache**.

1. Breid uit **Snelle configuratie** sectie.

1. Uitbreiden **Instellingen voor achtergrond** en selecteert u het tandwiel om het standaardachteruiteinde te controleren. Er wordt een modaal dialoogvenster geopend waarin de huidige instellingen worden weergegeven met opties om deze te wijzigen.

   ![Het achteruiteinde wijzigen](../../assets/cdn/fastly-backend.png)

1. Selecteer de **Schild** locatie (of datacenter).

   Met de standaardsnelconfiguratie voor uw project stelt u de locatie in die het dichtst bij uw cloudservicegebied ligt. Als u deze wilt wijzigen, selecteert u een locatie dicht bij de standaardlocatie.

1. Wijzig de time-outwaarden (in microseconden) voor de verbinding met het scherm, de tijd tussen bytes en de tijd voor de eerste byte. We raden u aan de standaardtime-outinstellingen te behouden.

1. Selecteer indien nodig **De achtergrond en de bescherming activeren na bewerken of opslaan**.

1. Klikken **Uploaden** om uw wijzigingen op te slaan en te uploaden naar de snelste servers.

1. Selecteer in Beheer de optie **Config opslaan**.

Zie de klasse [Hulplijn voor achtergrondinstellingen](https://github.com/fastly/fastly-magento2/blob/21b61c8189971275589219d418332798efc7db41/Documentation/Guides/BACKEND-SETTINGS.md) in de documentatie van de module Snelheid.

## Basisverificatie

Standaardverificatie is een functie waarmee u elke pagina en elk element op uw site kunt beveiligen met een gebruikersnaam en wachtwoord. Wij **niet aanbevelen** het activeren van basisauthentificatie op uw milieu van de Productie. U kunt het vormen op Staging om uw plaats tijdens het ontwikkelingsproces te beschermen. Zie de [Basishandleiding voor verificatie](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BASIC-AUTH.md) in de Fastly CDN moduledocumentatie.

Als u gebruikerstoegang toevoegt en basisauthentificatie bij het Opvoeren toelaat, kunt u tot Admin nog toegang hebben zonder extra geloofsbrieven te vereisen.

## Aangepaste VCL-fragmenten maken

Steunt snel een aangepaste versie van de Taal van de Configuratie van de Varnish (VCL) om de Snelle de dienstconfiguratie aan te passen. U kunt bijvoorbeeld toegang voor bepaalde gebruikers of IP-adressen toestaan, blokkeren of omleiden met VCL-codeblokken met de woordenboeken Rand en Toegangsbeheer (ACL).

Voor instructies om de fragmenten van douaneVCL, randwoordenboeken, en ACLs tot stand te brengen, zie [Aangepaste, snel VCL-fragmenten](fastly-vcl-custom-snippets.md).

>[!NOTE]
>
>Alvorens douanecode VCL, randwoordenboeken, en ACLs aan uw Fastly moduleconfiguratie toe te voegen, verifieer dat de Fastly caching dienst met de standaardconfiguratie werkt. Zie [Snel instellen](fastly-configuration.md).

## Domeinen beheren

Voor zowel de projecten van de Aanzet als van Pro, kunt u gebruiken [!UICONTROL Domains] om de snelste domeinconfiguratie voor uw winkel toe te voegen en te beheren.

- Ga voor Starter-projecten naar Project URL onder de [!UICONTROL Domains] in de [!DNL Cloud Console] om uw project-URL toe te voegen.

- Voor Pro-projecten dient u een [Adobe Commerce-ondersteuningsticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om het domein aan uw configuratie van het wolkenproject toe te voegen. Het ondersteuningsteam werkt ook de Adobe Commerce Fastly-accountconfiguratie bij om het domein toe te voegen.

**Domeinconfiguratie snel beheren vanuit de beheerder**:

{{admin-login-step}}

1. Selecteren **Winkels** > Instellingen > **Configuratie** > **Geavanceerd** > **Systeem** en uitbreiden **Volledige paginacache**.

1. In de beheerder _Snelle configuratie_ sectie, selecteert u **Domeinen**.

1. Klikken **Domeinen beheren** om de pagina Domains te openen.

1. Voeg de namen van het hoogste niveau en subdomein toe voor de winkels in de Cloud-omgeving.

   U kunt alleen domeinen opgeven die al zijn toegevoegd aan de configuratie van de Cloud-infrastructuur.

   ![Voeg snel domeinconfiguratie voor Starter toe](../../assets/cdn/fastly-starter-activate-domain.png)

1. Klikken **Activeren** om de Fastly domeinconfiguratie bij te werken.

>[!NOTE]
>
>Als hetzelfde domein is geconfigureerd op een andere snelaccount, moet u een Adobe Commerce-ondersteuningsticket indienen om Domeindelegatie aan te vragen voordat u het domein kunt toevoegen aan Adobe Commerce. Zie [Meerdere snelaccounts en toegewezen domeinen](fastly.md#multiple-fastly-accounts-and-assigned-domains).

## Onderhoudsmodus inschakelen

Gebruik de _Onderhoudsmodus_ optie om administratieve toegang tot uw plaats van gespecificeerde IP adressen toe te staan terwijl het terugkeren van een foutenpagina voor alle andere verzoeken.

**Onderhoudsmodus inschakelen met beheertoegang**:

1. Open de _Snelle configuratie_ in de Admin.

1. In de _Edge ACL_ sectie, update de `maint_allow` toegangsbeheerlijst (ACL) met de administratieve IP adressen die tot uw opslag kunnen toegang hebben terwijl het op de wijze van het Onderhoud is.

   ![Lijst van gewenste personen IP-onderhoudsmodus bijwerken](../../assets/cdn/fastly-maint-allowlist.png)

1. In de _Onderhoudsmodus_ sectie, selecteert u **Onderhoudsmodus inschakelen**.

   Nadat u onderhoudswijze toelaat, wordt al verkeer geblokkeerd behalve verzoeken van de IP adressen in `maint_allowlist` ACL. U kunt de `maint_allowlist` om de IP adressen in ACL te veranderen.

   Voor gedetailleerde configuratieinstructies, zie [Handleiding voor onderhoudsmodus](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/MAINTENANCE-MODE.md) in Fastly CDN voor Magento 2 moduledocumentatie.
