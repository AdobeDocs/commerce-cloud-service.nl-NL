---
title: Aangepaste VCL voor het blokkeren van aanvragen
description: Blok inkomende verzoeken door IP adres gebruikend een lijst van het Toegangsbeheer van de Rand (ACL) met een fragment van douaneVCL.
feature: Cloud, Configuration, Security
exl-id: 1f637612-3858-49d0-91f7-9b8823933cc9
source-git-commit: 0e9ace747cc56808108781e42b97c86756089818
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 0%

---

# Aangepaste VCL voor het blokkeren van aanvragen

U kunt de Fastly CDN module voor Magento 2 gebruiken om Rand ACL met een lijst van IP adressen tot stand te brengen die u wilt blokkeren. Vervolgens kunt u die lijst gebruiken met een VCL-fragment om binnenkomende aanvragen te blokkeren. De code controleert het IP adres van het inkomende verzoek. Als het een IP adres aanpast inbegrepen in de ACL lijst, blokkeert snel het verzoek om tot uw plaats toegang te hebben en keert a terug `403 Forbidden error`. Alle andere client-IP-adressen hebben toegang.

**Vereisten:**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- Lijst met client-IP-adressen die moeten worden geblokkeerd

## Creeer Rand ACL voor het blokkeren van cliëntIP adressen

U creeert Rand ACL om de lijst van IP te bepalen adressen aan blok. Na het creëren van ACL, kunt u het in een fragment van douaneVCL gebruiken om toegang tot uw het Opvoeren of plaats van de Productie te beheren.

Beheer toegang voor zowel het Opvoeren als de plaatsen van de Productie door Edge ACL met de zelfde naam in beide milieu&#39;s te creëren. De VCL-fragmentcode is van toepassing op beide omgevingen.

1. Meld u aan bij de beheerder.
1. Navigeren naar **Winkels** > Instellingen > **Configuratie** > **Geavanceerd** > **Systeem** > **Volledige paginacache** > **Snelle configuratie**.
1. Breid uit **Edge ACL** sectie.
1. Klikken **ACL toevoegen** om een lijst te maken. In dit voorbeeld geeft u de lijst &quot;lijst van gewezen personen&quot; een naam.
1. Voer IP-adreswaarden in de lijst in. Alle client-IP-adressen die aan deze lijst worden toegevoegd, worden geblokkeerd en hebben geen toegang tot de site.
1. Selecteer desgewenst de optie **Negatief** selectievakje indien nodig.

U verwijst naar Rand ACL door naam in uw VCL fragmentcode.

## De aangepaste VCL voor de lijst van gewezen personen maken

>[!NOTE]
>
>In dit voorbeeld ziet u hoe u geavanceerde gebruikers een VCL-codefragment kunt maken om aangepaste blokkeringsregels te configureren voor het uploaden naar de Fastly-service. U kunt een lijst van gewezen personen of een lijst van gewenste personen vormen die op land van Adobe Commerce Admin wordt gebaseerd gebruikend [Blokkeren](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) functie beschikbaar in de snelste CDN voor de module Magento 2.

Nadat u Edge ACL bepaalt, kunt u het gebruiken om het fragment tot stand te brengen VCL om toegang tot de IP adressen te blokkeren die in ACL worden gespecificeerd. U kunt hetzelfde VCL-fragment gebruiken in zowel de testomgeving als de productieomgeving, maar u moet het fragment afzonderlijk uploaden naar elke omgeving.

De volgende het fragmentcode van douaneVCL (formaat JSON) toont de logica om inkomende verzoeken met een cliëntIP adres te blokkeren dat een adres in lijst van gewezen personen ACL aanpast.

```json
{
  "name": "blocklist",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( client.ip ~ blocklist) { error 403 \"Forbidden\"; }"
}
```

Voordat u een op dit voorbeeld gebaseerd fragment maakt, controleert u de waarden om te bepalen of u wijzigingen wilt aanbrengen:

- `name`: Naam voor het VCL-fragment. In dit voorbeeld hebben we de naam gebruikt `blocklist`.

- `priority`: Hiermee bepaalt u wanneer het VCL-fragment wordt uitgevoerd. De prioriteit is `5` om onmiddellijk in werking te stellen en te controleren of een Admin- verzoek uit een toegestaan IP adres komt. Het fragment wordt uitgevoerd vóór de standaard VCL-fragmenten voor Magento&#39;s (`magentomodule_*`) een prioriteit van 50. Stel de prioriteit voor elk aangepast fragment in op een waarde hoger of lager dan 50, afhankelijk van het tijdstip waarop het fragment moet worden uitgevoerd. Fragmenten met een lagere prioriteit worden eerst uitgevoerd.

