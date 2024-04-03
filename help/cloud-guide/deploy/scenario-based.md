---
title: Implementatie op basis van scenario's
description: Leer hoe u Adobe Commerce kunt aanpassen bij de implementatie van cloudinfrastructuren met behulp van aangepaste configuratiebestanden.
feature: Cloud, Configuration, Deploy, Build
exl-id: df243068-c7a3-46dd-abe9-9e05198fa343
source-git-commit: 9b3772cf640ebc56063434e1aa8acb1ec51dc63c
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---

# Implementatie op basis van scenario&#39;s

Met `ece-tools` 2002.1.0 en later, kunt u de op scenario-gebaseerde plaatsingseigenschap gebruiken om het standaardplaatsingsgedrag aan te passen.
Deze functie gebruikt **scenario&#39;s** en **stappen** in de configuratie:

- **Scenario-configuratie**- Elke plaatsingshaak is a *scenario* Dit is een XML-configuratiebestand dat de volgorde en configuratieparameters beschrijft voor het uitvoeren van implementatietaken. U vormt de scenario&#39;s in `hooks` van de `.magento.app.yaml` bestand.

- **Stapconfiguratie**- Elk scenario gebruikt een opeenvolging van *stappen* die programmatically de verrichtingen beschrijven die worden vereist om plaatsingstaken te voltooien. U vormt de stappen in een op XML-Gebaseerd dossier van de scenarioconfiguratie.

