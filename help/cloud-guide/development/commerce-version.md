---
title: Versie voor upgradeopdracht
description: Leer hoe u de Adobe Commerce-versie kunt upgraden in het cloud-infrastructuurproject.
feature: Cloud, Upgrade
exl-id: 87821007-4979-4a20-940b-aa3c82c192d8
source-git-commit: 745a9f08353bd5dfbb871ca88947157c145c7c70
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 0%

---

# Versie voor upgradeopdracht

U kunt de Adobe Commerce-codebasis upgraden naar een nieuwere versie. Voordat u uw project upgradet, moet u de [Systeemvereisten](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) in de _Installatie_ handleiding voor de meest recente vereisten voor softwareversies.

Afhankelijk van uw projectconfiguratie, kunnen uw verbeteringstaken het volgende omvatten:

- Werk services bij, bijvoorbeeld MariaDB (MySQL), OpenSearch, RabbitMQ en Redis, voor compatibiliteit met nieuwe Adobe Commerce-versies.
- Converteer een ouder configuratiebeheerbestand.
- Werk de `.magento.app.yaml` bestand met nieuwe instellingen voor haken en omgevingsvariabelen.
- Voer een upgrade uit van externe extensies naar de nieuwste ondersteunde versie.
- Werk de `.gitignore` bestand.

{{upgrade-tip}}

{{pro-update-service}}

## Upgrade uitvoeren vanaf oudere versies

Als u een upgrade start vanaf een versie van Commerce die ouder is dan versie 2.1, kunnen sommige beperkingen in de Adobe Commerce-codebasis van invloed zijn op de mogelijkheid om _update_ naar een specifieke ECE-Tools-versie of naar _upgrade_ naar de volgende ondersteunde handelsversie. Gebruik de volgende tabel om het beste pad te bepalen:

