---
title: Voorbeeld van het beheren van systeemspecifieke instellingen
description: Bekijk een voorbeeld van hoe u de configuratie-instellingen van de winkel in alle Adobe Commerce kunt beheren en synchroniseren in omgevingen met cloudinfrastructuren.
hidefromtoc: true
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---


# Voorbeeld van het beheren van systeemspecifieke instellingen

In dit voorbeeld wordt getoond hoe u configuratiebeheer kunt gebruiken om de opslaginstellingen in alle omgevingen consistent te houden.

In het voorbeeld wordt de volgende procedure gebruikt die in [Opslaginstellingen](store-settings.md):

1. Voer uw configuraties in in de winkel Admin van uw integratieomgeving in.
1. Een `config.php` en breng het naar uw lokale werkstation over.
1. Push `config.php` naar de externe integratieomgeving.
1. Controleer of uw instellingen niet kunnen worden bewerkt in Beheer.
1. Breng de gewenste wijzigingen aan:

   * Wijzig de configuratie-instellingen in de integratieomgeving.
   * Om configuraties toe te voegen, stel het bevel in werking om te creëren `config.php` opnieuw. Nieuwe configuraties worden aan het bestand toegevoegd.
   * Als u bestaande configuraties wilt verwijderen of bewerken, bewerkt u het bestand handmatig.
   * Vastleggen en duwen.

U kunt bijvoorbeeld de volgende instellingen instellen:

