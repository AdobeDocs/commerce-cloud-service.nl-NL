---
title: Implementatieproces
description: Leer hoe implementatie werkt voor Adobe Commerce op cloud-infrastructuurprojecten.
feature: Cloud, Build, Deploy, SCD
exl-id: 378fa290-5a71-4ac2-816a-a7c837e45b2f
source-git-commit: 3d9e3294872fedcc43744f54a71c71d8951ed853
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Implementatieproces

Het implementatieproces begint wanneer u een samenvoeging, push of synchronisatie van uw omgeving uitvoert of wanneer u een [handmatige herplaatsing](../dev-tools/cloud-cli-overview.md#redeploy-the-environment). Het implementatieproces neemt tijd in beslag, maar er zijn manieren om de implementatie te optimaliseren die afhankelijk zijn van het feit of u een livesite ontwikkelt en test of ermee werkt. Met name kunt u de [implementatie van statische inhoud](static-content.md).

Er zijn drie, verschillende fasen van het plaatsingsproces: bouw, stel, en post-opstellen op. Elke fase voert specifieke acties met beperkte middelen uit:

## ![Bouwfase](../../assets/status-build.png) Bouwfase

De _build_ fase assembleert containers voor de diensten die in de configuratiedossiers worden bepaald, installeert gebiedsdelen die op de `composer.lock` en voert de bouwstijlhaken uit die in `.magento.app.yaml` bestand. Zonder de capaciteit om met om het even welke diensten te verbinden of tot het gegevensbestand toegang te hebben, hangt de bouwstijlfase van de middelen af die tot het milieu worden beperkt.

## ![Implementatiefase](../../assets/status-deploy.png) Implementatiefase

De _inzetten_ fase plaatst tijdelijk greep op inkomende verzoeken en overgaat de plaats aan [onderhoudsmodus](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html). De opstellen fase gebruikt de nieuwe containers en, na het opzetten van het dossiersysteem, opent netwerkverbindingen, activeert de diensten die in `relationships` van de `.magento.app.yaml` en voert de implementatiehaken uit die in het dialoogvenster `.magento.app.yaml` bestand. Alles is _alleen-lezen_, behalve voor mappen die zijn gedefinieerd in het `.magento.app.yaml` bestand. Standaard worden de [`mounts` eigenschap](../application/properties.md#mounts) bevat de volgende mappen:

- `app/etc`—bevat de `env.php` en `config.php` configuratiebestanden
- `pub/media`—bevat alle mediagegevens, zoals producten of categorieën
- `pub/static`—bevat gegenereerde statische bestanden
- `var`—bevat tijdelijke bestanden die tijdens runtime zijn gemaakt

Alle andere mappen hebben alleen-lezen machtigingen. De nieuwe plaats wordt actief aan het eind van de opstellen fase aangezien het uit onderhoudswijze overgaat en de tijdelijke greep op inkomende verzoeken vrijgeeft.

Tijdens de implementatiefase worden kopieën van de `app/etc/config.php` en `app/etc/env.php` implementatieconfiguratiebestanden worden opgeslagen met de BAK-extensie. Zie [Opslaginstellingen](../store/store-settings.md#restore-configuration-files) voor meer informatie over het herstellen van deze bestanden.

## ![Na implementatie](../../assets/status-post-deploy.png) Na implementatie

De _na implementatie_ fase voert de haken uit die na implementatie in de `.magento.app.yaml` bestand. Het uitvoeren van om het even welke actie op deze fase kan plaatsprestaties beïnvloeden; nochtans kunt u gebruiken [WARM_UP_PAGES](../environment/variables-post-deploy.md#warmuppages) omgevingsvariabele om de cache te vullen.

## ![Status verifiëren](../../assets/status-verify.png) Configuraties verifiëren

U kunt de optimale configuratie voor de staat van uw project testen door in werking te stellen [Slimme wizards](smart-wizards.md).

>[!NOTE]
>
>Met `ece-tools` 2002.1.0 en hoger kunt u de op scenario&#39;s gebaseerde implementatiefunctie gebruiken om de ontwikkelings-, implementatie- en postimplementatieprocessen voor uw Adobe Commerce aan te passen in het infrastructuurproject in de cloud. Zie [Implementatie op basis van scenario&#39;s](scenario-based.md).