- `type`: Geeft het type VCL-fragment op dat de locatie van het fragment in de gegenereerde VCL-code bepaalt. In dit voorbeeld gebruiken we `recv`, die de VCL-code in het dialoogvenster `vcl_recv` subroutine, onder de vaste plaat VCL en boven alle objecten. Zie de [VCL-fragmentverwijzing snel](https://docs.fastly.com/api/config#api-section-snippet) voor de lijst met fragmenttypen.

- `content`: Het fragment van VCL-code dat moet worden uitgevoerd, dat het IP-adres van de client controleert. Als IP in Rand ACL is, wordt het geblokkeerd van toegang met a `403 Forbidden` fout voor de gehele website. Alle andere client-IP-adressen hebben toegang.

Na het herzien van en het bijwerken van de code voor uw milieu, gebruik één van beiden van de volgende methodes om het fragment van douaneVCL aan uw Fastly de dienstconfiguratie toe te voegen:

- [Het aangepaste VCL-fragment toevoegen vanuit Beheer](#add-the-custom-vcl-snippet). Deze methode wordt aanbevolen als u toegang kunt krijgen tot de beheerder. (Vereist [Snelle versie 1.2.58](fastly-configuration.md#upgrade-fastly-module) of hoger.)

- Sla het JSON-codevoorbeeld op in een bestand (bijvoorbeeld `blocklist.json`) en [uploaden met de snelheids-API](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). Gebruik deze methode als u geen toegang hebt tot de beheerder.

## Het aangepaste VCL-fragment toevoegen

{{admin-login-step}}

1. Klikken **Winkels** > Instellingen > **Configuratie** > **Geavanceerd** > **Systeem**.

1. Uitbreiden **Volledige paginacache** > **Snelle configuratie** > **Aangepaste VCL-fragmenten**.

1. Klikken **Aangepast fragment maken**.

1. Voeg de waarden van het VCL-fragment toe:

   - **Naam** — `blocklist`

   - **Type** — `recv`

   - **Prioriteit** — `5`

   - Voeg de **VCL** inhoud van fragment:

     ```conf
     if ( client.ip ~ blocklist) { error 403 "Forbidden"; }
     ```

1. Klikken **Maken** om het VCL-fragmentbestand met het naampatroon te genereren `type_priority_name.vcl`bijvoorbeeld `recv_5_blocklist.vcl`

1. Klik op **VCL snel uploaden naar** in de *Snelle configuratie* om het bestand toe te voegen aan de configuratie van de Fastly-service.

1. Na uploads, vernieuw het geheime voorgeheugen volgens het bericht bij de bovenkant van de pagina.

Hiermee wordt de bijgewerkte versie van de VCL-code snel gevalideerd tijdens het uploadproces. Als de validatie mislukt, bewerkt u het aangepaste VCL-fragment om het probleem op te lossen. Vervolgens uploadt u de VCL opnieuw.

## Aanvullende VCL-voorbeelden voor het blokkeren van aanvragen

De volgende voorbeelden tonen hoe te om verzoeken te blokkeren gebruikend gealigneerde voorwaardenverklaringen in plaats van een ACL lijst.

>[!WARNING]
>
>In deze voorbeelden is de VCL-code opgemaakt als een JSON-payload die naar een bestand kan worden opgeslagen en in een Fastly API-aanvraag kan worden verzonden. U kunt de [VCL-fragment van Admin](#add-the-custom-vcl-snippet)of als een JSON-tekenreeks met de snelheids-API. Als u validatie wilt voorkomen wanneer u de snelheids-API gebruikt met een JSON-tekenreeks, moet u een backslash gebruiken om speciale tekens te verwijderen.

Zie [Dynamische VCL-fragmenten gebruiken](https://docs.fastly.com/vcl/vcl-snippets/) in de Fastly VCL documentatie.

### VCL-codevoorbeeld: blokcode per land

In dit voorbeeld wordt de ISO 3166-1-landcode van twee tekens gebruikt voor het land dat aan het IP-adres is gekoppeld.

```json
{
  "name": "blockbycountrycode",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( client.geo.country_code == \"HK\" ) { error 405 \"Not allowed\";}"
}
```

>[!NOTE]
>
>In plaats van een aangepast VCL-fragment kunt u het fragment Snelst gebruiken [Blokkeren](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) in de Adobe Commerce op cloudinfrastructuur Admin om blokkering te configureren op basis van landcode of een lijst met landcodes.

### Voorbeeld van VCL-code: Blok door aanvraagheader van HTTP-gebruikersagent

```json
{
  "name": "blockbyuseragent",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( req.http.User-Agent ~ \"(UCBrowser|MQQBrowser|LieBaoFast|Mb2345Browser)\" ) {error 405 \"Not allowed\";}"
}
```

{{automate-vcl-snippet-deployment}}

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
