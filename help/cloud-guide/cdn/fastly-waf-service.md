---
title: Web Application Firewall (WAF)
description: Leer hoe de Fastly WAF dienst ontdekt, registreert, en kwaadwillig verzoekverkeer blokkeert alvorens het het netwerk of de plaatsen van Adobe Commerce kan beschadigen.
feature: Cloud, Configuration, Security
exl-id: 40bfe983-7f32-4155-ae77-7cd18866f6e2
source-git-commit: 6b01bf91c3bf63ba268d0f8e10e19db4cb355997
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---

# Web Application Firewall (WAF)

De WAF-service (Web Application Firewall) voor Adobe Commerce op cloudinfrastructuur is snel en detecteert, registreert en blokkeert kwaadaardig aanvraagverkeer voordat uw sites of netwerk beschadigd kunnen raken. De WAF-service is alleen beschikbaar in productieomgevingen.

De WAF-service biedt de volgende voordelen:

- **naleving PCI** - WAF enablement zorgt ervoor dat Adobe Commerce storefronts in de milieu&#39;s van de Productie aan PCI DSS 6.6 veiligheidsvereisten voldoen.
- **StandaardWAF beleid** - het standaardbeleid van WAF, dat door Fastly wordt gevormd en wordt gehandhaafd, verstrekt een inzameling van veiligheidsregels die worden gemaakt om uw het Webtoepassingen van Adobe Commerce tegen een brede waaier van aanvallen, met inbegrip van injectieaanvallen, kwaadwillige input, dwars-plaats scripting, gegevensextractie, het protocolschendingen van HTTP, en andere [ Tien ](https://owasp.org/www-project-top-ten/) veiligheidsbedreigingen te beschermen.
- **WAF op het instappen en enablement** - de Adobe stelt en laat het standaardbeleid van WAF in uw milieu van de Productie binnen 2 tot 3 weken toe nadat de levering definitief is.
- **Verrichtingen en onderhoudssteun**—
   - Adobe en snel opstelling en beheer uw logboeken en alarm voor de dienst van WAF.
   - De Adobe brengt klantensteunkaartjes met betrekking tot de dienstkwesties van WAF in werking die wettig verkeer als Prioriteit 1 kwesties blokkeren.
   - De geautomatiseerde verbeteringen aan de de dienstversie van WAF verzekeren directe dekking voor nieuwe of evoluerende exploitaties. Zie [ onderhoud en verbeteringen van WAF ](#waf-maintenance-and-updates).

>[!TIP]
>
>Voor extra informatie over het handhaven van naleving PCI voor uw Adobe Commerce op de opslag van de wolkeninfrastructuur, zie [ naleving PCI ](https://business.adobe.com/products/magento/pci-compliance.html).

## WAF inschakelen

De Adobe laat de dienst van WAF op nieuwe rekeningen binnen 2 tot 3 weken toe nadat de levering definitief is. WAF wordt uitgevoerd door de Fastly CDN dienst. U hoeft geen hardware of software te installeren of te onderhouden.

>[!NOTE]
>
>Voordat u de WAF-service kunt gebruiken, moet u alle externe verkeer naar uw Adobe Commerce op het infrastructuurproject voor de cloud doorlopen via de Fastly-service. Zie [ Opstelling snel ](fastly-configuration.md).

## Hoe werkt het

De dienst van WAF integreert met Fastly en gebruikt de geheim voorgeheugenlogica binnen de Fastly dienst CDN om verkeer bij de Fastly globale knopen te filtreren. Wij laten de dienst van WAF in uw milieu van de Productie met een standaardbeleid van WAF toe dat op [ wordt gebaseerd ModSecurity Regels van Trustwave SpiderLabs ](https://github.com/owasp-modsecurity/ModSecurity) en de Hoogste Tien veiligheidsbedreigingen van OWASP.

De dienst van WAF filtert HTTP en HTTPS verkeer (GET en POST verzoeken) tegen de heersers van WAF en blokkeert verkeer dat kwaadwillig is of niet aan specifieke regels voldoet. De de dienstfilters slechts oorsprong-gebonden verkeer dat probeert om het geheime voorgeheugen te verfrissen. Dientengevolge, houden wij het meeste aanvalsverkeer bij het Fastly geheime voorgeheugen tegen, beschermend uw oorsprongsverkeer tegen kwaadwillige aanvallen. Door slechts oorsprongverkeer te verwerken, behoudt de dienst van WAF geheim voorgeheugenprestaties, introducerend slechts een geschatte 1.5 milliseconden aan 20 milliseconden van latentie aan elk niet in het voorgeheugen ondergebracht verzoek.

## Problemen met geblokkeerde aanvragen oplossen

Wanneer de dienst van WAF wordt toegelaten, filters het al Web en admin verkeer tegen de regels van WAF en blokkeert om het even welke Webverzoek die een regel teweegbrengt. Wanneer een aanvraag wordt geblokkeerd, ziet de aanvrager een standaard `403 Forbidden` foutpagina die een referentie-id bevat voor de blokkeringsgebeurtenis.

![ WAF foutenpagina ](../../assets/cdn/fastly-waf-403-error.png)

U kunt deze pagina met foutreacties aanpassen via de beheerfunctie. Zie [ de de reactiepagina van WAF ](fastly-custom-response.md#customize-the-waf-error-page) aanpassen.

Als uw Adobe Commerce admin pagina of storefront een `403 Forbidden` foutenpagina in antwoord op een wettig verzoek URL terugkeert, leg een [ kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) voor. Kopieer de referentie-id van de pagina met foutreacties en plak deze in de beschrijving van het ticket.

## WAF-onderhoud en -updates

De WAF-regels worden snel bijgehouden en bijgewerkt op basis van regelupdates van commerciële derden, Fastly Research en open bronnen. De gepubliceerde regels worden zo nodig snel bijgewerkt in een beleid of wanneer wijzigingen in de regels beschikbaar zijn uit de respectieve bronnen. Ook, kan de Fastly regels toevoegen die de gepubliceerde klassen van regels in de instantie van WAF van om het even welke dienst aanpassen nadat de dienst van WAF wordt toegelaten. Deze updates zorgen voor onmiddellijke dekking voor nieuwe of zich ontwikkelende exploitaties.

Adobe en beheer snel het updateproces om ervoor te zorgen dat de nieuwe of gewijzigde regels van WAF effectief in uw milieu van de Productie werken alvorens de updates op het blokkeren wijze worden opgesteld.

## Beperkingen

De standaard WAF-service van Fastly biedt geen ondersteuning voor de volgende functies:

- De bescherming tegen malware of beide beperking-overweegt het gebruiken van [ toegangsbeheerlijsten ](./fastly-vcl-allowlist.md) of de derdienst.
- Het tarief beperkt-zie [ Tarief dat ](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/RATE-LIMITING.md) in de Snelle documentatie beperkt, of zie [ het Tarief dat ](https://developer.adobe.com/commerce/webapi/get-started/rate-limiting/) beperkt in _het Web API van Commerce_ veiligheidssectie beperkt.
- Het vormen van een registrereneindpunt voor klant-zie [ dienst PrivateLink ](../development/privatelink-service.md) als alternatief.

Hoewel de dienst van WAF u niet toestaat om verkeer te blokkeren of toe te staan dat op IP adressen wordt gebaseerd, kunt u toegangsbeheerlijsten (ACL) en de fragmenten van douaneVCL aan uw Snelle dienst toevoegen om de IP adressen en logica VCL voor het blokkeren of het toestaan van verkeer te specificeren. Zie {de fragmenten van 0} Snelle VCL van de Douane {](fastly-vcl-custom-snippets.md).[

Het filtreren voor TCP, UDP, of verzoeken ICMP wordt niet gesteund door de dienst van WAF. Nochtans, wordt deze functionaliteit verstrekt door de ingebouwde bescherming DDoS inbegrepen met de Fastly dienst CDN. Zie [ bescherming DDoS ](fastly.md#ddos-protection).