Adobe Commerce on cloud Infrastructure biedt een set [standaardscenario&#39;s](https://github.com/magento/ece-tools/tree/2002.1/scenario) en [standaardstappen](https://github.com/magento/ece-tools/tree/2002.1/src/Step) in de `ece-tools` pakket. U kunt plaatsingsgedrag aanpassen door de configuratiedossiers van douaneXML te creëren om de standaardconfiguratie met voeten te treden of aan te passen. U kunt ook scenario&#39;s en stappen gebruiken om code uit aangepaste modules uit te voeren.

## Voeg scenario&#39;s toe gebruikend bouw en opstellings haken

U voegt de scenario&#39;s voor het bouwen en het opstellen van Adobe Commerce aan toe `hooks` van de `.magento.app.yaml` bestand. Elke haak specificeert de scenario&#39;s om tijdens elke fase te lopen. Het volgende voorbeeld toont de standaardscenario configuratie.

> `magento.app.yaml` haken

```yaml
hooks:
    build: |
        set -e
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    deploy: |
        php ./vendor/bin/ece-tools run scenario/deploy.xml
    post_deploy: |
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
```

>[!NOTE]
>
>Met de release van `ece-tools` 2002.1.x, er is een nieuwe [hakenconfiguratie](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/app/properties/hooks-property.html) gebruiken. De oudere indeling van `ece-tools` 2002.0.x-releases worden nog steeds ondersteund. Nochtans, moet u aan het nieuwe formaat bijwerken om de op scenario-gebaseerde plaatsingseigenschap te gebruiken.

## Evaluatiescenario-stappen

In de hakconfiguratie, is elk scenario een dossier van XML dat stappen bevat om bouwt, op te stellen, of post-stelt taken in werking te stellen. Bijvoorbeeld de `scenario/transfer` bestand bevat drie stappen: `compress-static-content`, `clear-init-directory`, en `backup-data`

> `scenario/transfer.xml`

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
    <step name="compress-static-content" type="Magento\MagentoCloud\Step\Build\CompressStaticContent" priority="100"/>
    <step name="clear-init-directory" type="Magento\MagentoCloud\Step\Build\ClearInitDirectory" priority="200"/>
    <step name="backup-data" type="Magento\MagentoCloud\Step\Build\BackupData" priority="300">
        <arguments>
            <argument name="logger" xsi:type="object">Psr\Log\LoggerInterface</argument>
            <argument name="steps" xsi:type="array">
                <item name="static-content" xsi:type="object" priority="100">Magento\MagentoCloud\Step\Build\BackupData\StaticContent</item>
                <item name="writable-dirs" xsi:type="object"  priority="200">Magento\MagentoCloud\Step\Build\BackupData\WritableDirectories</item>
            </argument>
        </arguments>
    </step>
</scenario>
```

## Een standaardscenario uitbreiden

Het volgende voorbeeld breidt het gebrek uit stelt scenario door extra op te nemen configuratiedossiers aan de hakenconfiguratie toe te voegen.

```yaml
hooks:
  deploy: |
    php ./vendor/bin/ece-tools run scenario/deploy.xml vendor/<vendor-name>/<module-name>/deploy.xml vendor/<vendor-name>/<module-name>/deploy2.xml
```

Tijdens plaatsing, voegen de douanescenario&#39;s met standaard scenario-gebaseerd op de volgende regels samen:

- De scenario&#39;s worden voorrang gegeven aan gebaseerd op hun opeenvolging in de hakdefinitie met het laatste vermelde scenario dat de hoogste prioriteit heeft.

  In het voorbeeld hebben de scenario&#39;s de volgende prioriteit:

   1. `vendor/vendor-name/module-name/deploy2.xml`
   1. `vendor/vendor-name/module-name/deploy.xml`
   1. `scenario/deploy.xml` (standaard- of basislijnscenario)

- De stappen in het hoogste prioritaire scenario treden stappen met de zelfde naam in de andere scenario&#39;s met voeten. Nieuwe stappen worden toegevoegd aan de configuratie. Dezelfde regels gelden voor meer dan twee scenario&#39;s waarbij elk scenario van rechts naar links voorrang krijgt, bijvoorbeeld (C → B → A).

### Standaardstappen verwijderen

U verwijdert stappen uit standaardscenario&#39;s gebruikend `skip` parameter.

Als u bijvoorbeeld het dialoogvenster `enable-maintenance-mode` en `set-production-mode` de stappen in het gebrek stellen scenario, leiden tot een configuratiedossier dat de volgende configuratie omvat.

> `vendor/vendor-name/module-name/deploy-custom-mode-config.xml`

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
    <step name="enable-maintenance-mode" skip="true" />
    <step name="set-production-mode"  skip="true" />
</scenario>
```

Als u het aangepaste configuratiebestand wilt gebruiken, werkt u het standaardbestand bij `.magento.app.yaml` bestand.

> `.magento.app.yaml` met een aangepast implementatiescenario

```yaml
hooks:
    build: |
        set -e
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    deploy: |
        php ./vendor/bin/ece-tools run scenario/deploy.xml vendor/vendor-name/module-name/deploy-custom-mode-config.xml
    post_deploy: |
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
```

### Standaardstappen vervangen

De scenario&#39;s van de douane kunnen standaardstappen vervangen om douaneimplementatie te verstrekken. Hiervoor gebruikt u de standaardnaam voor de stap als naam voor de aangepaste stap.

In het dialoogvenster [standaard implementatiescenario] de `enable-maintenance-mode` stap voert het gebrek uit [EnableMaintenanceMode PHP-script].

```xml
<step name="enable-maintenance-mode" type="Magento\MagentoCloud\Step\EnableMaintenanceMode" priority="300"/>
```

Als u deze stap wilt overschrijven, maakt u een aangepast scenario-configuratiebestand om een ander script uit te voeren wanneer de `enable-maintenance-mode` stap-uitvoering.

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
<scenario>
    <step name="enable-maintenance-mode" type="VendorName\VendorModule\Step\CustomEnableMaintenanceMode" priority="300"/>
</scenario>
```

### De prioriteit van de stap wijzigen

De scenario&#39;s van de douane kunnen de prioriteit van standaardstappen veranderen. In de volgende stap wordt de prioriteit van de `enable-maintenance-mode` stap van `300` tot `10` zodat de stap vroeger in stelt scenario in werking.

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
<scenario>
    <step name="enable-maintenance-mode" type="Magento\MagentoCloud\Step\EnableMaintenanceMode" priority="10"/>
</scenario>
```

In dit voorbeeld wordt `enable-maintenance-mode` De stappen bewegen zich aan het begin van het scenario omdat het een lagere prioriteit heeft dan alle andere stappen in het gebrek stelt scenario op.

### Voorbeeld: het implementatiescenario uitbreiden

In het volgende voorbeeld worden de [standaard implementatiescenario] met de volgende wijzigingen:

- Vervangt de `remove-deploy-failed-flag` stap met een aangepaste stap
- Hiermee slaat u de `clean-redis-cache` substap in de pre-implementatiestap
- Hiermee slaat u de `unlock-cron-jobs` stap
- Hiermee slaat u de `validate-config` stap om kritieke validators uit te schakelen
- Voegt een nieuwe pre-implementatiestap toe

> `vendor/vendor-name/module-name/deploy-extended.xml`

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
    <!-- Replace "remove-deploy-failed-flag" step with custom step -->
    <step name="remove-deploy-failed-flag" type="Vendor\ModuleName\Step\Deploy\RemoveDeployFailedFlag" priority="100"/>

    <!-- Skip "clean-redis-cache" sub-step in pre-deploy step -->
    <step name="pre-deploy" type="Magento\MagentoCloud\Step\Deploy\PreDeploy" priority="200">
        <arguments>
            <argument name="logger" xsi:type="object">Psr\Log\LoggerInterface</argument>
            <argument name="steps" xsi:type="array">
                <item name="clean-redis-cache" xsi:type="object" skip="true"/>
            </argument>
        </arguments>
    </step>

    <!-- Skip step "unlock-cron-jobs" -->
    <step name="unlock-cron-jobs" skip="true"/>

    <!-- Skip critical validators -->
    <step name="validate-config" type="Magento\MagentoCloud\Step\ValidateConfiguration" priority="300">
        <arguments>
            <argument name="logger" xsi:type="object">Psr\Log\LoggerInterface</argument>
            <argument name="validators" xsi:type="array">
                <item name="critical" xsi:type="array">
                    <item name="database-configuration" xsi:type="object" skip="true"/>
                    <item name="search-configuration" xsi:type="object" skip="true"/>
                </item>
            </argument>
        </arguments>
    </step>

    <!-- Add new step into the beginning of the deploy scenario -->
    <step name="new-pre-deploy-step" type="Vendor\ModuleName\Step\Deploy\PreDeploy" priority="10"/>
</scenario>
```

Om dit manuscript in uw project te gebruiken, voeg de volgende configuratie aan toe `.magento.app.yaml` bestand voor uw Adobe Commerce-infrastructuurproject in de cloud:

```yaml
hooks:
    build: |
        set -e
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    deploy: |
        php ./vendor/bin/ece-tools run scenario/deploy.xml vendor/vendor-name/module-name/deploy-extended.xml
    post_deploy: |
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
```

>[!TIP]
>
>U kunt de [standaardscenario&#39;s](https://github.com/magento/ece-tools/tree/2002.1/scenario) en [standaardstapconfiguratie](https://github.com/magento/ece-tools/tree/2002.1/src/Step) in de `ece-tools` De bewaarplaats van GitHub om te bepalen welke scenario&#39;s en stappen voor uw project bouwen, opstellen, en post-opstelt taken.

## Een uitgebreide aangepaste module toevoegen `ece-tools`

De `ece-tools` pakket biedt standaard API-interfaces die voldoen aan de normen voor semantische versies. Alle API-interfaces zijn gemarkeerd met **@api** aantekening. U kunt de standaard-API-implementatie vervangen door uw eigen implementatie door een aangepaste module te maken en de standaardcode desgewenst te wijzigen.

Als u de aangepaste module met Adobe Commerce wilt gebruiken op een cloudinfrastructuur, moet u uw module registreren in de lijst met extensies voor het dialoogvenster `ece-tools` pakket. Het registratieproces is vergelijkbaar met het proces dat u gebruikt om modules te registreren in Adobe Commerce.

**Als u een module wilt registreren bij de `ece-tools` package**:

1. Maak of breid de `registration.php` in de hoofdmap van uw module.

   ```php?start_inline=1
   \Magento\MagentoCloud\ExtensionRegistrar::register('module-name', __DIR__);
   ```

1. Werk de `autoload` sectie voor uw dossier van de moduleconfiguratie om te omvatten `registration.php` bestand dat automatisch wordt geladen in modulebestanden in `composer.json`.

   ```json
   {
     "name": "vendor/ece-tools-extend",
     "description": "Extension for ece-tools",
     "type": "magento2-component",
     "version": "1.0.0",
     "license": "OSL-3.0",
     "autoload": {
       "files": [ "registration.php" ],
       "psr-4": {
         "Vendor\\EceToolExtend\\": "src/"
       }
     }
   }
   ```

1. Voeg de `config/services.xml` in uw module. Deze configuratie wordt samengevoegd over `config/services.xml` van `ece-tools` pakket.

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <container xmlns="http://symfony.com/schema/dic/services"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://symfony.com/schema/dic/services https://symfony.com/schema/dic/services/services-1.0.xsd">
       <services>
           <defaults autowire="true" autoconfigure="true" public="true"/>
   
           <prototype namespace="Vendor\EceToolExtend\" resource="../src/*" exclude="../src/{Test}"/>
   
           <!-- Use your own implementation of EnvironmentDataInterface -->
           <service id="Magento\MagentoCloud\Config\EnvironmentDataInterface" alias="Vendor\EceToolExtend\Config\CustomEnvironmentData" />
       </services>
   </container>
   ```

Voor meer informatie over afhankelijkheidsinjectie raadpleegt u [Symfony Dependency Injection](https://symfony.com/doc/current/components/dependency_injection.html).

<!-- link definitions -->

[standaard implementatiescenario]: https://github.com/magento/ece-tools/blob/develop/scenario/deploy.xml
[EnableMaintenanceMode PHP-script]: https://github.com/magento/ece-tools/blob/develop/src/Step/EnableMaintenanceMode.php
