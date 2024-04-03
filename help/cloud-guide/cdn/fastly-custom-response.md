---
title: Fout- en onderhoudspagina's aanpassen
description: Leer hoe u de standaardfoutpagina aanpast die wordt weergegeven wanneer aanvragen bij de server met de snelste oorsprong mislukken.
feature: Cloud, Configuration, Security
exl-id: 16722821-b928-4872-8cef-7f049e600f0d
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# Fout- en onderhoudspagina&#39;s aanpassen

Wanneer een verzoek aan de Fastly oorsprong ontbreekt, keert de Snelle standaardreactiepagina&#39;s met basis het formatteren en generische overseinen terug die voor gebruikers kunnen verwarren. Bijvoorbeeld, kort keert de volgende standaardfoutenpagina terug wanneer een verzoek aan de Fastly oorsprong wegens een fout 503 ontbreekt.

![Standaardfoutpagina snel](../../assets/cdn/fastly-503-example.png)

U kunt uw Adobe Commerce-winkelconfiguratie bijwerken en zo sommige standaardresponspagina&#39;s vervangen door pagina&#39;s met vriendelijker berichten en verbeterde HTML-opmaak, zoals in het volgende voorbeeld wordt getoond.

![Snelle aangepaste foutpagina](../../assets/cdn/fastly-new-error-page.png)

Momenteel kunt u de volgende snelstresponspagina&#39;s aanpassen voor uw Adobe Commerce-project voor cloudinfrastructuur.

