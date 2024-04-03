---
title: '[!DNL ECE-Tools] Pakket'
description: Meer informatie over de [!DNL ECE-Tools] -pakket en hoe u Adobe Commerce kunt beheren en implementeren.
exl-id: 5583a685-29c5-4de5-8d2e-94cff5ff37ab
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# ECE-gereedschapspakket

De [!DNL ECE-Tools] pakket is een set scripts en gereedschappen die zijn ontworpen voor het beheren en implementeren van de [!DNL Commerce] toepassing. De `ece-tools` het pakket vereenvoudigt vele processen, zoals het beheren van kroonbanen, het verifiëren van projectconfiguratie, en het toepassen van de flarden van de Adobe en hete moeilijke situaties. U kunt de functie [open-source [!DNL ECE-Tools] codeopslagplaats op GitHub][ece-repo].

{{ece-tools-package}}

De `ece-tools` Het pakket is compatibel met Adobe Commerce—vanaf versie 2.1.4—en bevat scripts en Adobe Commerce op opdrachten voor de cloud-infrastructuur die zijn ontworpen om u te helpen uw code te beheren en automatisch uw projecten te maken en implementeren.

In het volgende overzicht worden de beschikbare `ece-tools` opdrachten:

```bash
php ./vendor/bin/ece-tools list
```

## Samenstellen en implementeren

De `ece-tools` -pakket bevat opdrachten voor het uitvoeren van bewerkingen voor de fasen van het maken, implementeren en implementeren van een Adobe Commerce op een cloudinframetoepassing. Bijvoorbeeld de `php ./vendor/bin/ece-tools build` begint het bouwproces van de toepassing.

Deze `ece-tools` bevindt zich in de [hooks, eigenschap](../application/hooks-property.md) van de `.magento.app.yaml` configuratiebestand.

## Docker-configuratiegenerator

De `ece-tools` pakket omvat een afhankelijkheid van [magento/magento-cloud-docker] -pakket, dat functionaliteit en configuratiebestanden biedt voor Docker-afbeeldingen om een Docker-ontwikkelomgeving voor Adobe Commerce op cloudinfrastructuur te starten. U kunt Cloud Docker voor Handel ook als een zelfstandig pakket uitvoeren. Zie [Dockingontwikkeling](../dev-tools/cloud-docker.md).

## Services, routes en variabelen

U kunt de `ece-tools` pakket om gedetailleerde informatie over Base64-Gecodeerd te tonen [Cloud-variabelen](../environment/variables-cloud.md) gebruikt in elke Cloud-omgeving. Het volgende bevel toont alle diensten, routes, en variabelen.

```bash
php ./vendor/bin/ece-tools env:config:show
```

Als u een specifieke set gegevens wilt weergeven, gebruikt u de volgende indeling:

```bash
php ./vendor/bin/ece-tools env:config:show <option>
```

- `services`—Toont de relatiegegevens van `MAGENTO_CLOUD_RELATIONSHIPS` omgevingsvariabele, gedefinieerd in de `services.yaml` bestand.
- `routes`—Toont de gevormde routes voor het project gebruikend `MAGENTO_CLOUD_ROUTES` omgevingsvariabele.
- `variables`—Toont de gevormde variabelen voor het project gebruikend `MAGENTO_CLOUD_VARIABLES` omgevingsvariabele.

Voorbeelduitvoer voor de `services` optie:

```terminal
Magento Cloud Services:
+-----------------------------------+----------------------------------+
| Service Configuration             | Value                            |
+-----------------------------------+----------------------------------+
| database:                                                            |
+-----------------------------------+----------------------------------+
| host                              | 127.0.0.1                        |
| password                          | <password>                       |
| port                              | 3306                             |
+-----------------------------------+----------------------------------+
| opensearch:                                                          |
+-----------------------------------+----------------------------------+
| host                              | 127.0.0.1                        |
| port                              | 9200                             |
...
```

## Omgevingsconfiguratie controleren

Er is een reeks verificatiebevelen beschikbaar helpen de configuratie van uw project evalueren. Zie [Slimme wizards](../deploy/smart-wizards.md) in de _Implementatie optimaliseren_ voor een gedetailleerde beschrijving van elke tovenaar bevel. De `wizard:ideal-state` bevel loopt automatisch tijdens de bouwstijlfase. Om de ideale staat van uw project te verifiëren:

```bash
php ./vendor/bin/ece-tools wizard:ideal-state
```

>[!NOTE]
>
>U moet de opdracht `wizard:ideal-state` in de externe Cloud-omgeving. Het bevel keert altijd terug `The configured state is not ideal` fout wanneer uitgevoerd in de lokale ontwikkelomgeving.

Voorbeelduitvoer:

```terminal
Ideal state is configured
```

Zie [Opmerkingen bij de release voor gereedschappen](../release-notes/cloud-tools-suite.md).

## Patches voor Adoben en aangepaste patches

De `ece-tools` pakket omvat een afhankelijkheid van [magento/magento-cloud-patches] -pakket, dat Adobe patches en hotfixes biedt die de integratie van alle Adobe Commerce-versies met Cloud-omgevingen verbeteren en snelle levering van kritieke oplossingen ondersteunt. De &quot;levert ook aangepaste patches die u toevoegt aan uw Adobe Commerce op het project voor cloudinfrastructuur. Zie [Patches toepassen](../development/apply-patches.md).

<!-- link definitions -->

[ece-repo]: https://github.com/magento/ece-tools
[magento/magento-cloud-docker]: https://github.com/magento/magento-cloud-docker
[magento/magento-cloud-patches]: https://github.com/magento/magento-cloud-patches
