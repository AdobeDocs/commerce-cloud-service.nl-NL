---
title: Services voor snel configureren
description: Leer hoe u snelle services instelt en configureert voor uw Adobe Commerce-project.
feature: Cloud, Configuration, Iaas, Cache, Security
exl-id: c53ff3bd-3df2-45fb-933e-d3b29f7edf4e
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '1961'
ht-degree: 0%

---

# Services voor snel configureren

Snelheid is vereist voor Adobe Commerce op omgevingen voor het opslaan en produceren van cloudinfrastructuur.

Met Varnish werkt u snel in cache en een [Inhoudsleveringsnetwerk](https://glossary.magento.com/content-delivery-network) (CDN) voor statische elementen. Verstrekt snel ook een Firewall van de Toepassing van het Web (WAF) om uw plaats en infrastructuur van de Wolk te beveiligen. Om uw plaats en infrastructuur van de Wolk tegen kwaadwillig verkeer en aanvallen te beschermen, route al inkomend plaatsverkeer door Snelst.

>[!NOTE]
>
>Snelheid is niet beschikbaar in integratieomgevingen.

Voer de volgende stappen uit om uw site snel in te schakelen, te configureren en te testen, zodat u veilig toegang hebt tot uw site.

- Krijg Snelle geloofsbrieven voor het Opvoeren en van de Productie milieu&#39;s
- SNELLE CDN-caching inschakelen
- VCL-fragmenten snel uploaden
- DNS van de update configuratie aan routeverkeer aan de Snelle dienst
- Snelle caching testen

>[!NOTE]
>
>Nadat u de eerste snelconfiguratie hebt ingeschakeld en geverifieerd, kunt u de configuratie aanpassen. U kunt bijvoorbeeld aanvullende opties inschakelen, zoals optimalisatie van afbeeldingen, randmodules en aangepaste VCL-code. Zie [Cacheconfiguratie aanpassen](fastly-custom-cache-configuration.md).

## Snelle gebruikersgegevens ophalen

Tijdens projectlevering, voegt de Adobe uw project aan [Snelle serviceaccount](fastly.md#fastly-service-account-and-credentials) voor Adobe Commerce op cloud-infrastructuur en maakt snel accountgegevens voor de Starter `master` en Pro Staging and Production-omgevingen. Elke omgeving heeft unieke referenties.

U hebt de Fastly geloofsbrieven nodig om de Snelle diensten CDN van Admin te vormen en Fastly API verzoeken voor te leggen.

>[!NOTE]
>
>Met Adobe Commerce op cloudinfrastructuur hebt u niet rechtstreeks toegang tot de snelbeheerder. Gebruik de beheerder om de snelconfiguratie voor uw omgevingen te controleren en bij te werken. Als u een probleem niet kunt oplossen met de snelste functies in de beheerder, verzendt u een [Adobe Commerce-ondersteuningsticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket).

Gebruik de volgende methoden om de Fastly-service-id en API-token voor uw omgeving te zoeken en op te slaan:

**Uw gegevens snel weergeven**:

De methode voor het bekijken van geloofsbrieven is verschillend voor Pro en de projecten van de Aanzet.

- Op IaaS gemonteerde gedeelde folder-op Pro projecten, gebruik SSH om met uw server te verbinden en de Fastly geloofsbrieven van te krijgen `/mnt/shared/fastly_tokens.txt` bestand. Staging- en productieomgevingen hebben unieke gegevens. U moet de geloofsbrieven voor elke milieu krijgen.

- De lokale werkruimte—Van de bevellijn, gebruik `magento-cloud` CLI naar [lijst en revisie](../environment/variables-cloud.md#viewing-environment-variables) Fastly environment variables.

  ```bash
  magento-cloud variable:get -e <environment-ID>
  ```

- [!DNL Cloud Console]—Controleer de volgende omgevingsvariabelen in het dialoogvenster [Omgevingsconfiguratie](../project/overview.md#configure-environment).

   - `CONFIG__DEFAULT__SYSTEM__FULL_PAGE_CACHE__FASTLY__FASTLY_API_KEY`

   - `CONFIG__DEFAULT__SYSTEM__FULL_PAGE_CACHE__FASTLY__FASTLY_SERVICE_ID`

>[!NOTE]
>
>Als u niet de Fastly geloofsbrieven voor de het Opvoeren of milieu&#39;s van de Productie kunt vinden, contacteer uw Technische Adviseur van de Klant van de Adobe (CTA).

## Snelle caching inschakelen

U hebt de volgende componenten nodig om de Snelle diensten toe te laten en te vormen:

- Laatste versie van de [Snelle CDN voor module Magento 2](fastly.md#fastly-cdn-module-for-magento-2) geïnstalleerd in de Staging- en Productieomgeving. Zie [Snelle upgrade uitvoeren](#upgrade-the-fastly-module).

- [Snelle referenties](#get-fastly-credentials) voor Adobe Commerce over cloudinfrastructuur Staging- en productieomgevingen

**Om snel CDN caching in het Staging en Productie toe te laten**:

{{admin-login-step}}

1. Klikken **Winkels** > Instellingen > **Configuratie** > **Geavanceerd** > **Systeem** en uitbreiden **Volledige paginacache**.

   ![Uitbreiden om snel te selecteren](../../assets/cdn/fastly-menu.png)

1. In de _Caching-toepassing_ de selectie verwijderen uit **Systeemwaarde gebruiken** en selecteer vervolgens **Fastly CDN** in de vervolgkeuzelijst.

   ![Kies snel](../../assets/cdn/fastly-enable-admin.png)

1. Uitbreiden **Snelle configuratie** en [cacheopties kiezen](https://github.com/fastly/fastly-magento2/blob/master/Documentation/CONFIGURATION.md#configure-the-module).

1. Nadat u de cacheopties hebt geconfigureerd, klikt u op **Config opslaan** boven aan de pagina.

1. Wis het geheime voorgeheugen volgens het bericht.

1. Doorgaan met snel configureren door terug te navigeren naar **Winkels** > **Instellingen** > **Configuratie** > **Geavanceerd** > **Systeem** > **Snelle configuratie**.

### Referenties snel testen

1. Navigeer in Beheer naar **Winkels** > Instellingen > **Configuratie** > **Geavanceerd** > **Systeem** > **Snelle configuratie**.

1. Voeg, indien nodig, de **Snelle service-id** en **API-token** waarden voor uw projectomgeving.

   ![Admin. snelle referenties](../../assets/cdn/fastly-credentials-admin-ui.png)

   >[!NOTE]
   >
   >Selecteer niet de koppeling waarmee u het snelheids-API-token wilt maken. Gebruik in plaats daarvan de opdracht [Snelle referenties (service-id en API-token) verstrekt door Adobe](#get-fastly-credentials) verstrekt door Adobe.

1. Klikken **Referenties testen**.

1. Als de test succesvol is, klikt u op **Config opslaan** en wist vervolgens de cache.

   Als de test ontbreekt, verifieer dat de correcte dienst ID en de symbolische waarden van API de geloofsbrieven voor het huidige milieu aanpassen.

   Als de test opnieuw mislukt, verzendt u een Adobe Commerce-ondersteuningsticket of neemt u contact op met uw Adobe-accountvertegenwoordiger. Neem voor Pro-projecten de URL&#39;s op voor uw productie- en staging-sites. Neem voor Starter-projecten de URL&#39;s op voor uw `Master` en Staging-site.

>[!NOTE]
>
>Ga voor instructies voor het wijzigen van snelle API-tokengegevens voor een testomgeving of productieomgeving naar [Snelheidsreferenties wijzigen](fastly.md#change-fastly-api-token).

### VCL snel uploaden naar

Nadat u de module Snelheid hebt ingeschakeld, uploadt u de standaardinstelling [VCL-code](https://github.com/fastly/fastly-magento2/tree/master/etc/vcl_snippets) naar de snelservers. Deze code verstrekt een reeks fragmenten VCL die de configuratiemontages specificeren om caching en andere snel CDN diensten voor uw Adobe Commerce op wolkeninfrastructuur toe te laten.

>[!NOTE]
>
>De services voor het snel in cache plaatsen werken pas wanneer u de eerste upload van de Fastly VCL-code naar de Adobe Commerce Staging and Production-sites hebt voltooid.

**Upload de Fastly VCL**:

1. In de _Snelle configuratie_ sectie, klikken **VCL snel uploaden naar** zoals het volgende cijfer toont.

   ![Upload een Magento-VCL naar Fastly](../../assets/cdn/fastly-upload-vcl-admin.png)

1. Nadat het uploaden is voltooid, vernieuwt u de cache volgens het bericht boven aan de pagina.

## SSL/TLS-certificaten leveren

Adobe biedt een door domein gevalideerd SSL/TLS-certificaat waarmee snel veilig HTTPS-verkeer kan worden aangeboden. Adobe verstrekt één certificaat voor elke ProProductie, het Staging, en het milieu van de Productie van de Aanzet om alle domeinen in dat milieu te beveiligen. Zie voor meer informatie over het geleverde certificaat [Adobe SSL-certificaten (TLS) voor Adobe Commerce op cloudinfrastructuur](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/ssl-tls-certificates-for-magento-commerce-cloud-faq.html).

>[!NOTE]
>
>U kunt uw eigen TLS- of SSL-certificaat opgeven in plaats van het Let&#39;s Encrypt-certificaat te gebruiken dat door de Adobe wordt geleverd. Dit proces vereist echter extra werk om op te zetten en te onderhouden. Als u deze optie wilt kiezen, dient u een Adobe Commerce-ondersteuningsticket in of werkt u met Adobe om aangepaste, gehoste certificaten toe te voegen aan uw Adobe Commerce in omgevingen met cloudinfrastructuur.

Voor het inschakelen van SSL/TLS-certificaten voor Adobe Commerce-omgevingen voert u de volgende stappen uit voor automatisering van de Adobe:

- Valideert domeineigendom
- Bevat een SSL/TLS-certificaat dat specifieke top-level en subdomeinen voor uw winkels dekt.
- Hiermee wordt het certificaat geüpload naar de cloud-omgeving als de site live is

Deze automatisering vereist u om de DNS configuratie voor uw plaats bij te werken om de informatie van de domeinbevestiging te leveren. Gebruiken **één** van de volgende methoden:

- **DNS-validatie**- Voor levende plaatsen, werk uw DNS configuratie met CNAME verslagen bij die aan de Snelle dienst richten
- **CNAME-records ACME-controle**- Werk uw DNS configuratie met de verslagen van de uitdagingCNAME van ACME bij die door Adobe voor elk domein in uw milieu worden verstrekt

>[!TIP]
>
>Als u een Productiedomein hebt dat niet actief is, gebruik de ACME verslagen van uitdagingCNAME voor domeinbevestiging. Door de records vroegtijdig aan uw DNS-configuratie toe te voegen, kunt u het SSL/TLS-certificaat voorzien van de juiste domeinen voordat u de site start. Alvorens aan productie te lanceren, moet u deze placeholder verslagen met de CNAME- verslagen vervangen die door Adobe worden verstrekt.

Wanneer domeinvalidatie is voltooid, bevat de Adobe het TLS/SSL-certificaat Let&#39;s Encrypt en uploadt deze naar live testomgeving of productieomgeving. Dit proces kan tot 12 uur duren. Wij adviseren dat u de DNS configuratieupdates verscheidene dagen vooraf voltooit om vertragingen in plaatsontwikkeling en plaatslancering te verhinderen.

## DNS-configuratie bijwerken met ontwikkelinstellingen

Tijdens het eerste Fastly opstellingsproces, kunt u de volgende URLs gebruiken om Fastly caching in het Opvoeren van het Staging en de milieu&#39;s van de Productie te vormen en te testen:

- Voor Pro Staging en Productie:

   - `mcprod.<your-domain>.com`
   - `mcstaging.<your-domain>.com`

- Uitsluitend voor startproductie:

   - `mcprod.<your-domain>.com`

Deze standaard pre-productie URLs is beschikbaar nadat uw project wordt provisioned. De waarde voor `"your-domain"` Dit is de domeinnaam die u hebt opgegeven tijdens het instapproces.

>[!NOTE]
>
>U kunt geen douanedomein voor een niet productiemilieu op de projecten van de Aanzet specificeren.

Om verkeer van uw opslag URLs aan de Snelle dienst te leiden werkt uw DNS configuratie bij. Wanneer u de configuratie bijwerkt, voorziet de Adobe automatisch van de vereiste SSL/TLS-certificaten en uploadt deze naar uw Cloud-omgevingen. Deze provisioning kan tot 12 uur duren.

>[!NOTE]
>
>Wanneer u bereid bent om uw plaats van de Productie te lanceren, moet u de DNS configuratie opnieuw bijwerken om uw productiedomeinen aan de Snelle dienst te richten en extra configuratietaken te voltooien. Zie [Checklist starten](../launch/checklist.md).

**Vereisten:**

- Schakel de module Snelheid in.
- Upload de standaard VCL-code snel.
- Verstrek een lijst van top-level en subdomeinen voor elk milieu aan Adobe, of verzend een kaartje van de Steun van Adobe Commerce.
- Wacht op bevestiging dat de opgegeven domeinen zijn toegevoegd aan uw Cloud-omgevingen.
- Voor de projecten van de Aanzet, voeg de domeinen aan uw Snelle de dienstconfiguratie toe. Zie [Domeinen beheren](fastly-custom-cache-configuration.md#manage-domains).
- Voor informatie over het bijwerken van de DNS configuratie, controleer met uw [DNS-registrar](https://lookup.icann.org/) voor de correcte methode voor uw domeindienst.

**Om uw DNS configuratie voor ontwikkeling bij te werken**:

1. Punt pre-productie URLs aan de Fastly dienst door CNAME- verslagen toe te voegen: `prod.magentocloud.map.fastly.net`, bijvoorbeeld:

   | Domein of Subdomein | CNAME |
   |---------------------------|----------------------------------|
   | mcprod.your-domain.com | prod.magentocloud.map.fastly.net |
   | mcstaging.your-domain.com | prod.magentocloud.map.fastly.net |

   Wanneer de CNAME-records live zijn, wordt de Adobe voorzien van certificaten en worden de SSL/TLS-certificaten geüpload.

   >[!NOTE]
   >
   >Als u apex-domeinen wilt gebruiken (`your-domain.com`) voor uw plaats van de Productie, moet u DNS adresverslagen (A verslagen) vormen om aan de Snelle serverIP adressen te richten. Zie [DNS-configuratie bijwerken met productie-instellingen](../launch/checklist.md#to-update-dns-configuration-for-site-launch).


1. Voeg de verslagen van de uitdagingCNAME van de ACME voor domeinbevestiging en pre-provisioning van de certificaten van de Productie SSL/TLS toe, bijvoorbeeld:

   | Domein of Subdomein | CNAME |
   |-------------------------------------------|-------------------------------------------|
   | _acme-challenge.your-domain.com | 0123456789abcdef.validation.magento.cloud |
   | _acme-challenge.www.your-domain.com | 9573186429stuvwx.validation.magento.com |
   | _acme-challenge.mystore.your-domain.com | 1234567898zxywvu.validation.magento.cloud |
   | _acme-challenge.subdomain.your-domain.com | 1098765743lmnopq.validation.magento.cloud |

   >[!NOTE]
   >
   >De ACME-aanvraagdossiers in dit voorbeeld zijn plaatsaanduidingen die niet bedoeld zijn om uw Adobe Commerce-opbouw- en productiesites te voorzien. Krijg de correcte ACME informatie van het uitdagingsverslag voor uw project door Adobe te contacteren.

   Nadat de CNAME-records zijn toegevoegd, valideert Adobe de domeinen en voorzieningen van het SSL/TLS-certificaat voor de omgeving. Wanneer u de DNS configuratie aan routeverkeer van deze domeinen aan de Snelle dienst bijwerkt, uploadt de Adobe het certificaat aan het milieu.

1. Werk de Adobe Commerce Base-URL bij.

   - Gebruik SSH om u aan te melden bij de productieomgeving.

     ```bash
     magento-cloud ssh
     ```

   - Met de Cloud CLI kunt u de basis-URL voor uw winkel wijzigen.

     ```bash
     php bin/magento setup:store-config:set --base-url="https://mcstaging.your-domain.com/"
     ```

   >[!NOTE]
   >
   >Als alternatief voor het gebruik van de Cloud CLI kunt u de Basis-URL bijwerken via het dialoogvenster [Beheerder](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-urls.html)

1. Start de webbrowser opnieuw.

1. Test uw website.

## Snelle caching testen

Nadat u de DNS configuratieveranderingen voltooit, gebruik [cURL](https://curl.se/) opdrachtregelprogramma om te controleren of de cache snel werkt.

**De antwoordheaders controleren**:

1. Gebruik in een terminal het volgende `curl` opdracht om de URL van uw livesite te testen:

   ```bash
   curl -vo /dev/null -H Fastly-Debug:1 https://<live-URL>
   ```

   Als u geen statische route hebt geplaatst of de DNS configuratie voor de domeinen op uw levende plaats voltooid, gebruik `--resolve` markering, die DNS naamresolutie overslaat.

   ```bash
   curl -vo /dev/null -H Fastly-Debug:1 --resolve <live-URL-hostname>:443:<live-IP-address>
   ```

1. Controleer in de reactie de [koppen](fastly-troubleshooting.md#check-cache-hit-and-miss-response-headers) om ervoor te zorgen dat Fastly werkt. De volgende unieke kopteksten worden weergegeven in het antwoord:

   ```http
   < Fastly-Magento-VCL-Uploaded: yes
   < X-Cache: HIT, MISS
   ```

Als de kopballen niet de correcte waarden hebben, zie [Fouten in de reactiekoppen oplossen](fastly-troubleshooting.md#curl) voor hulp bij probleemoplossing.

## De module Snelheid upgraden

Werk snel CDN voor Magento 2 module bij om kwesties op te lossen, prestaties te verbeteren, en nieuwe eigenschappen te verstrekken.
We raden u aan de module Snelheid in uw testomgeving en productieomgeving bij te werken naar de [nieuwste versie](https://github.com/fastly/fastly-magento2/blob/master/VERSION).

Nadat u de module bijwerkt, moet u de code uploaden VCL om de veranderingen op de Fastly de dienstconfiguratie toe te passen.

>[!WARNING]
>
> Als u de standaard snelle VCL-code hebt aangepast met een aangepaste versie, overschrijft de upgrade van de module Snelheid uw wijzigingen. Als u aangepaste VCL-fragmenten met unieke namen hebt toegevoegd, blijven deze wijzigingen behouden tijdens het upgradeproces. Als beste praktijken, bevorder de het Opvoeren milieu en bevestig de veranderingen alvorens veranderingen in het milieu van de Productie toe te passen.

**Om de versie van Fastly CDN module voor Magento 2 te controleren**:

1. Ga naar de hoofdmap van de cloud-omgeving.

1. Gebruik Composer om de geïnstalleerde versie te controleren.

   ```bash
   composer show *fastly*
   ```

1. Als de [nieuwste release](https://github.com/fastly/fastly-magento2/releases) niet is geïnstalleerd, voert u de stappen uit om de module Snelheid te upgraden.

**De module Snelheid upgraden**:

1. In uw lokale integratiemilieu, gebruik de volgende moduleinformatie aan [upgrade uitvoeren van de module Snelheid](../store/extensions.md#upgrade-an-extension).

   ```text
   module name: fastly/magento2
   repository: https://github.com/fastly/fastly-magento2.git
   ```

1. Verhoog uw updates naar de testomgeving.

1. Meld u aan bij de beheerder voor de testomgeving [uploadt de VCL-code](#upload-vcl-to-fastly).

1. [Services voor snel controleren](fastly-troubleshooting.md#verify-or-debug-fastly-services) op de Staging-site van Adobe Commerce.

Nadat u de Snelle diensten op de Staging plaats verifieert, herhaal het verbeteringsproces in het milieu van de Productie.

>[!TIP]
>
> Als u problemen hebt met services die snel kunnen worden uitgevoerd in uw Adobe Commerce-omgeving, raadpleegt u de [Adobe Commerce-probleemoplosser](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/magento-fastly-troubleshooter.html).