- [Serverfouten - Interne serverfout, time-out of uitval van siteonderhoud (foutcode 500 of hoger)](#customize-the-503-error-page)
- [WAF die gebeurtenissen blokkeren die voorkomen wanneer WAF verdacht verzoekverkeer (403 wordt verboden) ontdekt](#customize-the-waf-error-page)

**HTML coderingsvereisten:**

De HTML-code voor de aangepaste pagina moet aan de volgende vereisten voldoen:

- Inhoud kan maximaal 65.535 tekens bevatten.
- Geef alle CSS inline op in de HTML-bron.
- Bundel afbeeldingen op de pagina HTML met base64, zodat ze ook worden weergegeven als Fastly offline is. Zie [Gegevens-URI&#39;s op de css-tricks-site](https://css-tricks.com/data-uris/).

## De pagina met 503 fouten aanpassen

Klanten zien de standaardpagina met 503 fouten in de volgende gevallen:

- Wanneer een verzoek aan de snelste oorsprong een reactiestatus groter dan 500 terugkeert
- Wanneer de Fastly oorsprong neer is, zoals een onderbreking, onderhoudsactiviteit of gezondheidskwesties

U kunt de standaardpagina aanpassen door de volgende HTML-code aan te passen en de opmaak aan te passen aan het Adobe Commerce-winkelthema en de titel en het bericht indien nodig aan te passen.

```html
<!DOCTYPE html>
<html>
   <head>
      <meta charset="UTF-8">
         <title>503</title>
   </head>
   <body>
      <p>Service unavailable</p>
   </body></html>
```

Controleer of de gewijzigde bron correct wordt weergegeven in de browser. Voeg vervolgens de aangepaste HTML-code toe aan de configuratie Snelst.

De aangepaste reactiepagina toevoegen aan de snelconfiguratie:

{{admin-login-step}}

1. Selecteren **Winkels** > **Instellingen** > **Configuratie** > **Geavanceerd** > **Systeem**.

1. Vouw in het rechterdeelvenster uit **Volledige paginacache** > **Snelle configuratie** > **Aangepaste synthetische pagina&#39;s**.

   ![503-foutpagina bewerken](../../assets/cdn/fastly-custom-synthetic-pages-edit-html.png)

1. Selecteren **HTML instellen**.

1. Kopieer en plak de broncode voor de aangepaste reactiepagina in het veld HTML.

   ![Pagina met 503-fouten bijwerken](../../assets/cdn/fastly-customize-503-response.png)

1. Selecteren **Uploaden** boven aan de pagina om de aangepaste HTML-bron naar de snelserver te uploaden.

1. Selecteren **Config opslaan** boven aan de pagina om het bijgewerkte configuratiebestand op te slaan.

1. Vernieuw de cache.

   - Selecteer in het bericht boven aan de pagina de optie *Cachebeheer* koppeling.

   - Selecteer op de pagina Cachebeheer de optie **Cache van Magento leegmaken**.

## De WAF-foutpagina aanpassen

Klanten zien de volgende standaard WAF foutpagina wanneer een aanvraag naar de snelste oorsprong mislukt met een `403 Forbidden` fout veroorzaakt door [WAF](fastly-waf-service.md) blokkeringsgebeurtenis.

![WAF-foutpagina](../../assets/cdn/fastly-waf-403-error.png)

In het volgende codevoorbeeld wordt de HTML-bron voor de standaardpagina getoond:

```html
<html>
  <head>
    <title>Magento 403 Forbidden</title>
  </head>
  <body>
    <p>The requested URL was rejected.</p>
    <p>For additional information, please contact support and provide this reference ID:</p>
    <p>"} req.http.x-request-id {"</p>
    <p><button onclick='history.back();'>Go Back</button></p>
  </body>
</html>
```

U kunt de **Aangepaste synthetische pagina&#39;s** > **WAF-pagina bewerken** in het configuratiemenu Snelheid om de standaardcode voor uw Adobe Commerce op het project van de wolkeninfrastructuur aan te passen. Wanneer u de code bewerkt, behoudt u de volgende regel met de referentie-id voor de WAF-blokkeringsgebeurtenis:

```html
<p>"} req.http.x-request-id {"</p>
```

>[!NOTE]
>
>De optie WAF bewerken is alleen beschikbaar als de Beheerde Cloud WAF-service is ingeschakeld voor uw Adobe Commerce-infrastructuurproject in de cloud.

**De WAF-foutpagina bewerken**:

1. [Aanmelden bij de beheerder](../../get-started/onboarding.md#access-your-admin-panel).

1. Selecteren **Winkels** > **Instellingen** > **Configuratie** > **Geavanceerd** > **Systeem**.

1. Vouw in het rechterdeelvenster uit **Volledige paginacache** > **Snelle configuratie** > **Aangepaste synthetische pagina&#39;s**.

   ![Optie voor pagina met WAF-fouten bewerken](../../assets/cdn/fastly-custom-synthetic-pages-edit-waf.png)

1. Selecteren **WAF-pagina bewerken**.

1. Vul de velden in om de HTML bij te werken.

   ![WAF-foutpagina bijwerken](../../assets/cdn/fastly-edit-waf-html.png)

   - **Status** — Selecteer de `403 Forbidden` status.
   - **MIME-type** — Type `text/html`.
   - **Inhoud** — Bewerk de standaardreactie van de HTML om aangepaste CSS toe te voegen en werk de titel en het bericht zo nodig bij.

1. Selecteren **Uploaden** boven aan de pagina om de aangepaste HTML-bron naar de snelserver te uploaden.

1. Selecteren **Config opslaan** boven aan de pagina om het bijgewerkte configuratiebestand op te slaan.

1. Vernieuw de cache.

   - Selecteer in het bericht boven aan de pagina de optie **Cachebeheer** koppeling.

   - Selecteer op de pagina Cachebeheer de optie **Cache van Magento leegmaken**.

## Foutrapportnummer weergeven

Standaard worden met Snelheid alle Adobe Commerce-fouten achter de opdracht *503 Service niet beschikbaar* fout. Als u het rapportnummer van het foutenlogboek wilt weergeven, zodat u de foutdetails in de logboeken kunt vinden en bekijken, opent u de website zonder dat u snel de volgende stappen uitvoert:

1. Haal het IP-adres van uw winkel op:

   - Voor Pro Staging- en Productieomgevingen:

     ```bash
     nslookup {your_project_id}.ent.magento.cloud
     ```

   - Voor Pro-integratieomgevingen en Starter-omgevingen:

     ```bash
     nslookup gw.{your_region}.magentosite.cloud
     ```

1. Voeg uw toepassingsdomein en IP adres aan het gastheerdossier op uw lokale werkstation toe:

   ```text
   {server_IP} {store_domain}
   ```

1. Wis de browsercache en cookies (of schakel over naar de incognitomodus).

1. Open de website van uw winkel opnieuw om de foutcode weer te geven.

1. Gebruik de foutcode om de details in het foutrapportbestand te zoeken:

   - [Verbinding maken met de desbetreffende omgeving met behulp van SSH](../development/secure-connections.md#connect-to-a-remote-environment)

   - Zoek de `./var/report/{error_number}` bestand.
