---
title: Blokverwijzingsspam
description: Blokkeer verwijzingspamme van uw site met behulp van het snelste randwoordenboek en een aangepast VCL-fragment.
feature: Cloud, Configuration, Security
exl-id: 665bac93-75db-424f-be2c-531830d0e59a
source-git-commit: 7a181af2149eef7bfaed4dd4d256b8fa19ae1dda
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# Blokverwijzingsspam

Het volgende voorbeeld toont hoe te om te vormen [Dichtstbijliggend woordenboek](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api) met een aangepast VCL-fragment om verwijzingsspam van uw Adobe Commerce te blokkeren op de cloudinframesite.

>[!NOTE]
>
>Wij adviseren toevoegend de configuraties van douaneVCL aan een het Opvoeren milieu waar u hen kunt testen alvorens hen tegen het milieu van de Productie in werking te stellen.

**Vereisten:**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- Controleer uw sitelogboeken op nepverwijzing-URL&#39;s en maak een lijst met domeinen die u wilt blokkeren.

## Een lijst van gewezen personen met referentie maken

De Woordenboeken van de rand leiden tot sleutel-waardeparen die voor functies VCL tijdens VCL fragmentverwerking toegankelijk zijn. In dit voorbeeld maakt u een Edge-woordenboek met de lijst met referentiewebsites die u wilt blokkeren.

{{admin-login-step}}

1. Klikken **Winkels** > **Instellingen** > **Configuratie** > **Geavanceerd** > **Systeem**.

1. Uitbreiden **Volledige paginacache** > **Snelle configuratie** > **Randwoordenboeken**.

1. De container voor woordenboeken maken:

   - Klikken **Container toevoegen**.

   - Op de *Container* pagina, voert u een **Woordenboeknaam**—`referrer_blocklist`.

   - Selecteren **Activeren na de wijziging** om uw veranderingen in de versie van de Snelle de dienstconfiguratie op te stellen die u uitgeeft.

   - Klikken **Uploaden** om het woordenboek aan uw Fastly de dienstconfiguratie toe te voegen.

1. Voeg de lijst met domeinnamen die u wilt blokkeren toe aan het dialoogvenster `referrer_blocklist` woordenboek:

   - Klik op het pictogram Instellingen voor het dialoogvenster `referrer_blocklist` woordenboek.

   - U kunt sleutelwaardeparen toevoegen en opslaan in het nieuwe woordenboek. Voor dit voorbeeld, elk **Sleutel** is de domeinnaam van een referentie-URL die moet worden geblokkeerd en **Waarde** is `true`.

     ![Slechte verwijzingenwoordenboekitems toevoegen](../../assets/cdn/fastly-referrer-blocklist-dictionary.png)

   - Klikken **Annuleren** om naar de pagina van de systeemconfiguratie terug te keren.

1. Klikken **Config opslaan**.

1. Vernieuw de cache volgens het bericht boven aan de pagina.

Zie voor meer informatie over Edge-woordenboeken [Edge-woordenboeken maken en gebruiken](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api) en [aangepaste VCL-fragmenten](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api#custom-vcl-examples) in de Fastly documentatie.

## Een aangepast VCL-fragment maken om verwijzingsspam te blokkeren

De volgende aangepaste VCL-fragmentcode (JSON-indeling) toont de logica voor het controleren en blokkeren van aanvragen. Het VCL-fragment legt de host van een verwijzingswebsite vast in een header en vergelijkt vervolgens de hostnaam met de lijst met URL&#39;s in het dialoogvenster `referrer_blocklist` woordenboek. Als de hostnaam overeenkomt, wordt de aanvraag geblokkeerd met een `403 Forbidden` fout.

```json
{
  "name": "block_bad_referrer",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "set req.http.Referer-Host = regsub(req.http.Referer, \"^https?:\/\/?([^:\/s]+).*$\", \"\\1\"); if (table.lookup(referrer_blocklist, req.http.Referer-Host)) { error 403 \"Forbidden\"; }"
}
```

Voordat u een op dit voorbeeld gebaseerd fragment maakt, controleert u de waarden om te bepalen of u wijzigingen wilt aanbrengen:

- `name` — Naam voor het VCL-fragment. In dit voorbeeld hebben we `block_bad_referrer`.

- `dynamic` — Waarde 0 geeft een [regulier fragment](https://docs.fastly.com/en/guides/using-regular-vcl-snippets) uploaden naar de versioned VCL voor de snelconfiguratie.

- `priority` — Hiermee bepaalt u wanneer het VCL-fragment wordt uitgevoerd. De prioriteit is `5` om deze fragmentcode uit te voeren vóór een van de standaard VCL-fragmenten voor Magento&#39;s (`magentomodule_*`) een prioriteit van 50. Stel de prioriteit voor elk aangepast fragment in op een waarde hoger of lager dan 50, afhankelijk van het tijdstip waarop het fragment moet worden uitgevoerd. Fragmenten met een lagere prioriteit worden eerst uitgevoerd.

- `type` — Geeft een locatie op die moet worden ingevoegd in het VCL-fragment. In dit voorbeeld is het VCL-fragment een `recv` fragment. Wanneer het fragment in de VCL-versie wordt ingevoegd, wordt het toegevoegd aan de `vcl_recv` subroutine, onder de standaard VCL-code Fastly en boven alle objecten.

- `content` — Het fragment van VCL-code dat op één regel wordt uitgevoerd, zonder regeleinden.

Na het herzien van en het bijwerken van de code voor uw milieu, gebruik één van beiden van de volgende methodes om het fragment van douaneVCL aan uw Fastly de dienstconfiguratie toe te voegen:

- [Het aangepaste VCL-fragment toevoegen vanuit Beheer](#add-the-custom-vcl-snippet). Deze methode wordt aanbevolen als u toegang kunt krijgen tot de beheerder. (Vereist [Snelle versie 1.2.58](fastly-configuration.md#upgrade) of hoger.)

- Sla het JSON-codevoorbeeld op in een bestand (bijvoorbeeld `allowlist.json`) en [uploaden met de snelheids-API](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). Gebruik deze methode als u geen toegang hebt tot de beheerder.

## Het aangepaste VCL-fragment toevoegen

{{admin-login-step}}

1. Klikken **Winkels** > Instellingen > **Configuratie** > **Geavanceerd** > **Systeem**.

1. Uitbreiden **Volledige paginacache** > **Snelle configuratie** > **Aangepaste VCL-fragmenten**.

1. Klikken **Aangepast fragment maken**.

1. Voeg de waarden van het VCL-fragment toe:

   - **Naam** — `block_bad_referrer`

   - **Type** — `recv`

   - **Prioriteit** — `5`

   - **VCL** inhoud van fragmenten —

     ```conf
     set req.http.Referer-Host = regsub(req.http.Referer,
     "^https?://?([^:/\s]+).*$", "1");
     if (table.lookup(referrer_blocklist, req.http.Referer-Host)) {
       error 403 "Forbidden";
     }
     ```

1. Klikken **Maken**.

   ![VCL-fragment voor aangepast verwijzingsblok maken](/help/assets/cdn/fastly-create-referrer-block-snippet.png)

1. Klik op **VCL snel uploaden naar** in de *Snelle configuratie* sectie.

1. Nadat het uploaden is voltooid, vernieuwt u de cache volgens het bericht boven aan de pagina.

Hiermee valideert u de bijgewerkte VCL-versie snel tijdens het uploadproces. Als de validatie mislukt, bewerkt u het aangepaste VCL-fragment om eventuele problemen op te lossen. Vervolgens uploadt u de VCL opnieuw.

{{automate-vcl-snippet-deployment}}

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
