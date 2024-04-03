---
title: Robots voor site-toewijzing en zoekprogramma's toevoegen
description: Leer hoe u robots voor sites met hyperlinks en zoekprogramma's aan Adobe Commerce kunt toevoegen op cloudinfrastructuur.
feature: Cloud, Configuration, Search, Site Navigation
exl-id: b98f43fa-1878-466d-8ea0-1e7207af8b60
source-git-commit: ee1db75c73c086e0ea54e1a7591ca7f2b4d2b36d
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# Robots voor site-toewijzing en zoekprogramma&#39;s toevoegen

Een poging om het `sitemap.xml` resulteert het bestand in de hoofdmap in de volgende fout:

```terminal
Please make sure that "/" is writable by the web-server.
```

Met Adobe Commerce op cloudinfrastructuur kunt u alleen schrijven naar specifieke mappen, zoals `var`, `pub/media`, `pub/static`, of `app/etc`. Wanneer u de `sitemap.xml` bestand met behulp van het deelvenster Beheer moet u de `/media/` pad.

U hoeft geen `robots.txt` bestand omdat het de `robots.txt` inhoud op aanvraag en slaat deze op in de database. U kunt de inhoud in uw browser bekijken met de `<domain.your.project>/robots.txt` of `<domain.your.project>/robots` koppeling.

Hiervoor is ECE-Tools versie 2002.0.12 en hoger vereist, met een bijgewerkte versie `.magento.app.yaml` bestand. Zie een voorbeeld van deze regels in de [magento-cloud-opslagplaats](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml#L43-L49).

**Om een `sitemap.xml` bestand in versie 2.2 en hoger**:

1. Open de beheerder.
1. Op de _Marketing_ menu, klikt u op **Site-overzicht** in de _SEO &amp; Search_ sectie.
1. In de _Site-overzicht_ weergeven, klikken **Sitemap toevoegen**.
1. In de _Nieuwe site-overzicht_ Voer de volgende waarden in:

   - **Bestandsnaam**:`sitemap.xml`
   - **Pad**:`/media/`

1. Klikken **Opslaan en genereren**. Het nieuwe site-overzicht wordt beschikbaar in het dialoogvenster _Site-overzicht_ raster.
1. Klik op het pad in het dialoogvenster _Koppeling voor Google_ kolom.

**Inhoud toevoegen aan de `robots.txt` file**:

1. Open de beheerder.
1. Op de _Inhoud_ menu, klikt u op **Configuratie** in de _Ontwerp_ sectie.
1. In de _Ontwerpconfiguratie_ weergeven, klikken **Bewerken** voor de website in het _Handeling_ kolom.
1. In de _Hoofdwebsite_ weergeven, klikken **Zoekmachinekrobots**.
1. Werk de **Aangepaste instructies voor robots.txt bewerken** veld.
1. Klikken **Configuratie opslaan**.
1. Controleer de `<domain.your.project>/robots.txt` bestand of `<domain.your.project>/robots` URL in uw browser.

>[!NOTE]
>
>Als de `<domain.your.project>/robots.txt` bestand genereert een `404 error`, [Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om de omleiding te verwijderen uit `/robots.txt` tot `/media/robots.txt`.

## Herschrijven met VCL-fragment snel

Als u verschillende domeinen hebt en u afzonderlijke site-overzichten nodig hebt, kunt u een VCL maken om naar de juiste sitemap te leiden. Genereer de `sitemap.xml` in het deelvenster Beheer, zoals hierboven is beschreven, maakt u een aangepast, snel VCL-fragment om het omleiden te beheren. Zie [Aangepaste, snel VCL-fragmenten](../cdn/fastly-vcl-custom-snippets.md).

>[!NOTE]
>
> U kunt aangepaste VCL-fragmenten uploaden vanuit de beheerinterface of via de snelheids-API. Zie [Voorbeelden en zelfstudies van aangepaste VCL-fragmenten](../cdn/fastly-vcl-custom-snippets.md#example-vcl-snippet-code).

### Een VCL-fragment snel gebruiken voor omleiding

Een aangepast VCL-fragment maken om het pad te herschrijven voor `sitemap.xml` tot `/media/sitemap.xml` met de `type` en `content` sleutel-waarde paren.

```json
{
  "name": "sitemapxml_rewrite",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path ~ \"^/?sitemap.xml$\" ) { set req.url = \"/media/sitemap.xml\"; }"
}
```

In het volgende voorbeeld wordt getoond hoe u het pad herschrijft voor `robots.txt` en `sitemap.xml` tot `/media/robots.txt` en `/media/sitemap.xml`

```json
{
  "name": "sitemaprobots_rewrite",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path ~ \"^/?sitemap.xml$\" ) { set req.url = \"/media/sitemap.xml\"; } else if (req.url.path ~ \"^/?robots.txt$\") { set req.url = \"/media/robots.txt\";}"
}
```

**Een VCL-fragment snel gebruiken voor een bepaald domein omleiden**:

Een `pub/media/domain_robots.txt` bestand, waarbij het domein `domain.com`en gebruik het volgende VCL-fragment:

```json
{
  "name": "domain_robots",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path == \"/robots.txt\" ) { if ( req.http.host ~ \"(domain).com$\" ) { set req.url = \"/media/\" re.group.1 \"_robots.txt\"; }}"
}
```

De VCL-fragmentroutes `http://domain.com/robots.txt` en presenteert de `pub/media/domain_robots.txt` bestand.

Een omleiding configureren voor `robots.txt` en `sitemap.xml` in één fragment maken `pub/media/domain_robots.txt` en `pub/media/domain_sitemap.xml` bestanden, waarbij het domein `domain.com` en gebruik het volgende VCL-fragment:

```json
{
  "name": "domain_sitemaprobots",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path == \"/robots.txt\" ) { if ( req.http.host ~ \"(domain).com$\" ) { set req.url = \"/media/\" re.group.1 \"_robots.txt\"; }} else if ( req.url.path == \"/sitemap.xml\" ) { if ( req.http.host ~ \"(domain).com$\" ) {  set req.url = \"/media/\" re.group.1 \"_sitemap.xml\"; }}"
}
```

In de `sitemap` admin config, moet u de plaats van het dossier specificeren gebruikend `pub/media/` eerder dan `/`.

### Indexeren via zoekprogramma configureren

Om te activeren `robots.txt` aanpassingen, moet u toelaten **Indexeren door zoekmachines is ingeschakeld voor`<environment-name>`** in uw projectinstellingen.

![Gebruik de [!DNL Cloud Console] om omgevingen te beheren](../../assets/robots-indexing-by-search-engine.png)

>[!NOTE]
>
>Als u PWA Studio gebruikt en tot uw gevormd niet kunt toegang hebben `robots.txt` bestand, toevoegen `robots.txt` aan de [Lijst van gewenste personen voornaam](https://github.com/magento/magento2-upward-connector#front-name-allowlist) om **Winkels** > Configuratie > **Algemeen** > **Web** > UPWARD PWA Configuration.
