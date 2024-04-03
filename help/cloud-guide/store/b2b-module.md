---
title: De B2B-module inschakelen
description: Leer hoe u de business-to-business module voor Adobe Commerce kunt inschakelen voor cloudinfrastructuur.
feature: Cloud, B2B
exl-id: 01d02ea0-1e7d-4608-adbf-1dad7f5e2182
source-git-commit: bb7a866b1896a8a43d01ad3f83dc655bcf383374
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# De B2B-module inschakelen

Als uw klanten bedrijven zijn, kunt u de B2B voor de module van Adobe Commerce installeren om uw Adobe Commerce op het project van de wolkeninfrastructuur Pro uit te breiden om een zaken-aan-bedrijfsmodel aan te passen. Hoewel dit onderwerp informatie specifiek voor het installeren en het vormen van de B2B module voor Adobe Commerce op wolkeninfrastructuur verstrekt, kunt u extra B2B informatie in de volgende gidsen vinden:

- [Adobe Commerce B2B-ontwikkelaarsgids](https://developer.adobe.com/commerce/webapi/rest/b2b/)
- [Adobe Commerce B2B-gebruikershandleiding](https://experienceleague.adobe.com/docs/commerce-admin/b2b/guide-overview.html)

>[!TIP]
>
>Omdat B2B een module voor Adobe Commerce op wolkeninfrastructuur is, adviseert de Adobe dat u uw toepassing van Adobe Commerce aan een Integratie of het Staging milieu alvorens begint op te stellen.

## B2B-module installeren

De Adobe adviseert werkend in een ontwikkelingstak wanneer het toevoegen van de module B2B aan uw project. Als u geen vertakking hebt, zie [Een vertakking maken voor ontwikkeling](../development/cli-branches.md#create-a-branch-for-development). Wanneer u de B2B-module installeert, `Magento_B2b` modulenaam wordt automatisch ingevoegd in het dialoogvenster `app/etc/config.php` bestand. U hoeft het bestand niet rechtstreeks te bewerken.

**De B2B-module installeren**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Maak of check een ontwikkelingsvertakking uit.

1. Voeg de B2B-module toe aan de `require` van de `composer.json` bestand.

   ```bash
   composer require magento/extension-b2b --no-update
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
   git commit -m "Install the B2B module."
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Nadat de bouw en de opstelling eindigt, gebruik SSH aan login aan het verre milieu en verifieer dat de B2B module geïnstalleerd is.

   ```bash
   bin/magento module:status Magento_B2b
   ```

   De extensienaam gebruikt de indeling: `<VendorName>_<ComponentName>`.

   Monsterrespons:

   ```terminal
   Magento_B2b : Module is enabled
   ```

   Als u plaatsingsfouten ontmoet, zie [Herstellen van componentfout](../deploy/recover-failed-deployment.md).

## De B2B-module inschakelen

Wanneer u de module B2B gebruikend Composer installeert, laat het plaatsingsproces automatisch de module toe. Als u reeds de B2B module hebt geïnstalleerd, kunt u de module toelaten of onbruikbaar maken gebruikend CLI

De B2B-module inschakelen:

```bash
bin/magento module:enable Magento_B2b
```

Monsterrespons:

```terminal
The following modules have been enabled:
- Magento_B2b

Cache cleared successfully.
Generated classes cleared successfully. Please run the 'setup:di:compile' command to generate classes.
Info: Some modules might require static view files to be cleared. To do this, run 'module:enable' with the --clear-static-content option to clear them.
```

Zie [Extensies beheren](extensions.md).

## De B2B-module configureren

Nadat u de B2B-module voor Adobe Commerce hebt geïnstalleerd, moet u [de boodschap van de consument beginnen](https://experienceleague.adobe.com/docs/commerce-admin/b2b/install.html#start-message-consumers) zodat u de _Gedeelde catalogus_ en u moet [de B2B-functies inschakelen](https://experienceleague.adobe.com/docs/commerce-admin/b2b/enable-basic-features.html).
