---
title: Implementatie van toepassingen configureren
description: Leer hoe te om de eigenschappen in het dossier van de toepassingsconfiguratie te vormen die de manier controleren [!DNL Commerce] toepassingen worden ontwikkeld en geïmplementeerd in de cloud-omgeving.
feature: Cloud, Configuration, Build, Deploy
exl-id: 900da20d-98d2-4c9f-97ec-578aee775b55
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Implementatie van toepassingen configureren

De `.magento.app.yaml` Het bestand bepaalt de manier waarop uw toepassing wordt gemaakt en geïmplementeerd. Hoewel Adobe Commerce op cloudinfrastructuur meerdere toepassingen per project ondersteunt, heeft een project doorgaans één toepassing met de `.magento.app.yaml` in de hoofdmap van de opslagplaats.

De `.magento.app.yaml` heeft vele standaardwaarden, zie [een monster `.magento.app.yaml` file](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml). Altijd de `.magento.app.yaml` voor uw geïnstalleerde versie. Dit bestand kan in Adobe Commerce verschillen in versies van de cloudinfrastructuur.

Gebruik de `.magento.app.yaml` bestand om de volgende configuratiewaarden te definiëren:

- [Eigenschappen](properties.md)—Definieer eigenschapswaarden voor de toepassingsinstantie.
- [Variables, eigenschap](variables-property.md)—Omgevingsvariabelen controleren die vereist zijn voor de [!DNL Commerce] toepassingsversie.
- [PHP-instellingen](php-settings.md)—PHP-opties voor uitvoering configureren.
- [Cache instellen voor statische bestanden](set-cache.md)—Plaats geheime voorgeheugen TTL voor uw media en statische dossiers.
