---
title: Niveaus en opties van variabele
description: Leer meer over de verschillende niveaus en opties die worden gebruikt voor het aanpassen van uw Adobe Commerce in de runtimeomgeving van een cloudinfrastructuurproject.
feature: Cloud, Configuration, Security
exl-id: 11aa0862-94c0-47fb-946a-0148f75cc24c
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# Variabele niveaus

De variabelen van het project zijn op alle milieu&#39;s binnen het project van toepassing. Omgevingsvariabelen zijn van toepassing op een specifieke omgeving of vertakking. Een omgeving _overerven_ variabele definities van de bovenliggende omgeving.

U kunt een overgeërfde waarde met voeten treden door de variabele specifiek voor het milieu te bepalen. Als u bijvoorbeeld variabelen voor ontwikkeling wilt instellen, definieert u de variabelewaarden in het dialoogvenster `.magento.env.yaml` in de integratieomgeving. Alle omgevingen die vertakkingen ondervinden van de integratieomgeving nemen deze waarden over. Zie [Implementatieconfiguratie](configure-env-yaml.md) voor meer informatie over het configureren van uw omgeving met behulp van `.magento.env.yaml` bestand.

>[!BEGINTABS]

>[!TAB CLI]

**Variabelen instellen met de Cloud CLI**:

- **Projectspecifieke variabelen**—Dezelfde waarde instellen voor _alles_ in uw project. Deze variabelen zijn beschikbaar bij het samenstellen en uitvoeren in alle omgevingen.

  ```bash
  magento-cloud variable:create --level project --name <variable-name> --value <variable-value>
  ```

- **Omgevingsspecifieke variabelen**—Een unieke waarde instellen voor een _specifiek_ milieu. Deze variabelen zijn beschikbaar bij uitvoering en worden overgeërfd door onderliggende omgevingen. Geef de omgeving in de opdracht op met de opdracht `-e` -optie.

  ```bash
  magento-cloud variable:create --level environment --name <variable-name> --value <variable-value>
  ```

Nadat u projectspecifieke variabelen hebt ingesteld, moet u de externe omgeving handmatig opnieuw implementeren voordat de wijziging van kracht wordt. Duw de nieuwe verplichtingen om een herplaatsing teweeg te brengen.

>[!TAB Console]

**Variabelen instellen met de opdracht[!DNL Cloud Console]**:

1. In de _[!DNL Cloud Console]_klikt u op het configuratiepictogram rechts van de projectnavigatie.

   ![Project configureren](../../assets/icon-configure.png){width="36"}

1. Om een project-vlakke variabele te plaatsen, onder _Projectinstellingen_ klikken **Variabelen**.

   ![Projectvariabelen](../../assets/ui-project-variables.png)

1. Om een milieu-vlakke variabele te plaatsen, in _Omgevingen_ selecteer een omgeving en klik op **[!UICONTROL Variables]** tab.

   ![Het tabblad Omgevingsvariabelen](../../assets/ui-environment-variables.png)

1. Klik op **[!UICONTROL Create variable]**.

1. Geef een naam en waarde voor de variabele op. Kies een van de volgende opties:

   - Beschikbaar tijdens runtime
   - Beschikbaar tijdens buildtijd
   - JSON-waarde
   - Gevoelige variabele (waarde verborgen in de console en CLI reacties)
   - Overerving mogelijk maken (onderliggende omgevingen kunnen omgevingspremies overerven)

1. Klik op **[!UICONTROL Create variable]**.

>[!CAUTION]
>
>Omgevingsspecifieke variabelen instellen in het dialoogvenster [!DNL Cloud Console] past automatisch de omgeving opnieuw in.

>[!ENDTABS]

## Zichtbaarheid

U kunt de zichtbaarheid van een variabele tijdens het samenstellen of uitvoeren beperken met de opdracht `--visible-<build|runtime>` gebruiken. Er zijn ook opties om overerving en gevoeligheid in te stellen.

Gebruik de volgende opties om te voorkomen dat een variabele wordt gezien of overgeërfd:

- `--inheritable false`—schakelt overerving voor kindmilieu&#39;s uit. Dit is handig als u alleen productiewaarden wilt instellen op de `master` vertakking en het toestaan van alle andere milieu&#39;s om een project-vlakke variabele van de zelfde naam te gebruiken.
- `--sensitive true`—markeert de variabele als _onleesbaar_ in de [!DNL Cloud Console]. U kunt de variabele niet weergeven in de gebruikersinterface, maar u kunt de variabele wel vanuit de toepassingscontainer bekijken, net als elke andere variabele.

Hieronder ziet u een specifiek geval waarin wordt voorkomen dat een variabele wordt gezien of overgeërfd. U kunt deze opties slechts in CLI specificeren. Dit geval heeft niet betrekking op alle beschikbare omgevingsvariabelen.

```bash
magento-cloud variable:create --name <variable-name> --value <variable-value> --inheritable false --sensitive true
```

## Variabeleniveaus en -waarden verifiëren

U kunt een lijst met bestaande variabelen weergeven met de CLI van de cloud.

```bash
magento-cloud variables
```

```terminal
Variables on the project Project-Name (<project-id>), environment <environment-name>:
+----------------------------+-------------+-------------------------------------------+
| Name                       | Level       | Value                                     |
+----------------------------+-------------+-------------------------------------------+
| env:COMPOSER_AUTH          | project     | {                                         |
|                            |             |    "http-basic": {                        |
|                            |             |       "repo.magento.com": {               |
|                            |             |       "username":                         |
|                            |             | "<public-key>",                           |
|                            |             |       "password":                         |
|                            |             | "<private-key>"                           |
|                            |             |     }                                     |
|                            |             |   }                                       |
|                            |             | }                                         |
| ADMIN_EMAIL                | project     | admin@123.com                             |
| ADMIN_EMAIL                | environment | admin@123.com                             |
| ADMIN_PASSWORD             | environment | password                                  |
| ADMIN_URL                  | environment | admin123                                  |
| ADMIN_USERNAME             | environment | admin                                     |
| php:newrelic.license       | environment | xxxx71fb030366182117f955a22e4baf8exxxxxx  |
+----------------------------+-------------+-------------------------------------------+
```