* Uitschakelen [landinstelling](https://glossary.magento.com/locale) en de statische montages van de dossieroptimalisering in uw integratiemilieu
* Optimalisatie van statische bestanden inschakelen in testomgevingen en productieomgevingen
* Vorm snel in het Staging en Productie met specifieke geloofsbrieven voor elk

_Statische bestandoptimalisatie_ betekent het samenvoegen en miniaturen van JavaScript en CSS (Cascading Style Sheets) en het miniaturen van HTML-sjablonen. Zie [Statische strategieën voor implementatie van inhoud](../deploy/static-content.md).

## Vereisten

Om deze taken van het configuratiebeheer te voltooien, hebt u het volgende nodig:

* Rol projectlezer met [omgeving &quot;admin&quot;](../project/user-access.md) rechten
* Admin URL en geloofsbrieven voor integratie, het Opvoeren, en de milieu&#39;s van de Productie

## Admin van de Handel vormen

In de integratieomgeving kunt u zich aanmelden bij de beheerder om de systeemconfiguratie-instellingen voor winkels, websites, modules of extensies, de optimalisatie van statische bestanden en systeemwaarden te wijzigen voor de implementatie van statische inhoud. Zie [Configuratiegegevens](store-settings.md#scd-performance).

**Optimalisatie-instellingen voor landinstellingen en statische bestanden wijzigen**:

1. Meld u aan bij de beheerder van de integratieomgeving. U hebt toegang tot deze URL via [[!DNL Cloud Console]](../project/overview.md).
1. Navigeren naar **Winkels** > Instellingen > **Configuratie** > Algemeen > **Algemeen**.
1. Vouw in de paginanavigatie de **Landinstellingen**.
1. Van de **Landinstelling** wijzigt u de landinstelling. U kunt deze later wijzigen.

   ![De landinstelling wijzigen](../../assets/locale-options.png)

1. Klikken **Config opslaan**.
1. Indien gevraagd, [cachegeheugen leegmaken](https://docs.magento.com/user-guide/system/cache-management.html).
1. Afmelden bij de beheerder.

## Waarden exporteren en config.php overbrengen naar uw lokale systeem

Deze stap leidt tot en brengt `config.php` configuratiebestand op de integratieomgeving gebruiken met een opdracht die u op uw lokale computer uitvoert.

Deze procedure komt overeen met stap 2 in de [aanbevolen procedure](store-settings.md). Nadat u `config.php`, breng het over naar uw lokale systeem zodat u het aan Git kunt toevoegen.

**Om te creëren en over te brengen`config.php`**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Verandering in het milieu van de Integratie.

   ```bash
   magento-cloud environment:checkout integration
   ```

1. Creeer een lokale stortplaats van het verre gegevensbestand.

   ```bash
   magento-cloud db:dump
   ```

Het volgende fragment uit `config.php` toont een voorbeeld van het wijzigen van de standaardlandinstelling in `en_GB` en wijzigen van de optimalisatie-instellingen voor statische bestanden:

```php?start_inline=1
'general' => [
     'locale' => [
         'code' => 'en_GB',
         'timezone' => 'UTC',
     ],

     ... more ...

 'dev' => [
     'template' => [
         'allow_symlink' => '0',
         'minify_html' => '0',
     ],
     'js' => [
         'merge_files' => '0',
         'enable_js_bundling' => '0',
         'minify_files' => '0',
     ],
     'css' => [
         'merge_css_files' => '0',
         'minify_files' => '0',
     ],

     ... more ...
```

## config.php naar omgevingen duwen en implementeren

Nu hebt u `config.php` en deze naar uw lokale systeem overbrengen, deze toewijzen aan Git en naar uw omgeving duwen. Deze procedure komt overeen met de stappen 3 en 4 in de [aanbevolen procedure](store-settings.md).

Met de volgende opdracht voegt u opdrachten toe aan de `master` vertakking:

```bash
git add app/etc/config.php && git commit -m "Add system-specific configuration" && git push origin master
```

Volledige codeplaatsing aan het Staging en Productie. Voor Starter drukt u op `staging` en `master` bijkantoren. Voor details op plaatsingsbevelen, zie [Je winkel implementeren](../deploy/staging-production.md).

Wacht tot de implementatie in alle omgevingen is voltooid.

## Wijzigingen in configuratie controleren

Nadat u `config.php` in uw omgeving zijn gewijzigde waarden alleen-lezen in de beheertoepassing. In dit voorbeeld zijn de gewijzigde standaardinstellingen voor landinstellingen en optimalisatie van statische bestanden niet bewerkbaar in Beheer. Deze configuratie-instellingen worden ingesteld in `config.php`.

Om uw configuratieveranderingen te verifiëren:

1. Log uit van de beheerder in een van de omgevingen.
1. Meld u weer aan bij de beheerder.
1. Klikken **Winkels** > Instellingen > **Configuratie** > Algemeen > **Algemeen**.
1. Vouw in het rechterdeelvenster uit **Landinstellingen**.

   U ziet dat verschillende velden niet kunnen worden bewerkt, zoals in het volgende voorbeeld wordt getoond. Deze configuratiemontages worden gehandhaafd door `config.php`.

   ![Bepaalde waarden kunnen niet meer worden bewerkt in Beheer](../../assets/locale-options-disabled.png)

1. Afmelden bij de beheerder.

## Systeemspecifieke configuratie-instellingen wijzigen en bijwerken

Als u een van deze instellingen moet wijzigen, wijzigt u de instelling `config.php` bestand handmatig met een teksteditor. Nadat u de bewerkingen of verwijderingen hebt voltooid, kunt u deze doorvoeren en naar de externe omgeving verplaatsen volgens de vorige stappen.

Om configuraties toe te voegen, wijzig uw integratiemilieu en stel het bevel opnieuw in werking om het dossier te produceren. Nieuwe configuraties worden toegevoegd aan de code in het bestand. Duw het aan Git na de vorige stappen.

In dit voorbeeld wijzigt u de optimalisatie-instellingen voor statische bestanden en voegt u een nieuwe instelling voor JavaScript toe.

### Configuraties toevoegen in integratie

Configuratiewaarden toevoegen in de integratieomgeving Admin. In dit voorbeeld worden JavaScript-bestanden samengevoegd.

1. Meld u af bij de integratie-beheerder.
1. Meld u weer aan bij de integratiebeheerder.
1. Klikken **Winkels** > Instellingen > **Configuratie** > **Geavanceerd** > **Ontwikkelaar**.
1. Vouw in het rechterdeelvenster uit **JavaScript-instellingen**.
1. Van de **JavaScript-bestanden samenvoegen** lijst, klik **Ja**.
1. Klikken **Config opslaan**.
1. Indien gevraagd, [cachegeheugen leegmaken](https://docs.magento.com/user-guide/system/cache-management.html).
1. Afmelden bij de beheerder.

Door het dumpbevel opnieuw in werking te stellen, wordt de nieuwe configuratie toegevoegd aan het dossier.

```bash
magento-cloud db:dump
```

### config.php bewerken met nieuwe instellingen

Op uw lokale computer gebruikt u een teksteditor om de bijgewerkte `app/etc/config.php` bestand. Bewerk deze instellingen om miniaturen voor JavaScript-, HTML- en CSS-bestanden in te schakelen.

```php?start_inline=1
 'dev' => [
     'template' => [
         'allow_symlink' => '0',
         'minify_html' => '0',
     ],

     ... more ...

     'js' => [
         'merge_files' => '0',
         'enable_js_bundling' => '0',
         'minify_files' => '0',
     ],
     'css' => [
         'merge_css_files' => '0',
         'minify_files' => '0',
     ],
```

Als u instellingen wilt wijzigen om miniaturen toe te staan, bewerkt u `'0'` tot `'1'` for `'minify_html'` en elk `'minify_files'` optie:

```php?start_inline=1
 'dev' => [
     'template' => [
         'allow_symlink' => '0',
         'minify_html' => '1',
     ],

     ... more ...

     'js' => [
         'merge_files' => '0',
         'enable_js_bundling' => '0',
         'minify_files' => '1',
     ],
     'css' => [
         'merge_css_files' => '0',
         'minify_files' => '1',
     ],
```

Sla de wijzigingen in het bestand op.

### De wijzigingen in Git duwen

Voer het volgende in om uw wijzigingen door te voeren:

```bash
git add app/etc/config.php
```

```bash
git commit -m "Add system-specific configuration and edit settings"
```

```bash
git push origin master
```

Wacht tot de implementatie is voltooid.

Herhaal het implementatieproces om de code naar alle omgevingen te verplaatsen.
