---
title: Patches toepassen
description: Leer hoe u patches in de Adobe Commerce kunt toepassen op een cloudinfrastructuurproject.
feature: Cloud, Upgrade
exl-id: a7bf672f-7b89-45cd-8436-e885bca9029d
source-git-commit: e67d3259b1b5195147e4e441fe9efd82e48241ab
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---

# Patches toepassen

[Cloud-patches voor handel](https://github.com/magento/magento-cloud-patches) en de [Gereedschap Kwaliteitspatches](https://github.com/magento/quality-patches) patches leveren aan uw geïnstalleerde Adobe Commerce-toepassing.

- Het pakket Cloud Patches for Commerce biedt vereiste patches met kritieke oplossingen
- Kwaliteitspatches bieden optionele oplossingen met een lage kwaliteit zoals [afzonderlijke patches](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/versioning-policy.html#individual-patch) die geen achterwaartse incompatibele wijzigingen bevatten

Zie [Beschikbare patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) in de _Handboek Handelingen_ om een volledige lijst met vrijgegeven patches te bekijken.

Beide pakketten verbeteren de integratie van alle Adobe Commerce-versies met Cloud-omgevingen en ondersteunen snelle levering van kritieke, optionele en aangepaste oplossingen. U kunt deze pakketten gebruiken om algemene informatie over alle afzonderlijke patches die beschikbaar zijn voor Handel toe te passen, terug te draaien en weer te geven.

>[!TIP]
>
>U kunt de [Gereedschap Kwaliteitspatches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) en Cloud Patches for Commerce als zelfstandige pakketten voor Magento Open Source- en Adobe Commerce-projecten. We raden u aan het gereedschap Kwaliteitspatches te gebruiken voor niet-cloud-projecten.

Wanneer u veranderingen in het verre milieu opstelt, `ece-tools` pakketgebruik `magento/magento-cloud-patches` en `magento/quality-patches` om te controleren op in behandeling zijnde patches en deze automatisch toe te passen in de volgende volgorde:

1. Pas alle vereiste Commerce-patches toe die zijn opgenomen in het pakket Cloud Patches for Commerce.
1. Geselecteerde optionele Commerce-patches in het gereedschap Kwaliteitspatches toepassen.
1. Aangepaste patches toepassen in het dialoogvenster `/m2-hotfixes` directory in alfabetische volgorde op flardnaam.

>[!NOTE]
>
>Wanneer u de `ece-tools` het pakket of het pakket van de Patches van de Wolk voor Handel, de recentste vereiste flarden worden toegepast de volgende tijd u uw project opstelt, of u kunt hen onmiddellijk opstellen gebruikend `ece-patches apply` CLI-opdracht en herimplementatie van uw Cloud-omgeving. U kunt niet overslaan [vereiste patches](https://github.com/magento/magento-cloud-patches/tree/develop/patches) tijdens het implementatieproces.

## Vereisten

{{upgrade-tip}}

Het hulpmiddel van de Patches van de Kwaliteit is een afhankelijkheid voor de Patches van de Wolk voor Handel en `ece-tools` pakket. Als u de nieuwste patches wilt toepassen, moet u [de meest recente versie van ECE-Tools](../dev-tools/update-package.md) geïnstalleerd. De minimaal vereiste versie van ECE-Tools is 2002.1.2.

## Beschikbare patches en status weergeven

U kunt als volgt de lijst met beschikbare afzonderlijke patches weergeven:

```bash
php ./vendor/bin/ece-patches status
```

Monsterrespons:

```terminal
More detailed information about patches you can find on https://support.magento.com/
╔════════════════╤═════════════════════════════════════════════════╤══════════╤═════════════╤═════════════════════════════════╗
║ Id             │ Title                                           │ Type     │ Status      │ Details                         ║
╠════════════════╪═════════════════════════════════════════════════╪══════════╪═════════════╪═════════════════════════════════╣
║ MAGECLOUD-5069 │ FPC is getting disabled during deployments      │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-page-cache    ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MCLOUD-5650    │ Hold deployment config after reading from file  │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/framework            ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MCLOUD-5684    │ Pagination Not working - product_list_limit=all │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-elasticsearch ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-65837       │ Fix load balancer issue                         │Deprecated│ Applied     │ Recommended replacement: MC-1   ║
║                │                                                 │          │             │ Affected components:            ║
║                │                                                 │          │             │  - magento/framework            ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ BUNDLE-2554    │ Set Payment info bug                            │ Required │ Not applied │ Affected components:            ║
║                │                                                 │          │             │  - amzn/amazon-pay-module       ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-1           │ Fixes issue 1                                   │ Optional │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-2           │ Fixes issue 2                                   │ Optional │ Not applied │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-3           │ Fixes issue 3                                   │ Optional │ Not applied │ Required patches:               ║
║                │                                                 │          │             │  - MC-2                         ║
║                │                                                 │          │             │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ N/A            │ ../m2-hotfixes/MDVA_custom__2.3.5_ce.patch      │ Custom   │ N/A         │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-framework     ║
╚════════════════╧═════════════════════════════════════════════════╧══════════╧═════════════╧═════════════════════════════════╝
Magento 2 Enterprise Edition, version 2.3.5.0
```

De statustabel bevat de volgende soorten informatie:

- **Type**:
   - `Optional`—Alle patches van het gereedschap Kwaliteitspatches en het pakket Cloudepatches zijn optioneel voor installatie van Adobe Commerce en Magento Open Source. Voor Adobe Commerce op cloud-infrastructuur zijn alle patches optioneel.
   - `Required`—Alle patches uit het pakket Cloud Patches for Commerce zijn vereist voor klanten van de cloud.
   - `Deprecated`—De afzonderlijke pleister is gemarkeerd als afgekeurd en we raden u aan deze weer in te stellen als u deze heeft aangebracht. Nadat u een vervangen patch hebt hersteld, wordt deze niet meer weergegeven in de statustabel.
   - `Custom`—Alle patches uit de map &#39;m2-hotfixes&#39;.

- **Status**:
   - `Applied`—De pleister is aangebracht.
   - `Not applied`—De pleister is niet aangebracht.
   - `N/A`—De status van de patch kan niet worden gedefinieerd vanwege conflicten.

- **Details**:
   - `Affected components`—De lijst van betrokken modules.
   - `Required patches`—De lijst met vereiste patches (afhankelijkheden).
   - `Recommended replacement`—De pleister die een geadviseerde vervanging voor een afgekeurde flard is.

## Een patch toepassen in een lokale omgeving

U kunt patches handmatig toepassen in een lokale omgeving en ze testen voordat u ze implementeert.

**Afzonderlijke patches toepassen in een lokale ontwikkelomgeving**:

1. Voeg de variabele &#39;QUALITY_PATCH&#39; toe aan de `.magento.env.yaml` en vermeld de vereiste patches onderaan.

   ```yaml
   stage:
     build:
       QUALITY_PATCHES:
         - MCTEST-1002
         - MCTEST-1003
   ```

1. Pas de patches toe vanuit de projecthoofdmap.

   ```bash
   php ./vendor/bin/ece-patches apply
   ```

   De `ece-patches apply` past flarden in de volgende orde toe:
   - Vereiste patches
   - Optionele afzonderlijke patches
   - Aangepaste patches van het dialoogvenster `/m2-hotfixes` directory

1. Wis de cache.

   ```bash
   php ./bin/magento cache:clean
   ```

1. Test de patches en breng de benodigde wijzigingen aan in aangepaste patches.

## Een patch toepassen in een externe omgeving

>[!WARNING]
>
>We raden u ten zeerste aan om alle patches in een integratie- of testomgeving te testen voordat u deze implementeert in de productieomgeving.

**Patches toepassen in een externe omgeving**:

1. Voeg de `QUALITY_PATCHES` aan de `.magento.env.yaml` en vermeld de vereiste patches onderaan.

   ```yaml
   stage:
     build:
       QUALITY_PATCHES:
         - MCTEST-1002
         - MCTEST-1003
   ```

   >[!NOTE]
   >
   >Nadat u de upgrade naar een nieuwe versie van Adobe Commerce hebt uitgevoerd, moet u de patches opnieuw toepassen als de patches niet in de nieuwe versie zijn opgenomen.

1. De bijgewerkte versie toevoegen, toewijzen en duwen `.magento.env.yaml` bestand.

   ```bash
   git add .magento.env.yaml
   ```

   ```bash
   git commit -m "Apply patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

## Een aangepaste patch toepassen

Wanneer u opstelt, past ECE-Tools alle patches voor Adoben en aangepaste patches toe die u toevoegt aan de `/m2-hotfixes` directory in de projectwortel.

>[!NOTE]
>
>Alle namen van patchbestanden moeten eindigen op `.patch` extensie.

**Een aangepaste patch toepassen en testen in een Cloud-omgeving**:

1. In de projectwortel, creeer een folder genoemd `m2-hotfixes` indien deze niet bestaat

   ```bash
   mkdir m2-hotfixes
   ```

1. Kopieer het patchbestand naar de `/m2-hotfixes` directory.

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add m2-hotfixes/
   ```

   ```bash
   git commit -m "Apply patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   >[!NOTE]
   >
   >Zorg ervoor dat u alle pleisters test in een pre-productieomgeving. Voor Adobe Commerce op cloudinfrastructuur kunt u vertakkingen maken met de `magento-cloud environment:branch <branch-name>` CLI-opdracht.

## Een aangepaste patch herstellen

Een eerder toegepaste aangepaste patch herstellen of verwijderen:

1. Verwijder het patchbestand uit het dialoogvenster `/m2-hotfixes` directory.

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add m2-hotfixes/
   ```

   ```bash
   git commit -m "Revert patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   >[!NOTE]
   >
   >Zorg ervoor dat u test in een pre-productieomgeving. Voor Adobe Commerce op cloudinfrastructuur kunt u vertakkingen maken met de `magento-cloud environment:branch <branch-name>` CLI-opdracht.

## Patches toepassen op een niet-cloud-project

Gebruik de [Gereedschap Kwaliteitspatches](https://github.com/magento/quality-patches) voor Magento Open Source- en Adobe Commerce-projecten.

## Een patch herstellen in een lokale omgeving

U kunt alle eerder toegepaste patches in een lokale ontwikkelomgeving herstellen met de opdracht `ece-patches` CLI.

Alle toegepaste patches herstellen:

```bash
php ./vendor/bin/ece-patches revert
```

Met deze opdracht worden alle patches in de volgende volgorde teruggezet:

- Keert alle toegepaste douaneflarden van /m2-hotfixes folder om.
- Hiermee worden alle toegepaste optionele afzonderlijke patches omgekeerd.
- Hiermee herstelt u alle toegepaste vereiste patches.

## Logboekregistratie

Met het gereedschap Kwaliteitspatches kunt u alle bewerkingen in de `<Project_root>/var/log/patch.log` bestand.
