---
title: Extensies beheren
description: Leer extensies installeren en beheren in Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Extensions, Upgrade
exl-id: 9c6e98ca-85da-4342-8402-d576eb382ba2
source-git-commit: f8fb9d4d43c85f91ff87686160bcddb7cd417635
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Extensies beheren

U kunt de mogelijkheden van uw Adobe Commerce-toepassing uitbreiden door een extensie toe te voegen via het [Commerce Marketplace](https://marketplace.magento.com). U kunt bijvoorbeeld een thema toevoegen om de vormgeving van uw winkel te wijzigen of u kunt een taalpakket toevoegen om uw winkel en Admin te lokaliseren.

>[!NOTE]
>
>Om installatiekwesties te voorkomen, moeten alle aankopen van Marketplace worden voltooid met dezelfde account (MAGEID) als die eigenaar is van het cloudproject.

## Composernaam van een extensie

Hoewel in deze sectie wordt besproken hoe u de Composer-naam en -versie van een extensie kunt ophalen vanuit de Commerce Marketplace, kunt u de naam en versie van _alle_ in het Composer-bestand van de module. Open de `composer.json` in een teksteditor en noteer de `"name"` en `"version"` waarden.

**De Composer-naam van een module ophalen uit de Commerce Marketplace**:

1. Aanmelden bij [Commerce Marketplace](https://marketplace.magento.com) met de gebruikersnaam en het wachtwoord waarmee u de component hebt aangeschaft.

1. Klik in de rechterbovenhoek op uw gebruikersnaam en selecteer **Mijn profiel**.

   ![Toegang tot uw Marketplace-account](../../assets/marketplace/my-profile.png)

1. Op de _Mijn account_ pagina, klikt u **Mijn aankopen**.

   ![Aankoopgeschiedenis van Marketplace](../../assets/marketplace/my-purchases.png)

1. Op de _Mijn aankopen_ pagina, selecteert u een module die u hebt aangeschaft en klikt u op **Technische details**.

1. Klikken **Kopiëren** om de [!UICONTROL Component name] naar het klembord.

1. Open een teksteditor en plak de componentnaam en voeg een dubbele punt toe (`:`).

1. In **Technische details**, klikt u op **Kopiëren** om de [!UICONTROL Component version] naar het klembord.

1. Voeg in de teksteditor het versienummer toe aan de componentnaam na de dubbele punt. Bijvoorbeeld:

   ```text
   extension-name/magento2:1.0.1
   ```

## Een extensie installeren

Adobe raadt u aan in een ontwikkelingsvertakking te werken wanneer u een extensie toevoegt aan uw implementatie. Wanneer u een extensie installeert, wordt de extensienaam (`<VendorName>_<ComponentName>`) wordt automatisch ingevoegd in het dialoogvenster [`app/etc/config.php`](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/deployment-files.html) bestand. U hoeft het bestand niet rechtstreeks te bewerken.

**Een extensie installeren**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Maak of check een ontwikkelingsvertakking uit. Zie [vertakking](../development/cli-branches.md).

1. Voeg de extensie met de naam en versie van de Composer toe aan de `require` van de `composer.json` bestand.

   ```bash
   composer require <extension-name>:<version> --no-update
   ```

1. Werk de projectgebiedsdelen bij.

   ```bash
   composer update
   ```

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Install <extension-name>"
   ```

   ```bash
   git push origin <branch-name>
   ```

   >[!WARNING]
   >
   >Wanneer u een extensie installeert, moet u de opdracht `composer.lock` bestand als u code wijzigt in de externe omgeving. De `composer install` de opdracht leest `composer.lock` bestand om de gedefinieerde afhankelijkheden in de externe omgeving in te schakelen.

1. Nadat de build en implementatie is voltooid, gebruikt u een SSH om u aan te melden bij de externe omgeving en om de geïnstalleerde extensie te controleren.

   ```bash
   bin/magento module:status <extension-name>
   ```

   De extensienaam gebruikt de indeling: `<VendorName>_<ComponentName>`.

   Monsterrespons:

   ```terminal
   Module is enabled
   ```

   Als u plaatsingsfouten ontmoet, zie [implementatiefout extensie](../deploy/recover-failed-deployment.md).

## Extensies beheren

Wanneer u een uitbreiding gebruikend Composer toevoegt, laat het plaatsingsproces automatisch de uitbreiding toe. Als u reeds de uitbreiding hebt geïnstalleerd, kunt u de uitbreiding toelaten of onbruikbaar maken gebruikend CLI. Gebruik de indeling bij het beheren van extensies: `<VendorName>_<ComponentName>`

Schakel een extensie nooit in of uit wanneer u bent aangemeld bij de externe omgevingen.

**Een extensie in- of uitschakelen**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Een module in- of uitschakelen. De `module` de opdracht werkt de `config.php` bestand met de gewenste status van de module.

   >Een module inschakelen.

   ```bash
   bin/magento module:enable <module-name>
   ```

   >Een module uitschakelen.

   ```bash
   bin/magento module:disable <module-name>
   ```

1. Als u een module hebt ingeschakeld, gebruikt u `ece-tools` om de configuratie te vernieuwen.

   ```bash
   ./vendor/bin/ece-tools module:refresh
   ```

1. Controleer de status van een module.

   ```bash
   bin/magento module:status <module-name>
   ```

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Disable <extension-name>"
   ```

   ```bash
   git push origin <branch-names>
   ```

## Een extensie upgraden

Voordat u verdergaat, hebt u de naam en de versie van de Composer nodig voor de extensie. Controleer ook of de extensie compatibel is met uw project en de Adobe Commerce-versie. Met name: [de vereiste PHP-versie controleren](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) voordat u begint.

**Een extensie bijwerken**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Maak of check een ontwikkelingsvertakking uit. Zie [vertakking](../development/cli-branches.md).

1. Open de `composer.json` in een teksteditor.

1. Zoek de extensie en werk de versie bij.

1. Sla de wijzigingen op en sluit de teksteditor af.

1. Werk de projectgebiedsdelen bij.

   ```bash
   composer update
   ```

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Update <extension-name>"
   ```

   ```bash
   git push origin <branch-names>
   ```

Als u fouten tegenkomt, raadpleegt u [Herstellen van componentfout](../deploy/recover-failed-deployment.md). Ga voor meer informatie over het gebruik van extensies met Adobe Commerce naar [Extensies](https://experienceleague.adobe.com/docs/commerce-admin/start/resources/extensions.html) in de _Beheerdershandleiding_.
