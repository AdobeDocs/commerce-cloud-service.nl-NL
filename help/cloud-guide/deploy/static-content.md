---
title: Statische implementatie van inhoud
description: Leer meer over strategieën voor het implementeren van statische inhoud, zoals afbeeldingen, scripts en CSS, op Adobe Commerce op cloud-infrastructuurprojecten.
feature: Cloud, Build, Deploy, SCD
exl-id: e128d0d5-1326-44e5-a822-009e11ba105f
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# Statische strategieën voor implementatie van inhoud

De statische plaatsing van de inhoud (SCD) heeft een significante invloed op het proces van de opslagplaatsing dat afhangt van hoeveel te produceren inhoud-zoals beelden, manuscripten, CSS, video&#39;s, thema&#39;s, scènes, en Web-pagina&#39;s-en wanneer om de inhoud te produceren. De standaardstrategie genereert bijvoorbeeld statische inhoud tijdens de [implementatiefase](process.md#deploy-phase-deploy-phase) wanneer de plaats op onderhoudswijze is; nochtans neemt deze plaatsingsstrategie tijd om de inhoud aan opgezette inhoud direct te schrijven `pub/static` directory. U hebt verschillende opties of strategieën om u te helpen de implementatietijd afhankelijk van uw behoeften te verbeteren.

## JavaScript- en HTML-inhoud optimaliseren

U kunt bundelen en miniaturen gebruiken om geoptimaliseerde JavaScript- en HTML-inhoud te maken tijdens de implementatie van statische inhoud.

### Inhoud minimaliseren

U kunt de laadtijd van SCD tijdens het implementatieproces verbeteren als u het kopiëren van de statische weergavebestanden in het dialoogvenster `var/view_preprocessed` map en genereren _geminimaliseerd_ HTML op verzoek. U kunt dit activeren door het [SKIP_HTML_MINIFICATION](../environment/variables-global.md#skiphtmlminification) globale omgevingsvariabele naar `true` in de `.magento.env.yaml` bestand.

>[!NOTE]
>
>Beginnen met de `ece-tools` pakketversie 2002.0.13, wordt de standaardwaarde voor de variabele SKIP_HTML_MINIFICATION ingesteld op `true`.

U kunt opslaan **meer** implementatietijd en schijfruimte door het aantal onnodige themabestanden te verminderen. U kunt bijvoorbeeld de `magento/backend` thema in het Engels en een aangepast thema in andere talen. U kunt deze themamontages met vormen [SCD_MATRIX](../environment/variables-deploy.md#scdmatrix) omgevingsvariabele.

## Een implementatiestrategie kiezen

De strategieën van de plaatsing verschillen gebaseerd op of u verkiest om statische inhoud tijdens te produceren _build_ de _inzetten_ fase, of _op aanvraag_. Zoals gezien in de volgende grafiek, is het produceren van statische inhoud tijdens de opstellen fase de minste optimale keus. Zelfs met geminiateerde HTML, moet elk inhoudsbestand naar de gekoppelde server worden gekopieerd `~/pub/static` map, die veel tijd kan kosten. Het genereren van statische inhoud op aanvraag lijkt de optimale keuze. Als het inhoudsbestand echter niet bestaat in de cache die het op dat moment genereert, wordt het opgevraagd. Hierdoor wordt laadtijd toegevoegd aan de gebruikerservaring. Daarom is het produceren van statische inhoud tijdens de bouwstijlfase de meest optimale.

![SCD-belastingvergelijking](../../assets/scd-load-times.png)

### Het SCD instellen bij het samenstellen

Het produceren van statische inhoud tijdens de bouwstijlfase met geminificeerde HTML is de optimale configuratie voor [**nuldowntime** implementaties](reduce-downtime.md), ook wel bekend als de **ideale status**. In plaats van bestanden te kopiëren naar een gemonteerd station, wordt er een koppeling gemaakt van de `./init/pub/static` directory.

Voor het genereren van statische inhoud hebt u toegang tot thema&#39;s en landinstellingen nodig. Adobe Commerce slaat thema&#39;s op in het bestandssysteem, dat toegankelijk is tijdens de constructiefase. Adobe Commerce slaat de landinstellingen echter op in de database. De database is _niet_ beschikbaar tijdens de bouwstijlfase. Om de statische inhoud tijdens de bouwstijlfase te produceren, moet u gebruiken `config:dump` in de `ece-tools` verpakken om landinstellingen naar het bestandssysteem te verplaatsen. De landinstellingen worden gelezen en opgeslagen in de `app/etc/config.php` bestand.

**Om uw project te vormen om SCD op bouwstijl te produceren**:

1. Wijzig op uw lokale werkstation de projectmap.
1. Gebruik SSH om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Landinstellingen verplaatsen naar het bestandssysteem en vervolgens de [`config.php` file](../development/commerce-version.md#create-a-configphp-file).

1. De `.magento.env.yaml` Het configuratiebestand moet de volgende waarden bevatten:

   - [SKIP_HTML_MINIFICATION](../environment/variables-global.md#skip_html_minification) is `true`
   - [SKIP_SCD](../environment/variables-build.md#skip_scd) in constructiefase `false`
   - [SCD_STRATEGY](../environment/variables-build.md#scd_strategy) is `compact`

1. Verifieer configuratie van [Haak na implementatie](../application/hooks-property.md) in de `.magento.app.yaml` bestand.

1. Controleer uw instellingen door het [Slimme wizard voor de ideale status](smart-wizards.md).

   ```bash
   php ./vendor/bin/ece-tools wizard:ideal-state
   ```

### SCD op verzoek instellen

Het genereren van SCD op verzoek is optimaal voor een ontwikkelingsworkflow in de integratieomgeving. Het vermindert plaatsingstijd zodat u uw implementaties kunt snel herzien en integratietests in werking stellen. De optie [SCD_ON_DEMAND](../environment/variables-global.md#scdondemand) omgevingsvariabele in het mondiale stadium van de `.magento.env.yaml` bestand. De variabele SCD_ON_DEMAND negeert alle andere configuraties met betrekking tot SCD en wist bestaande inhoud van `~/pub/static` directory.

Wanneer het gebruiken van SCD op bestelling strategie, helpt het om het geheime voorgeheugen met pagina&#39;s vooraf te laden u verwacht om, zoals de homepage te verzoeken. Voeg uw lijst met verwachte pagina&#39;s toe in het dialoogvenster [WARM_UP_PAGES](../environment/variables-post-deploy.md#warmuppages) omgevingsvariabele in de fase na de implementatie van de `.magento.env.yaml` bestand.

>[!WARNING]
>
>Gebruik de SCD-strategie op verzoek niet in de productieomgeving.

### SCD wordt overgeslagen

Soms kunt u het genereren van statische inhoud volledig overslaan. U kunt de [SKIP_SCD](../environment/variables-build.md#skipscd) omgevingsvariabele in het algemene werkgebied om andere configuraties met betrekking tot SCD te negeren. Dit heeft geen invloed op de bestaande inhoud in de `~/pub/static` directory.
