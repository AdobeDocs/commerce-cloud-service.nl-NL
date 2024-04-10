---
title: Upgradeproject voor gebruik van ECE-tools
description: Leer hoe u een upgrade uitvoert van uw Adobe Commerce op een cloud-infrastructuurproject, zodat u het pakket ECE-Tools kunt gebruiken en de nieuwste oplossingen en functies kunt benutten.
feature: Cloud, Install
exl-id: 820cca84-2817-4881-829f-ebb78400d8c7
source-git-commit: bcdb59f0d2a17e55e8b0479ee69fac06c710638f
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# Upgradeproject voor gebruik van het pakket ECE-Tools

Adobe heeft de `magento/magento-cloud-configuration` en `magento/ece-patches` pakketten ten gunste van de `ece-tools` pakket, dat veel cloudprocessen vereenvoudigt. Als u een ouder Adobe Commerce gebruikt voor een infrastructuurproject in de cloud _niet_ bevatten `ece-tools` en moet u een eenmalige, handmatige _upgrade_ aan uw project te verwerken.

>[!WARNING]
>
>Als uw project de `ece-tools` kunt u de volgende upgrade overslaan. Om te verifiëren, wint terug [!DNL Commerce] versie die de `php vendor/bin/ece-tools -V` in de lokale hoofdmap van het project.

Voor dit upgradeproces van het project moet u het `magento/magento-cloud-metapackage` versiebeperking in de `composer.json` bestand in de hoofdmap. Met deze beperking kunnen updates voor Adobe Commerce worden uitgevoerd op metapakketten voor cloudinfrastructuur, zoals het verwijderen van verouderde pakketten, zonder dat de huidige Adobe Commerce-versie wordt bijgewerkt.

{{upgrade-tip}}

## Vervangen pakketten verwijderen

Voordat u een upgrade uitvoert, moet u de opdracht `ece-tools` pakket, controleer de `composer.lock` bestand voor de volgende vervangen pakketten:

- `magento/magento-cloud-configuration`
- `magento/ece-patches`

## Het pakket metapakketten bijwerken

Voor elke Adobe Commerce-versie is een andere beperking vereist op basis van het volgende:

```terminal
>=current_version <next_version
```

- Voor `current_version`, geeft u de Adobe Commerce-versie op die u wilt installeren.
- Voor `next_version`geeft u de volgende patchversie op na de waarde die is opgegeven in `current_version`.

Als u Adobe Commerce wilt installeren `2.3.5-p2`, set `current_version` tot `2.3.5` en de `next_version` tot `2.3.6`. De beperking `">=2.3.5 <2.3.6"` Hiermee installeert u het nieuwste beschikbare pakket voor 2.3.5.

U kunt de meest recente metapakketbeperking altijd vinden in het dialoogvenster [`magento-cloud` template](https://github.com/magento/magento-cloud/blob/master/composer.json).

In het volgende voorbeeld wordt een beperking voor het Adobe Commerce-pakket voor de infrastructuur van de cloud geplaatst in elke versie die hoger is dan of gelijk is aan de huidige versie 2.4.7 en lager is dan de volgende versie 2.4.8:

```json
"require": {
    "magento/magento-cloud-metapackage": ">=2.4.7 <2.4.8"
},
```

## Het project upgraden

Om uw project te bevorderen om te gebruiken `ece-tools` moet u het pakket metapakket en de `.magento.app.yaml` Koppelt eigenschappen en voert een Composer-update uit.

**Om project te bevorderen om Griekenland-hulpmiddelen te gebruiken**:

1. Werk de `magento/magento-cloud-metapackage` versiebeperking in de `composer.json` bestand.

   ```bash
   composer require "magento/magento-cloud-metapackage":">=2.4.7 <2.4.8" --no-update
   ```

1. Werk het metapakket bij.

   ```bash
   composer update magento/magento-cloud-metapackage
   ```

1. Wijzig de haakbevelen in `magento.app.yaml` bestand.

   ```yaml
   hooks:
       # We run build hooks before your application has been packaged.
       build: |
           set -e
           php ./vendor/bin/ece-tools run scenario/build/generate.xml
           php ./vendor/bin/ece-tools run scenario/build/transfer.xml
       # We run deploy hook after your application has been deployed and started.
       deploy: |
           php ./vendor/bin/ece-tools run scenario/deploy.xml
       # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
       post_deploy: |
           php ./vendor/bin/ece-tools run scenario/post-deploy.xml
   ```

1. Controleren op en verwijderen de [verouderde pakketten](#remove-deprecated-packages). De vervangen pakketten kunnen een geslaagde upgrade verhinderen.

   ```bash
   composer remove magento/magento-cloud-configuration
   ```

   ```bash
   composer remove magento/ece-patches
   ```

1. Het kan nodig zijn de `ece-tools` pakket.

   ```bash
   composer update magento/ece-tools
   ```

1. Voeg de codewijzigingen toe en wijs deze toe. In dit voorbeeld zijn de volgende bestanden bijgewerkt:

   ```terminal
   .magento.app.yaml
   composer.json
   composer.lock
   ```

1. Verduw uw codeveranderingen in de verre server en voeg deze tak met samen `integration` vertakking.

   ```bash
   git push origin <branch-name>
   ```