| Huidige versie | Upgradepad |
| ----------------- | ------------ |
| 2.1.3 en eerdere versies | Upgrade Adobe Commerce naar versie 2.1.4 of hoger voordat u verdergaat. Voer vervolgens een [eenmalige upgrade voor de installatie van ECE-tools](../dev-tools/install-package.md). |
| 2.1.4 - 2.1.14 | [ECE-gereedschappen bijwerken](../dev-tools/update-package.md) pakket.<br>Zie opmerkingen bij de release voor [2002,0,9](../release-notes/cloud-release-archive.md#v200209) en hoger versies van 2002.0.x. |
| 2.1.15 - 2.1.16 | [ECE-gereedschappen bijwerken](../dev-tools/update-package.md) pakket.<br>Zie opmerkingen bij de release voor[2002,0,9](../release-notes/cloud-release-archive.md#v200209) en later. |
| 2.2.x en hoger | [ECE-gereedschappen bijwerken](../dev-tools/update-package.md) pakket.<br>Zie opmerkingen bij de release voor[2002,0,8](../release-notes/cloud-release-archive.md#v200208) en later. |

{style="table-layout:auto"}

{{ece-tools-package}}

## Configuratiebeheer

Oudere versies van Adobe Commerce, zoals 2.1.4 of hoger naar 2.2.x of hoger, gebruikten een `config.local.php` bestand voor configuratiebeheer. Adobe Commerce versie 2.2.0 en hoger `config.php` bestand, dat precies hetzelfde werkt als het `config.local.php` bestand, maar het heeft andere configuratie-instellingen die een lijst met de ingeschakelde modules en aanvullende configuratieopties bevatten.

Wanneer u een upgrade uitvoert vanaf een oudere versie, moet u de opdracht `config.local.php` bestand gebruiken om nieuwer te gebruiken `config.php` bestand. Gebruik de volgende stappen om een back-up van het configuratiebestand te maken en een bestand te maken.

**Een tijdelijke `config.php` file**:

1. Een kopie maken van `config.local.php` bestand en noem het bestand `config.php`.

1. Dit bestand toevoegen aan de `app/etc` van uw project.

1. Voeg het bestand toe en wijs het toe aan uw vertakking.

1. Verplaats het bestand naar de integratietak.

1. Ga door met het upgradeproces.

>[!WARNING]
>
>Na de upgrade kunt u de `config.php` en een nieuw, volledig bestand genereren. U kunt dit bestand alleen deze keer verwijderen om het te vervangen. Na het genereren van een nieuwe, volledige `config.php` kunt u het bestand niet verwijderen om een nieuw bestand te genereren. Zie [Configuratiebeheer en implementatie van pijpleidingen](../store/store-settings.md).

### Afhankelijkheden van Zend Framework-composer verifiëren

Bij upgrade naar **2.3.x of hoger vanaf 2.2.x**, controleert u of de afhankelijkheden van het Zend Framework zijn toegevoegd aan de `autoload` eigendom van de `composer.json` bestand ter ondersteuning van Laminas. Deze insteekmodule ondersteunt nieuwe vereisten voor het Zend Framework, dat naar het Laminas-project is gemigreerd. Zie [Migratie van Zend Framework naar het Laminas-project](https://community.magento.com/t5/Magento-DevBlog/Migration-of-Zend-Framework-to-the-Laminas-Project/ba-p/443251) op de _Magento DevBlog_.

**Als u de opdracht `auto-load:psr-4` configuratie**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Ontdek je integratietak.

1. Open de `composer.json` in een teksteditor.

1. Controleer de `autoload:psr-4` voor de Zend plugin manager implementatie voor controlemechanismeafhankelijkheid.

   ```json
    "autoload": {
       "psr-4": {
          "Magento\\Framework\\": "lib/internal/Magento/Framework/",
          "Magento\\Setup\\": "setup/src/Magento/Setup/",
          "Magento\\": "app/code/Magento/",
          "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
       },
   }
   ```

1. Als de Zend-afhankelijkheid ontbreekt, werkt u de `composer.json` bestand:

   - Voeg de volgende regel toe aan de `autoload:psr-4` sectie.

     ```json
     "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
     ```

   - Werk de projectgebiedsdelen bij.

     ```bash
     composer update
     ```

   - Wijzigingen in code toevoegen, vastleggen en doorvoeren.

     ```bash
     git add -A
     ```

     ```bash
     git commit -m "Add Zend plugin manager implementation for controllers dependency for Laminas support"
     ```

     ```bash
     git push origin <branch-name>
     ```

   - Voeg de wijzigingen in de Staging-omgeving en vervolgens in Production samen.

## Configuratiebestanden

Voordat u de toepassing kunt upgraden, moet u de projectconfiguratiebestanden bijwerken om rekening te houden met wijzigingen in de standaardconfiguratie-instellingen voor Adobe Commerce op de cloudinfrastructuur of de toepassing. De meest recente standaardwaarden vindt u in het gedeelte [magento-cloud GitHub-opslagplaats](https://github.com/magento/magento-cloud).

### .magento.app.yaml

Controleer altijd de waarden in het dialoogvenster [.magento.app.yaml](../application/configure-app-yaml.md) bestand voor uw geïnstalleerde versie, omdat deze de manier bepaalt waarop uw toepassing wordt gebouwd en geïmplementeerd in de cloudinfrastructuur. Het volgende voorbeeld is voor versie 2.4.6 en gebruikt Composer 2.2.21. De `build: flavor:` eigenschap wordt niet gebruikt voor Composer 2.x; zie [Composer 2 installeren en gebruiken](../application/properties.md#installing-and-using-composer-2).

**Als u het dialoogvenster `.magento.app.yaml` file**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Open en bewerk de `magento.app.yaml` bestand.

1. Werk de PHP-opties bij.

   ```yaml
   type: php:8.2
   
   build:
       flavor: none
   dependencies:
       php:
           composer/composer: '2.2.21'
   ```

1. Wijzig de `hooks` eigenschap `build` en `deploy` opdrachten.

   ```yaml
   hooks:
       # We run build hooks before your application has been packaged.
       build: |
           set -e
           composer install
           php ./vendor/bin/ece-tools run scenario/build/generate.xml
           php ./vendor/bin/ece-tools run scenario/build/transfer.xml
       # We run deploy hook after your application has been deployed and started.
       deploy: |
           php ./vendor/bin/ece-tools run scenario/deploy.xml
       # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
       post_deploy: |
           php ./vendor/bin/ece-tools run scenario/post-deploy.xml
   ```

1. Voeg de volgende omgevingsvariabelen toe aan het einde van het bestand.

   Voor Adobe Commerce 2.2.x tot en met 2.3.x-

   ```yaml
   variables:
       env:
           CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
           CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL: 'Magento_Enterprise_Cloud_BT'
           CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
   ```

   Voor Adobe Commerce 2.4.x-

   ```yaml
   variables:
       env:
           CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
           CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
   ```

1. Sla het bestand op. Breng nog geen wijzigingen aan in de externe omgeving.

1. Ga door met het upgradeproces.

### composer.json

Controleer vóór de upgrade altijd of de afhankelijkheden in de `composer.json` zijn compatibel met de Adobe Commerce-versie.

**Als u het dialoogvenster `composer.json` bestand voor Adobe Commerce versie 2.4.4 en hoger**:

1. Voeg het volgende toe `allow-plugins` aan de `config` sectie:

   ```json
   "config": {
      "allow-plugins": {
         "dealerdirect/phpcodesniffer-composer-installer": true,
         "laminas/laminas-dependency-plugin": true,
         "magento/*": true
      }
   },
   ```

1. Voeg de volgende plug-in toe aan de `require` sectie:

   ```json
   "require": {
       "magento/composer-root-update-plugin": "^2.0.3"
   },
   ```

1. Voeg de volgende component aan toe `extra:component_paths` sectie:

   ```json
   "extra": {
      "component_paths": {
         "tinymce/tinymce": "lib/web/tiny_mce_5"
      },
   },
   ```

1. Sla het bestand op. Wijzig de vertakking nog niet en duw er nog niet op.

1. Ga door met het upgradeproces.

## Projectback-up

We raden u aan een back-up van uw project te maken voordat u de upgrade uitvoert. Gebruik de volgende stappen om een back-up te maken van uw integratie-, staging- en productieomgevingen.

**Een back-up maken van de database en code van uw integratieomgeving**:

1. Maak een lokale back-up van de externe database.

   ```bash
   magento-cloud db:dump
   ```

   >[!NOTE]
   >
   >De `magento-cloud db:dump` bevel stelt het bevel in werking [mysqldump](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) gebruiken met de `--single-transaction` markering, die u aan file uw gegevensbestand toestaat zonder de lijsten te sluiten.

1. Maak een back-up van code en media.

   ```bash
   php bin/magento setup:backup --code [--media]
   ```

   U kunt desgewenst weglaten `[--media]` als u een groot aantal statische dossiers hebt die reeds in broncontrole zijn.

**Om een back-up te maken van uw milieu-database voor Staging of Productie voordat u deze implementeert**:

1. Gebruik SSH om u aan te melden bij de externe omgeving.

1. Een [databasedruk](../storage/database-dump.md). Om een doelfolder voor de stortplaats van DB te kiezen, gebruik `--dump-directory` -optie.

   ```bash
   vendor/bin/ece-tools db-dump
   ```

   De stortplaatsverrichting leidt tot een `dump-<timestamp>.sql.gz` archiefbestand in uw externe projectmap. Zie [Back-up van database maken](../storage/database-dump.md).

## Toepassingsupgrade

Controleer de [serviceversies](../services/services-yaml.md#service-versions) informatie voor de meest recente vereisten voor softwareversies voordat u uw toepassing upgradet.

**De toepassingsversie upgraden**:

1. Wijzig op uw lokale werkstation de projectmap.

1. De upgradeversie instellen met de [syntaxis voor versiebeperking](overview.md#cloud-metapackage).

   ```bash
   composer require "magento/magento-cloud-metapackage":">=CURRENT_VERSION <NEXT_VERSION" --no-update
   ```

   >[!NOTE]
   >
   >U moet de syntaxis van de versiebeperking gebruiken om de `ece-tools` pakket. U kunt de versiebeperking vinden in de `composer.json` bestand voor de versie van het [toepassingssjabloon](https://github.com/magento/magento-cloud/blob/master/composer.json) u gebruikt voor de upgrade.

1. Werk het project bij.

   ```bash
   composer update
   ```

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Upgrade"
   ```

   ```bash
   git push origin <branch-name>
   ```

   `git add -A` is vereist om alle veranderde dossiers aan broncontrole wegens de manier toe te voegen Composer basispakketten marshals. Beide `composer install` en `composer update` marshal-bestanden uit het basispakket (`magento/magento2-base` en `magento/magento2-ee-base`) in de hoofdmap van het pakket.

   De bestanden die Composer marshals hebben, horen bij de nieuwe versie van Adobe Commerce, om de verouderde versie van dezelfde bestanden te overschrijven. Op dit moment is het rangschikken in Adobe Commerce uitgeschakeld, dus u moet de gemarcheerde bestanden toevoegen aan bronbesturing.

1. Wacht tot de implementatie is voltooid.

1. Verifieer de verbetering in uw Integratie, het Staging, of milieu van de Productie door SSH te gebruiken om login en de versie te controleren.

   ```bash
   php bin/magento --version
   ```

### Een bestand config.php maken

Zoals vermeld in [Configuratiebeheer](#configuration-management), na de upgrade moet u een bijgewerkte `config.php` bestand. Voltooi eventuele aanvullende configuratiewijzigingen via de beheerfunctie in uw integratieomgeving.

**Een systeemspecifiek configuratiebestand maken**:

1. Van de terminal, gebruik een bevel van SSH om te produceren `/app/etc/config.php` bestand voor de omgeving.

   ```bash
   ssh <SSH-URL> "<Command>"
   ```

   Bijvoorbeeld voor Pro, om `scd-dump` op de `integration` vertakking:

   ```bash
   ssh <project-id-integration>@ssh.us.magentosite.cloud "php vendor/bin/ece-tools config:dump"
   ```

1. Breng de `config.php` bestand naar uw lokale werkstations met `rsync` of `scp`. U kunt dit bestand alleen lokaal aan de vertakking toevoegen.

   ```bash
   rsync <SSH-URL>:app/etc/config.php ./app/etc/config.php
   ```

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add app/etc/config.php && git commit -m "Add system-specific configuration" && git push origin master
   ```

   Hiermee wordt een bijgewerkte versie gegenereerd `/app/etc/config.php` bestand met een modulelijst en configuratie-instellingen.

>[!WARNING]
>
>Voor een upgrade verwijdert u het dialoogvenster `config.php` bestand. Nadat dit bestand aan de code is toegevoegd, moet u **niet** verwijderen. Als u instellingen moet verwijderen of bewerken, bewerkt u het bestand handmatig.

### Extensies upgraden

Bekijk de extensie- en modulepagina&#39;s van derden in Marketplace of andere bedrijfssites en controleer de ondersteuning voor Adobe Commerce en Adobe Commerce op cloudinfrastructuur. Als u extensies en modules van derden moet bijwerken, raadt de Adobe aan te werken in een nieuwe integratievertakking met uw extensies uitgeschakeld.

**Uw extensies verifiëren en upgraden**:

1. Maak een vertakking op uw lokale werkstation.

1. Schakel de extensies desgewenst uit.

1. Indien beschikbaar, downloadextensies voor upgrades.

1. Installeer de upgrade zoals wordt beschreven in de documentatie van derden.

1. Schakel de extensie in en test deze.

1. Voeg de wijzigingen aan de externe code toe, wijs deze aan en duw erop.

1. Zet uw integratieomgeving aan en test deze.

1. Druk op de testomgeving om te testen in een pre-productieomgeving.

Adobe beveelt ten zeerste aan uw productieomgeving te upgraden _voor_ inclusief de bijgewerkte extensies in het startproces van uw site.

>[!NOTE]
>
>Wanneer u uw toepassingsversie verbetert, werkt het verbeteringsproces aan de recentste versie van het [Fastly CDN-module](../cdn/fastly.md#fastly-cdn-module-for-magento-2) automatisch.

## Upgrade problemen oplossen

Als de upgrade is mislukt, ontvangt u een foutbericht in de browser waarin wordt aangegeven dat u geen toegang hebt tot uw winkel of het deelvenster Beheer:

```terminal
There has been an error processing your request
Exception printing is disabled by default for security reasons.
  Error log record number: <error-number>
```

**De fout oplossen**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Gebruik SSH om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Open de `./app/var/report/<error number>` bestand.

1. [De logboeken controleren](../test/log-locations.md) en bepaalt u de bron van de uitgave.

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add -A && git commit -m "Fixed deployment failure" && git push origin <branch-name>
   ```
