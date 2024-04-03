---
title: Aangepaste VCL voor het toestaan van aanvragen
description: De inkomende verzoeken van de filter en verleent toegang door IP adres voor de plaatsen van Adobe Commerce door met een Fastly Edge ACL lijst en een douaneVCL fragment.
feature: Cloud, Configuration, Security
exl-id: a6ee958a-c3d3-47be-b2df-510707f551fc
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# Aangepaste VCL voor het toestaan van aanvragen

U kunt een Snelle Rand ACL lijst met een codefragment van douaneVCL gebruiken om inkomende verzoeken te filtreren en toegang door IP adres toe te staan. De ACL lijst specificeert de IP adressen toe te staan.

Creeer een lijst van gewenste personen om toegang tot uw het Opvoeren milieu te beperken zodat slechts de verzoeken van gespecificeerde IP adressen voor interne ontwikkelaars en de goedgekeurde externe diensten worden toegelaten. U kunt ook een lijst van gewenste personen maken om de toegang tot de beheeromgeving te beveiligen in de omgeving voor staging en productie.

In het volgende voorbeeld wordt getoond hoe u een aangepast VCL-fragment met een [Snelle toegangsbeheerlijst (ACL)](https://docs.fastly.com/guides/access-control-lists/about-acls) om toegang tot Admin voor een Adobe Commerce op het projectmilieu van de wolkeninfrastructuur te beveiligen. Wanneer u het douaneVCL fragment aan het milieu van de Wolk toevoegt, staat snel slechts verzoeken van IP adressen inbegrepen in ACL toe.

>[!TIP]
>
>Voor Staging- en integratieomgevingen die niet openbaar toegankelijk moeten zijn, gebruikt u de optie voor HTTP-toegangsbeheer in het dialoogvenster [[!DNL Cloud Console]](../project/overview.md#access-the-project-web-interface) om toegang tot de volledige plaats door IP adres te beheren.

**Vereisten:**


{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- Lijst van cliëntIP adressen om op de lijst van gewenste personen te omvatten

## Creeer Rand ACL voor het toestaan van cliëntIP adressen

Edge ACLs leidt IP adreslijsten voor het beheren van toegang tot uw plaats. In dit voorbeeld, creeert u Rand ACL en voegt de lijst van cliëntIP adressen toe die worden toegestaan om tot Admin voor uw projectmilieu toegang te hebben.

{{admin-login-step}}

1. Klikken **Winkels** > Instellingen > **Configuratie** > **Geavanceerd** > **Systeem**.

1. Uitbreiden **Volledige paginacache** > **Snelle configuratie** > **Edge ACL**.

1. Creeer de ACL container:

   - Klikken **ACL toevoegen**.

   - Op de *ACL-container* pagina, voert u een **ACL-naam**—`allowlist`.

   - Selecteren **Activeren na de wijziging** om uw veranderingen in de versie van de Snelle de dienstconfiguratie op te stellen die u uitgeeft.

   - Klikken **Uploaden** om ACL aan uw Fastly de dienstconfiguratie vast te maken.

1. Voeg de lijst met IP-adressen toe die toegang geven tot de beheerder:

   - Klik op het pictogram Instellingen voor het dialoogvenster `allowlist` ACL.

   - Voeg en sla de *IP-waarde* voor elk cliëntIP adres.

   - Klikken **Annuleren** om naar de pagina van de systeemconfiguratie terug te keren.

1. Klikken **Config opslaan**.

1. Vernieuw de cache volgens het bericht boven aan de pagina.

## Het aangepaste VCL-fragment maken om beheertoegang te beveiligen

De volgende aangepaste VCL-fragmentcode (JSON-indeling) toont de logica voor het filteren van aanvragen naar Admin en het toestaan van toegang als het client-IP-adres overeenkomt met een adres in het dialoogvenster `allowlist` ACL.

```json
{
  "name": "allowlist",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ((req.url ~ \"^/admin\") && !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 \"Forbidden\"; }"
}
```

Voor [een aangepast fragment maken](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-allowlist.html#add-the-custom-vcl-snippet) In dit voorbeeld controleert u de waarden om te bepalen of u wijzigingen moet aanbrengen. Voer vervolgens elke waarde in de desbetreffende velden in, zoals `type` in het veld Type, `content` in het veld Inhoud.

- `name` — Naam voor het VCL-fragment. In dit voorbeeld: `allowlist`.

- `priority` — Hiermee bepaalt u wanneer het VCL-fragment wordt uitgevoerd. De prioriteit is `5` om onmiddellijk in werking te stellen en te controleren of een Admin- verzoeken uit een toegestaan IP adres komen. Het fragment wordt uitgevoerd vóór de standaard VCL-fragmenten voor Magento&#39;s (`magentomodule_*`) een prioriteit van 50. Stel de prioriteit voor elk aangepast fragment in op een waarde hoger of lager dan 50, afhankelijk van het tijdstip waarop het fragment moet worden uitgevoerd. Fragmenten met een lagere prioriteit worden eerst uitgevoerd.

- `type` — Geeft een locatie op waar het fragment moet worden ingevoegd in de versioned VCL code. Dit VCL is een `recv` fragmenttype waarmee de fragmentcode aan de `vcl_recv` subroutine onder de standaard VCL-code en boven objecten.

- `content` — Het fragment van VCL-code dat moet worden uitgevoerd. In dit voorbeeld vragen de codefilters aan Admin en staan toegang toe als het cliëntIP adres een adres in `allowlist` ACL. Als het adres niet aanpast, wordt het verzoek geblokkeerd met een `403 Forbidden` fout.

  Als de URL voor uw beheerder is gewijzigd, vervangt u de samplewaarde `/admin` met de URL voor uw omgeving. Bijvoorbeeld: `/company-admin`.

In het codevoorbeeld, de voorwaarde `!req.http.Fastly-FF` is belangrijk bij gebruik [Oorspronkelijke afscherming](fastly-custom-cache-configuration.md#configure-back-ends-and-origin-shielding). Verwijder of bewerk deze code niet.

Na het herzien van en het bijwerken van de code voor uw milieu, gebruik één van beiden van de volgende methodes om het fragment van douaneVCL aan uw Fastly de dienstconfiguratie toe te voegen:

- [Het aangepaste VCL-fragment toevoegen vanuit Beheer](#add-the-custom-vcl-snippet). Deze methode wordt aanbevolen als u toegang kunt krijgen tot de beheerder. (Vereist [Snelle CDN-module voor Magento 2 versie 1.2.58](fastly-configuration.md#upgrade) of hoger.)

- Sla het JSON-codevoorbeeld op in een bestand (bijvoorbeeld `allowlist.json`) en [uploaden met de snelheids-API](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). Gebruik deze methode als u geen toegang hebt tot de beheerder.

## Het aangepaste VCL-fragment toevoegen

{{admin-login-step}}

1. Klikken **Winkels** > Instellingen > **Configuratie** > **Geavanceerd** > **Systeem**.

1. Uitbreiden **Volledige paginacache** > **Snelle configuratie** > **Aangepaste VCL-fragmenten**.

1. Klikken **Aangepast fragment maken**.

1. Voeg de waarden van het VCL-fragment toe:

   - **Naam** — `allowlist`

   - **Type** — `recv`

   - **Prioriteit** — `5`

   - Voeg de **VCL** inhoud van fragment:

     ```conf
     if ((req.url ~ "^/admin") && !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 "Forbidden";}
     ```

1. Klikken **Maken** om het VCL-fragmentbestand met het naampatroon te genereren `type_priority_name.vcl`bijvoorbeeld `recv_5_allowlist.vcl`

1. Klik op **VCL snel uploaden naar** in de *Snelle configuratie* om het bestand toe te voegen aan de configuratie van de Fastly-service.

1. Nadat het uploaden is voltooid, vernieuwt u de cache volgens het bericht boven aan de pagina.

Hiermee wordt de bijgewerkte versie van de VCL-code snel gevalideerd tijdens het uploadproces. Als de validatie mislukt, bewerkt u het aangepaste VCL-fragment om het probleem op te lossen. Vervolgens uploadt u de VCL opnieuw.

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
