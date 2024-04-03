---
title: Aan de slag met aangepaste VCL-fragmenten
description: Leer over het gebruiken van de codefragmenten van de Taal van de Controle van de Varnish om de Fastly de dienstconfiguratie voor Adobe Commerce aan te passen.
feature: Cloud, Configuration, Services
exl-id: df0f0906-8ffa-41a1-a31c-d36deb5a6a31
source-git-commit: 89c57a486545d6165e0407f913f4fa4cf6c95abe
workflow-type: tm+mt
source-wordcount: '1947'
ht-degree: 0%

---

# Aan de slag met aangepaste VCL

Steunt snel een aangepaste versie van de Taal van de Configuratie van de Varnish (VCL) om de Snelle de dienstconfiguratie aan uw vereisten aan te passen.

Aangepaste VCL-fragmenten zijn blokken VCL-logica die zijn toegevoegd aan de actieve VCL-versie die is geüpload naar uw Adobe Commerce-site. Een aangepast VCL-fragment wijzigt hoe services die snel in cache worden geplaatst, reageren op aanvraagverkeer. U kunt bijvoorbeeld een aangepast VCL-fragment toevoegen om alleen aanvraagverkeer vanaf opgegeven IP-adressen van de client toe te staan. U kunt ook een fragment maken om het verkeer te blokkeren van websites die bekend staan om het verzenden van spam naar uw Adobe Commerce-sites.

Aangepaste VCL-fragmenten - gegenereerd, gecompileerd en verzonden naar alle caches met een snelheid - laden en activeren zonder serverdowntime.

>[!NOTE]
>
>Alvorens douanecode VCL, randwoordenboeken, en ACLs aan uw Fastly moduleconfiguratie toe te voegen, verifieer dat de Fastly caching dienst met de standaardconfiguratie werkt. Zie [Services voor snel configureren](fastly-configuration.md).

Snelle ondersteuning voor twee typen aangepaste VCL-fragmenten:

- [Gewone fragmenten](https://docs.fastly.com/en/guides/about-vcl-snippets)—Aangepaste gewone VCL-fragmenten worden gecodeerd voor specifieke VCL-versies. U kunt gewone VCL-fragmenten maken, wijzigen en implementeren via de API voor beheerders of snelkoppelingen.

- [Dynamische fragmenten](https://docs.fastly.com/en/guides/using-dynamic-vcl-snippets)—VCL-fragmenten die zijn gemaakt met de snelheids-API. U kunt dynamische fragmenten wijzigen en opstellen zonder het moeten de Fastly versie VCL voor uw dienst bijwerken.

Wij adviseren gebruikend de fragmenten van douaneVCL met de Woordenboeken van de Rand en de Lijsten van het Toegangsbeheer (ACL) om gegevens op te slaan die in uw douanecode worden gebruikt.

- [**Edge-woordenboek**](https://docs.fastly.com/guides/edge-dictionaries/about-edge-dictionaries)—Hiermee worden gegevens opgeslagen als sleutel-waardeparen in een woordenboekcontainer waarnaar kan worden verwezen vanuit aangepaste VCL-fragmenten

- [**Edge ACL**](https://docs.fastly.com/guides/access-control-lists/about-acls)—Slaat de cliëntIP adresgegevens op die de toegangsbeheerlijst voor blok bepalen of regels toestaan die gebruikend de fragmenten van douaneVCL worden uitgevoerd

Het woordenboek en ACL gegevens worden opgesteld aan de Snelle knopen van de Rand die over netwerkgebieden toegankelijk zijn. Ook, kunnen de gegevens dynamisch over het netwerk worden bijgewerkt zonder u te vereisen om de code VCL voor uw het opvoeren of productiemilieu opnieuw op te stellen.

>[!NOTE]
>
>U kunt aangepaste VCL-fragmenten alleen toevoegen aan een testomgeving of productieomgeving als u [geconfigureerde snelservices](fastly-configuration.md) voor die omgeving.

## Zelfstudie

Deze zelfstudie en voorbeelden demonstreren het gebruik van gewone aangepaste VCL-fragmenten met Edge Dictionaries en Edge ACLs om de Fastly-serviceconfiguratie voor Adobe Commerce aan te passen. Raadpleeg de documentatie bij Snelheid voor meer informatie:

- [Gids voor VCL van de Vloot](https://docs.fastly.com/guides/vcl/guide-to-vcl)—Informatie over de Fastly Varnish implementatie, de Snelle uitbreidingen VCL, en middelen voor het leren meer over Varnish en VCL.
- [Fastly VCL reference](https://docs.fastly.com/guides/vcl/)—Gedetailleerde programmeringsverwijzing om snel douaneVCL en de fragmenten van douaneVCL te ontwikkelen en problemen op te lossen.

U kunt aangepaste VCL-fragmenten maken en beheren via Adobe Commerce Admin of met de snelheids-API:

- [Adobe Commerce Admin](#manage-custom-vcl-from-admin)—We raden u aan de Adobe Commerce Admin te gebruiken voor het beheer van aangepaste VCL-fragmenten, omdat hiermee het proces voor het valideren, uploaden en toepassen van de VCL-wijzigingen in de configuratie van de Fastly-service wordt geautomatiseerd. Bovendien kunt u de aangepaste VCL-fragmenten die aan de Fastly-serviceconfiguratie zijn toegevoegd, weergeven en bewerken via de beheerfunctie.

- [Snelle API](#manage-vcl-using-the-api)—Als u geen toegang hebt tot Admin, gebruikt u de snelheids-API om aangepaste VCL-fragmenten te beheren. Gebruik bijvoorbeeld de API om de Fastly-serviceconfiguratie problemen op te lossen wanneer de site uitvalt, of om een aangepast VCL-fragment toe te voegen. Bovendien kunnen sommige bewerkingen alleen met de API worden voltooid. U moet de API bijvoorbeeld gebruiken om een oudere VCL-versie te reactiveren of om alle VCL-fragmenten in een opgegeven VCL-versie weer te geven. Zie [Snelle API-referentie voor VCL-fragmenten](#api-quick-reference-for-vcl-snippets).

### Voorbeeld-VCL-fragmentcode

In het volgende voorbeeld wordt het aangepaste VCL-fragment (JSON-indeling) getoond dat verkeer filtert op IP-adres van client:

```json
{
  "service_id": "FASTLY_SERVICE_ID",
  "version": "{Editable Version #}",
  "name": "apply_acl",
  "priority": "100",
  "dynamic": "1",
  "type": "hit",
  "content": "if ((client.ip ~ {ACLNAME}) && !req.http.Fastly-FF){ error 403; }"
}
```

>[!WARNING]
>
>In dit voorbeeld is de VCL-code geformatteerd als een JSON-payload die naar een bestand kan worden opgeslagen en in een Fastly API-aanvraag kan worden verzonden. Als u JSON-validatiefouten wilt voorkomen bij het verzenden van het fragment als JSON voor een API-aanvraag, gebruikt u een backslash om speciale tekens in de code te verwijderen. Zie [Dynamische VCL-fragmenten gebruiken](https://docs.fastly.com/vcl/vcl-snippets/) in de Fastly VCL documentatie. Als u het VCL-fragment vanuit Beheer verzendt, hoeft u geen speciale tekens te verwijderen.

De VCL-logica in de `content` in het veld worden de volgende handelingen uitgevoerd:

- Controleert het inkomende IP adres, `client.ip` op elk verzoek

- Hiermee blokkeert u een aanvraag met een IP-adres dat is opgenomen in het dialoogvenster *ACLNAME* edge ACL, die een `403 Forbidden` fout

De volgende lijst verstrekt details over zeer belangrijke gegevens voor de fragmenten van douaneVCL. Zie voor een meer gedetailleerde referentie de [VCL-fragmenten](https://docs.fastly.com/api/config#api-section-snippet) in de Fastly documentatie.

| Waarde | Beschrijving |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `API_KEY` | De API-sleutel voor toegang tot uw snelaccount. Zie [Referenties ophalen](fastly-configuration.md). |
| `active` | Actieve status van een fragment of versie. Retourneert `true` of `false`. Indien waar (true), wordt het fragment of de versie gebruikt. Een actief fragment klonen met het versienummer ervan. |
| `content` | Het fragment van VCL-code dat moet worden uitgevoerd. Snelheid biedt geen ondersteuning voor alle VCL-taalfuncties. Bovendien beschikt Fastly over aangepaste functionaliteit voor extensies. Raadpleeg voor meer informatie over ondersteunde functies de [Snelle VCL-programmeringsreferentie](https://docs.fastly.com/vcl/reference/). |
| `dynamic` | Dynamische status van een fragment. Retourneert `false` for [reguliere fragmenten](https://docs.fastly.com/en/guides/about-vcl-snippets) opgenomen in de versioned VCL voor de Fastly de dienstconfiguratie. Retourneert `true` voor een [dynamisch fragment](https://docs.fastly.com/vcl/vcl-snippets/using-dynamic-vcl-snippets/) die kunnen worden gewijzigd en geïmplementeerd zonder dat een nieuwe VCL-versie nodig is. |
| `number` | VCL-versienummer waar het fragment wordt opgenomen. Snelle toepassingen *Bewerkbaar versienummer* in hun voorbeeldwaarden. Als u aangepaste fragmenten uit de API toevoegt, neemt u het versienummer op in de API-aanvraag. Als u aangepaste VCL toevoegt via de beheerfunctie, is de versie beschikbaar voor u. |
| `priority` | Numerieke waarde van `1` tot `100` die aangeeft wanneer de aangepaste VCL-fragmentcode wordt uitgevoerd. Fragmenten met lagere prioriteitswaarden worden eerst uitgevoerd. Indien niet opgegeven, wordt `priority` standaardwaarde `100`.<p>Elk aangepast VCL-fragment met een prioritaire waarde van `5` De looppas onmiddellijk, die voor code VCL het best is die verzoek het verpletteren (blok en lijsten van gewenste personen en richt opnieuw) uitvoert. Prioriteit `100` is het meest geschikt voor het overschrijven van standaard VCL-fragmentcode.<p>Alles [standaard VCL-fragmenten](fastly-configuration.md#upload-vcl-snippets) opgenomen in de module Magento-Fastly `priority=50`.<ul><li>Een hoge prioriteit toewijzen als `100` om aangepaste VCL-code uit te voeren na alle andere VCL-functies en de standaard VCL-code te overschrijven.</li></ul> |
| `service_id` | De snelste service-id voor een specifieke omgeving voor Staging of Productie. Deze id wordt toegewezen wanneer uw project wordt toegevoegd aan de Adobe Commerce op de cloud-infrastructuur [Snelle serviceaccount](fastly.md#fastly-service-account-and-credentials). |
| `type` | Hiermee geeft u de locatie op voor het invoegen van het gegenereerde fragment, zoals `init` (boven subroutines) en `recv` (binnen subroutines). Zie de snelkoppeling voor meer informatie [VCL-fragmenten](https://docs.fastly.com/api/config#api-section-snippet) referentie. |

## Aangepaste VCL beheren vanuit beheerder

U kunt [aangepaste VCL-fragmenten toevoegen](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/CUSTOM-VCL-SNIPPETS.md) van de *Snelle configuratie* > *Aangepaste VCL-fragmenten* in de Admin.

![Aangepaste VCL-fragmenten beheren](../../assets/cdn/fastly-edit-snippets.png)

De *Aangepaste VCL-fragmenten* in de weergave worden alleen fragmenten weergegeven die via Beheer zijn toegevoegd. Als u fragmenten toevoegt met de snelheids-API, gebruikt u de API voor [beheren](#manage-vcl-using-the-api).

In de volgende voorbeelden ziet u hoe u aangepaste VCL-fragmenten maakt en beheert vanuit de beheerfunctie en hoe u snel Edge-modules en Edge-woordenboeken kunt gebruiken:

- [Reroute-aanvragen naar een CMS-backend](fastly-vcl-wordpress.md)
- [Blokverwijzingsspam](fastly-vcl-badreferer.md)
- [Blokverwijzingsspam](fastly-vcl-badreferer.md)
- [Aangepaste VCL voor IP-lijst van gewenste personen](fastly-vcl-allowlist.md)
- [Aangepaste VCL voor IP-lijst van gewezen personen](fastly-vcl-blocking.md)
- [Snelcache omzeilen](fastly-vcl-bypass-to-origin.md)

## VCL beheren met de API

De volgende analyse toont u hoe te om regelmatige VCL fragmentdossiers tot stand te brengen en hen toe te voegen aan uw Snelle de dienstconfiguratie gebruikend Snelle API. U kunt de fragmenten maken en beheren vanuit de *terminal* toepassing. U hebt geen SSH-verbinding in een specifieke omgeving nodig.

**Vereisten:**

- Configureer uw Adobe Commerce op de cloud-infrastructuur voor snelle services. Zie [Snel instellen](fastly-configuration.md).

- [Snelle API-referenties ophalen](fastly-configuration.md) aanvragen voor verificatie van de Fastly-API. Zorg ervoor dat u de geloofsbrieven voor het correcte milieu krijgt: het Opvoeren of de Productie.

- Sla snel de dienstgeloofsbrieven van de sparen als basisomgevingsvariabelen die u in cURL bevelen kunt gebruiken:

  ```bash
  export FASTLY_SERVICE_ID=<Service-ID>
  ```

  ```bash
  export FASTLY_API_TOKEN=<API-Token>
  ```

  De geëxporteerde omgevingsvariabelen zijn alleen beschikbaar in de huidige basissessie en gaan verloren wanneer u de terminal sluit. U kunt variabelen opnieuw definiëren door een nieuwe waarde te exporteren. U kunt als volgt de lijst met geëxporteerde variabelen weergeven die betrekking hebben op Snelheid:

  ```bash
  export | grep FASTLY
  ```

## VCL-fragmenten toevoegen

Deze zelfstudie bevat de basisstappen voor het toevoegen van aangepaste fragmenten met de snelheids-API.

>[!NOTE]
>
>Ga voor meer informatie over het beheren van aangepaste VCL-fragmenten in Adobe Commerce Admin naar [VCL beheren vanuit de Adobe Commerce-beheerder](#manage-custom-vcl-from-admin).


**Vereisten**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

### Stap 1: Zoek de actieve VCL-versie

De snelheids-API gebruiken [get version](https://docs.fastly.com/api/config#version_dfde9093f4eb0aa2497bbfd1d9415987) bewerking om het actieve VCL-versienummer op te halen:

```bash
curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/active
```

In de JSON-reactie noteert u het actieve VCL-versienummer dat in de `number` toets, bijvoorbeeld `"number": 99`. U hebt het versienummer nodig wanneer u de VCL kloont om te bewerken.

```json
{
  "testing": false,
  "locked": true,
  "number": 99,
  "active": true,
  "service_id": "872zhjyxhto5SIRb3GAE0",
  "staging": false,
  "created_at": "2019-01-29T22:38:53Z",
  "deleted_at": null,
  "comment": "Magento Module uploaded VCL",
  "updated_at": "2019-01-29T22:39:06Z",
  "deployed": false
}
```

Sla het actieve versienummer op in een basisomgevingsvariabele voor gebruik in volgende API-aanvragen:

```bash
export FASTLY_VERSION_ACTIVE=<Version>
```

### Stap 2: De actieve VCL-versie en alle fragmenten klonen

Voordat u aangepaste VCL-fragmenten kunt toevoegen of wijzigen, moet u een kopie van de actieve VCL-versie maken voor bewerking. De snelheids-API gebruiken [klonen](https://docs.fastly.com/api/config#version_7f4937d0663a27fbb765820d4c76c709) bewerking:

```bash
curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION_ACTIVE/clone -X PUT
```

In de JSON-reactie wordt het versienummer verhoogd en wordt het *actief* sleutelwaarde is `false`. U kunt de nieuwe, inactieve versie van VCL plaatselijk wijzigen.

```json
{
  "testing": false,
  "locked": false,
  "number": 100,
  "active": false,
  "service_id": "vW2bLFWhhto5SIRb3GAE0",
  "staging": false,
  "created_at": "2019-01-29T22:38:53Z",
  "deleted_at": null,
  "comment": "Magento Module uploaded VCL",
  "updated_at": "2019-01-29T22:39:06Z",
  "deployed": false
}
```

Sla het nieuwe versienummer op in een basisomgevingsvariabele voor gebruik in volgende opdrachten:

```bash
export FASTLY_EDIT_VERSION=<Version>
```

### Stap 3: Een aangepast VCL-fragment maken

Maak en sla uw aangepaste VCL-code op in een JSON-bestand met de volgende inhoud en indeling:

```json
{
  "name": "<name>",
  "dynamic": "0",
  "type": "<type>",
  "priority": "100",
  "content": "<code all in one line>"
}
```

De volgende waarden zijn beschikbaar:

- `name`—Naam voor het VCL-fragment.

- `dynamic`—Geeft aan of dit een [regulier fragment](https://docs.fastly.com/en/guides/about-vcl-snippets) of [dynamisch fragment](https://docs.fastly.com/guides/vcl-snippets/using-dynamic-vcl-snippets).

- `type`—Geeft de locatie op voor het invoegen van het gegenereerde fragment, zoals `init` (boven subroutines) en `recv` (binnen subroutines). Zie [VCL-fragmentobjectwaarden snel](https://docs.fastly.com/api/config#snippet) voor informatie over deze waarden.

- `priority`—Een waarde van `1` tot `100` die bepaalt wanneer de de fragmentcode van douaneVCL loopt. Aangepaste VCL-fragmenten met lagere waarden worden eerst uitgevoerd.

  Alle standaard VCL-code uit de Fastly VCL-module heeft een `priority` van `50`. Als u wilt dat een handeling het laatst plaatsvindt of als u de standaard VCL-code wilt overschrijven, gebruikt u een hoger getal, zoals `100`. Als u de aangepaste VCL-fragmentcode direct wilt uitvoeren, stelt u de prioriteit in op een lagere waarde, zoals `5`.

- `content`—Het fragment van VCL-code dat op één regel wordt uitgevoerd, zonder regeleinden. Zie [Voorbeeld van aangepast VCL-fragment](#example-vcl-snippet-code).

### Stap 4: voeg VCL-fragment toe aan de snelconfiguratie

De snelheids-API gebruiken [fragment maken](https://docs.fastly.com/api/config#snippet_41e0e11c662d4d56adada215e707f30d) bewerking om het aangepaste VCL-fragment toe te voegen aan de VCL-versie.

```bash
curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_EDIT_VERSION/snippet -H 'Content-Type: application/json' -X POST --data @<filename.json>
```

De `<filename.json>` Dit is de naam van het bestand dat u in de vorige stap hebt voorbereid. Herhaal deze opdracht voor elk VCL-fragment.

Als u een `500 Internal Server Error` Controleer de syntaxis van JSON-bestanden om te controleren of u een geldig bestand uploadt.

### Stap 5: Valideer en activeer aangepaste VCL-fragmenten

Nadat u een aangepast VCL-fragment hebt toegevoegd, wordt het fragment snel ingevoegd in de VCL-versie die u bewerkt. Als u wijzigingen wilt toepassen, voert u de volgende stappen uit om de VCL-fragmentcode te valideren en de VCL-versie te activeren.

1. De snelheids-API gebruiken [VCL-versie valideren](https://docs.fastly.com/api/config#version_97f8cf7bfd5dc2e5ea1933d94dc5a9a6) bewerking om de bijgewerkte VCL-code te verifiëren.

   ```bash
   curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_EDIT_VERSION/validate
   ```

   Als de Fastly-API een fout retourneert, verhelpt u het probleem en valideert u de bijgewerkte VCL-versie opnieuw.

1. De snelheids-API gebruiken [activate](https://docs.fastly.com/api/config#version_0b79ae1ba6aee61d64cc4d43fed1e0d5) om de nieuwe VCL-versie te activeren.

   ```bash
   curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_EDIT_VERSION/activate -X PUT
   ```

## Snelle API-referentie voor VCL-fragmenten

In deze API-aanvraagvoorbeelden worden geëxporteerde omgevingsvariabelen gebruikt om de referenties te leveren die u snel wilt verifiëren. Voor details over deze bevelen, zie [Snelle API-referentie](https://docs.fastly.com/api/config#vcl).

>[!NOTE]
>
>Gebruik deze opdrachten om fragmenten te beheren die u met de snelheids-API hebt toegevoegd. Als u fragmenten hebt toegevoegd vanuit de beheerfunctie, raadpleegt u [VCL-fragmenten beheren met behulp van Admin](#manage-vcl-using-the-api).

- **Actief VCL-versienummer ophalen**

  ```bash
  curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/active
  ```

- **Alle gewone VCL-fragmenten weergeven die aan een service zijn gekoppeld**

  ```bash
  curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION/snippet
  ```

- **Een afzonderlijk fragment bekijken**

  ```bash
  curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION/snippet/<snippet_name>
  ```

  De `<snippet_name>` is de naam van een fragment, zoals `my_regular_snippet`.

- **Een fragment bijwerken**

  Wijzig de [voorbereid JSON-bestand](#step-3-create-a-custom-vcl-snippet) en verzendt het volgende verzoek:

  ```bash
  curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION/snippet/<snippet_name> -H 'Content-Type: application/json' -X PUT --data @<filename.json>
  ```

- **Een afzonderlijk VCL-fragment verwijderen**

  Een lijst met fragmenten ophalen en het volgende gebruiken `curl` opdracht met de specifieke fragmentnaam die moet worden verwijderd:

  ```bash
  curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION/snippet/<snippet_name> -X DELETE
  ```

- **Waarden overschrijven in het dialoogvenster [standaard VCL-code](https://github.com/fastly/fastly-magento2/tree/master/etc/vcl_snippets)**

  Maak een fragment met bijgewerkte waarden en wijs een prioriteit toe van `100`.
