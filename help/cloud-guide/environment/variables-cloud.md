---
title: Cloudspecifieke variabelen
description: Zie een lijst met omgevingsvariabelen die specifiek zijn voor Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Configuration
recommendations: noDisplay, catalog
role: Developer
exl-id: 84b7c0fc-f0b0-4ff5-9f33-9d17180a9306
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Cloudspecifieke variabelen

Omgevingsvariabelen die specifiek zijn voor Adobe Commerce op cloudinfrastructuur gebruiken de `MAGENTO_CLOUD_*` prefix:

| Variabele | Beschrijving |
| -------- | --------------- |
| `MAGENTO_CLOUD_APP_DIR` | Het absolute pad naar de toepassingsmap. |
| `MAGENTO_CLOUD_APPLICATION` | Een basis64-gecodeerd JSON-object dat de toepassing beschrijft. Het is toegewezen aan de `.magento.app.yaml` bestandsinhoud en heeft subsleutels. |
| `MAGENTO_CLOUD_APPLICATION_NAME` | De naam van de toepassing die in het dialoogvenster `.magento.app.yaml` bestand. |
| `MAGENTO_CLOUD_DOCUMENT_ROOT` | Het absolute pad naar de hoofdmap van het webdocument, indien van toepassing. |
| `MAGENTO_CLOUD_ENVIRONMENT` | De naam van de omgevingsvertakking. |
| `MAGENTO_CLOUD_PROJECT` | De project-id. |
| `MAGENTO_CLOUD_RELATIONSHIPS` | Een base64-gecodeerd JSON-object dat de definitie van het eindpunt van een key (relatienaam) en value (arrays of relationship pairs) vertegenwoordigt. Elke definitie van het relatieeindpunt is een ontlede vorm van een URL. Het heeft een `scheme`, `host`, `port`, en _optioneel_ a `username`, `password`, `path`en aanvullende informatie in `query`. |
| `MAGENTO_CLOUD_ROUTES` | Beschrijf de routes die in het milieu worden bepaald `.magento/routes.yaml` bestand. |
| `MAGENTO_CLOUD_TREE_ID` | De boom-id voor de toepassing, die overeenkomt met de SHA van de boomstructuur in Git. |
| `MAGENTO_CLOUD_VARIABLES` | Een basis64-gecodeerd JSON-object met sleutel-waardeparen, zoals `"key":"value"`. |
| `MAGENTO_CLOUD_LOCKS_DIR` | Verstrekt de weg aan het onderstelpunt voor de slotleverancier op de infrastructuur van de Wolk. De vergrendelingsprovider voorkomt het starten van dubbele snijtaken en afdekgroepen. |

>[!WARNING]
>
>Omgevingsvariabelen toevoegen aan [configuratie-instellingen overschrijven](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/override-config-settings.html) met de [[!DNL Cloud Console]](../project/overview.md), moet u de variabelenaam vooraf aan `env:` zoals in het volgende voorbeeld:
>
>![Voorbeeld van de variabele Environment](../../assets/set-env-variable-ui.png)

Aangezien de waarden in de loop der tijd kunnen veranderen, is het best om de variabele bij runtime te inspecteren en het te gebruiken om uw toepassing te vormen. Gebruik bijvoorbeeld de opdracht `MAGENTO_CLOUD_RELATIONSHIPS` variabele voor het ophalen van relaties met betrekking tot het milieu, als volgt:

```php
<?php
/**
  * Get relationships information from cloud environment variable.
  *
  * @return mixed
  */
    protected function getRelationships()
    {
        return json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]), true);
    }
```

## Omgevingsvariabelen weergeven

U kunt de `env:config:show` opdracht van [de `ece-tools` package](../dev-tools/package-overview.md) om een lijst met variabelen voor de huidige omgeving weer te geven.

```bash
php ./vendor/bin/ece-tools env:config:show variables
```

Voorbeelduitvoer voor de `variables` optie:

```terminal
Magento Cloud Environment Variables:
+-----------------------------------+----------------------------------+
| Variable name                     | Value                            |
+-----------------------------------+----------------------------------+
| ADMIN_EMAIL                       | commerceadmin@company.com        |
| ADMIN_PASSWORD                    | 123123q                          |
+-----------------------------------+----------------------------------+
```
