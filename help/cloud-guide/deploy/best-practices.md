---
title: Aanbevolen werkwijzen voor implementatie
description: Ontdek best practices voor de implementatie van Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Deploy, Best Practices
exl-id: bac3ca83-0eee-4fda-9a5c-a84ab25a837a
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '1904'
ht-degree: 0%

---

# Aanbevolen werkwijzen voor implementatie

Scripts maken en implementeren die worden geactiveerd wanneer u code samenvoegt in een externe omgeving. Deze scripts gebruiken de omgeving [configuratiebestanden](../environment/overview.md) en toepassingscode om cloudinfrastructuur van geschikte gegevens en diensten te voorzien. Deze scripts worden ook gebruikt om de Adobe Commerce-toepassing, services van derden en aangepaste extensies in de cloud te installeren of bij te werken.

Het bouwstijl en opstellen proces is lichtjes verschillend voor elk plan:

- **Startersplannen**—Voor het integratiemilieu, bouwt elke actieve tak en stelt aan een volledig milieu voor toegang en het testen op. Test de code na het samenvoegen tot de `staging` vertakking. Als u uw site wilt starten, drukt u op `staging` tot `master` in de productieomgeving te implementeren. U hebt volledige toegang tot alle vertakkingen via [!DNL Cloud Console] en de CLI bevelen.

- **Pro-abonnementen**—Voor het integratiemilieu, bouwt elke actieve tak en stelt aan een volledig milieu voor toegang en het testen op. Voeg uw code samen met de `integration` vertakken alvorens aan de het Staging en milieu&#39;s van de Productie samen te voegen. U kunt samenvoegen tot de omgevingen voor Staging en Productie met de [!DNL Cloud Console] of SSH gebruiken en `magento-cloud` CLI-opdrachten.

## Het proces volgen

U kunt bouwstijl volgen en acties in real time opstellen gebruikend de terminal of [!DNL Cloud Console] Statusberichten—`in-progress`, `pending`, `success`, of `failed`—display tijdens het implementatieproces. U kunt details in de logboekdossiers bekijken. Zie [Logboeken weergeven](../test/log-locations.md).

Als u externe bewaarplaatsen GitHub gebruikt, toont het logboek van verrichtingen niet in de zitting GitHub. U kunt echter wel de activiteit volgen in de interface voor de externe opslagplaats en de [!DNL Cloud Console]. Zie [Integraties](../integrations/overview.md).

>[!NOTE]
>
>In integratieomgevingen kunt u de implementatielogboeken niet weergeven vanuit de [!DNL Cloud Console]. Deze functie is alleen beschikbaar voor Productie- en Staging-omgevingen. Nochtans, kunt u logboeken voor elke fase van de plaatsing in om het even welk milieu bekijken gebruikend [bouwen en implementeren](../test/log-locations.md#build-and-deploy-logs) logboeken. Voor het oplossen van problemeninformatie, zie [Overzicht van implementatiefouten](../dev-tools/error-reference.md).

U kunt [Implementaties bijhouden met New Relic](../monitor/track-deployments.md) om plaatsingsgebeurtenissen te controleren en prestaties tussen plaatsingen te analyseren.

## Aanbevolen werkwijzen voor builds en implementatie

Bekijk deze best practices en overwegingen voor uw implementatieproces:

- **Zorg ervoor dat u de meest actuele versie van de `ece-tools` package**

  Zie [Opmerkingen bij de release ECE-tools](../release-notes/ece-tools-package.md).

- **Volg het bouwstijl en opstellen proces**

  Zorg ervoor dat u de juiste code in elke omgeving hebt om te voorkomen dat configuraties worden overschreven wanneer u code samenvoegt tussen omgevingen. Bijvoorbeeld, om configuratieveranderingen op alle milieu&#39;s toe te passen, wijzig en test de veranderingen in het lokale milieu alvorens aan het verre integratiemilieu op te stellen. Dan, stel en test de veranderingen in het het Opvoeren milieu op alvorens aan Productie op te stellen. Wanneer u van één milieu aan een andere samenvoegt, beschrijft de plaatsing al code in het milieu, behalve milieu-specifieke configuratie en montages.

- **Dezelfde variabelen gebruiken in omgevingen**

  De waarden voor deze variabelen kunnen in verschillende omgevingen verschillen, maar meestal hebt u in elke omgeving dezelfde variabelen nodig. Zie [Configuratiebeheer voor opslaginstellingen](../store/store-settings.md).

- **Behoud gevoelige configuratiewaarden en gegevens in milieu-specifieke variabelen**

  Deze waarden omvatten variabelen die zijn opgegeven met de Cloud CLI, de [!DNL Cloud Console]of toegevoegd aan de `env.php` bestand. Zie [Variabele niveaus](../environment/variable-levels.md).

- **Zorg ervoor dat alle code beschikbaar is in de omgevingsvertakking**

  Verwijzen naar code van andere takken, zoals een privé tak, kan problemen tijdens het bouwstijl veroorzaken en proces opstellen. Als u bijvoorbeeld naar een thema van een privé-vertakking verwijst, is het thema niet toegankelijk en kan het niet worden samengesteld met de toepassingscode.

- **Extensies, integratie en code toevoegen in herhaalde vertakkingen**

  Wijzigingen lokaal aanbrengen en testen `integration`, dan naar `staging` en `production`. Test en los problemen in elke omgeving op voordat u de updates samenvoegt tot de volgende omgeving. Sommige uitbreidingen en integratie moeten in een specifieke orde wegens gebiedsdelen worden toegelaten en worden gevormd. Door het toevoegen en testen in groepen kunt u uw ontwikkelings- en implementatieproces veel eenvoudiger maken en bepalen waar zich problemen voordoen.

- **Verifieer de dienstversies en verhoudingen en de capaciteit om te verbinden**

  Controleer welke services beschikbaar zijn voor uw toepassing en zorg ervoor dat u de meest actuele, compatibele versie gebruikt. Zie [Servicerelaties](../services/services-yaml.md#service-relationships) en [Systeemvereisten](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) in de _Installatiehandleiding_ voor aanbevolen versies.

- **Testen plaatselijk en in het integratiemilieu alvorens aan Staging en Productie op te stellen**

  Identificeer en los kwesties in uw lokale en integratiemilieu&#39;s op om uitgebreide onderbreking te verhinderen wanneer u aan het Opvoeren van Staging en Productiemilieu&#39;s opstelt.

  >[!TIP]
  >
  >Er zijn [slimme wizard](../deploy/smart-wizards.md) bevelen die u kunt gebruiken om te verifiëren dat uw configuratie van het wolkenproject beste praktijken voor bouwstijl en plaatsingsconfiguratie, met inbegrip van de statische strategie van de inhoudsplaatsing (SCD) volgt.

- **Implementeer en test deze in de testomgeving na het uitvoeren van tests in lokale en integratieomgevingen**

  Zie [Testen van het strooisel en de productie](../test/staging-and-production.md).

- **Configuratie van productieomgeving controleren**

  Voordat u gaat implementeren in Productie, moet u de volgende taken uitvoeren:

   - Zorg ervoor dat u verbinding kunt maken met alle drie de knooppunten in de productieomgeving met behulp van [SSH](../development/secure-connections.md).

   - Controleren of Indexers zijn ingesteld op _Bijwerken in schema_. Zie [Indexeringsmodi](https://developer.adobe.com/commerce/php/development/components/indexing/) in de _Handleiding voor extensieontwikkelaars_.

   - Bereid het milieu door om het even welke milieu-specifieke variabelen in de code van de Productie voor te werken, de beschikbaarheid en verenigbaarheid van de dienst te verifiëren, en om het even welke andere vereiste configuratieveranderingen aan te brengen.

- **Het implementatieproces controleren**

  Herzie de berichten van de plaatsingsstatus en verminder kwesties zoals nodig. De cloud controleren [logs](../test/log-locations.md#) voor gedetailleerde logboekberichten.

## Vijf fasen van integratie bouwen en plaatsing

De volgende fasen komen in uw lokale ontwikkelomgeving en integratieomgeving voor. Voor Pro plannen, wordt de code niet opgesteld aan de het Staging of milieu&#39;s van de Productie in deze aanvankelijke fasen.

### Fase 1: Validatie van code en configuratie

Wanneer u eerst een project instelt, [de sjabloon voor de cloudinfrastructuur](https://github.com/magento/magento-cloud) biedt een basis voor de codebestanden. Dit codereantwoord wordt gekloond aan uw project als `master` vertakking.

- **Voor Starter**—`master` vertakking is uw productieomgeving.
- **Voor Pro**—`master` begint als oorsprongvertakking voor het integratiemilieu.

Een vertakking maken van `master` voor uw douanecode, uitbreidingen en modules, en derdesintegratie. Er is een externe integratieomgeving voor het testen van uw code in de cloud.

Wanneer u uw code van uw lokale werkruimte aan de verre bewaarplaats duwt, voltooit een reeks controles en codebevestigingen alvorens manuscripten te bouwen en op te stellen beginnen. De ingebouwde server van de Git bevestigt wat u duwt en veranderingen aanbrengt. Bijvoorbeeld, als u de dienst OpenSearch toevoegt, verifieert de ingebouwde server van het Git dat de topologie van uw cluster dienovereenkomstig wordt gewijzigd.

Als een configuratiebestand een syntaxisfout bevat, wijst de Git-server de push af. Zie [Beveiligingsblok](../development/protective-block.md).

Deze fase loopt ook `composer install` om afhankelijkheden op te halen.

### Fase 2: Genereren

>[!NOTE]
>
>Tijdens de bouwstijlfase, is de plaats niet op onderhoudswijze en als de fouten of de kwesties voorkomen niet neer worden gebracht. Het bouwt slechts de code die sinds vorige bouwt is veranderd.

Deze fase bouwt codebase en loopt haken in `build` deel van `.magento.app.yaml`. De standaardbuild-haak is de `php ./vendor/bin/ece-tools` en voert het volgende uit:

- Hiermee past u patches toe in `vendor/magento/ece-patches`en optionele, projectspecifieke patches in `m2-hotfixes`
- Regeneert code en de [afhankelijkheidsinjectie](https://experienceleague.adobe.com/docs/commerce-operations/operational-playbook/glossary.html) configuratie (dat wil zeggen, de `generated/` map, die `generated/code` en `generated/metapackage`) gebruiken `bin/magento setup:di:compile`.
- Controleert of de [`app/etc/config.php`](../store/store-settings.md) bestaat in de codebase. Adobe Commerce genereert dit bestand automatisch als het tijdens de constructiefase niet wordt gedetecteerd en bevat een lijst met modules en extensies. Als het bestaat, gaat de bouwstijlfase als normaal verder, comprimeert statische dossiers gebruikend GZIP, en stelt op, die onderbreking in de plaatsingsfase vermindert. Zie [build-opties](../environment/variables-build.md) voor meer informatie over het aanpassen of uitschakelen van bestandscompressie.

>[!WARNING]
>
>Op dit punt, is de cluster niet gecreeerd, zodat probeer niet om met een gegevensbestand te verbinden of veronderstel dat er een actief daemon proces is.

Nadat de toepassing is gemaakt, wordt deze op een **alleen-lezen bestandssysteem**. U kunt specifieke koppelpunten vormen die zullen worden gelezen/schrijven. U kunt geen FTP aan de server en modules toevoegen. In plaats daarvan moet u code toevoegen aan uw lokale opslagplaats en uitvoeren `git push`, die het milieu bouwt en opstelt. Zie voor de projectstructuur [De lokale structuur van de projectdirectory](../project/file-structure.md).

### Fase 3: De witruimte voorbereiden

Het resultaat van de bouwstijlfase is een read-only dossiersysteem dat als _slikken_. In deze fase wordt een archief gemaakt en wordt de witruimte permanent opgeslagen. De volgende keer dat u code indrukt, wordt de witruimte uit het archief gebruikt als de service niet is gewijzigd.

- Maakt continue integratie sneller opbouwen door ongewijzigde code opnieuw te gebruiken
- Als de code verandert, werkt de schuine streep voor volgende bouwstijl aan hergebruik bij
- Staat voor onmiddellijk het terugkeren van een plaatsing toe, indien nodig
- Bevat statische bestanden als de `app/etc/config.php` bestand bestaat in de codebase

De witruimte omvat alle bestanden en mappen **met uitzondering van:** montage geconfigureerd in `magento.app.yaml`:

- `"var": "shared:files/var"`
- `"app/etc": "shared:files/etc"`
- `"pub/media": "shared:files/media"`
- `"pub/static": "shared:files/static"`

### Fase 4: Slakken en cluster implementeren

Uw toepassingen en alle [achterste](https://experienceleague.adobe.com/docs/commerce-operations/operational-playbook/glossary.html) dienstverlening als volgt:

- Elke service in een container koppelen, zoals een webserver, OpenSearch, [!DNL RabbitMQ]
- Hiermee wordt het lees-schrijfbestandssysteem gemonteerd (op een opslagraster met hoge beschikbaarheid)
- Vormt het netwerk zodat kunnen de diensten &quot;zien&quot;elkaar (en slechts elkaar)

>[!NOTE]
>
>Breng uw veranderingen in een tak van de Plaats aan nadat al bouwt en plaatsing voltooit en opnieuw duw. Alle omgevingsbestandssystemen zijn _alleen-lezen_. Een alleen-lezen systeem garandeert deterministische implementaties en verbetert de beveiliging van uw site aanzienlijk, omdat geen enkel proces naar het bestandssysteem kan schrijven. Het werkt ook om ervoor te zorgen dat uw code in de milieu&#39;s van de Integratie, het Opvoeren, en van de Productie identiek is.

### Fase 5: implementatiehaken

>[!NOTE]
>
>Deze fase plaatst de [!DNL Commerce] toepassing in de onderhoudsmodus totdat de implementatie is voltooid.

De laatste stap stelt een plaatsingsmanuscript in werking, dat u kunt gebruiken om gegevens in ontwikkelomgevingen, duidelijke geheime voorgeheugens, en vraagexterne ononderbroken-integratiegereedschappen anoniem te maken. Wanneer dit manuscript loopt, hebt u toegang tot alle diensten in uw milieu, zoals Redis.

Als de `app/etc/config.php` bestand bestaat niet in de codebase, statische bestanden worden gecomprimeerd met `gzip` en geïmplementeerd tijdens deze fase, waardoor de duur van de implementatiefase en het onderhoud van de site wordt verhoogd.

>[!NOTE]
>
>Zie [variabelen implementeren](../environment/variables-deploy.md) voor meer informatie over het aanpassen of uitschakelen van bestandscompressie.

Er zijn twee implementatiehaken. De `pre-deploy.php` de haak voltooit noodzakelijke schoonmaak en terugwinning van middelen en code die in de bouwstijlhaak wordt geproduceerd. De `php ./vendor/bin/ece-tools deploy` haakje voert een reeks opdrachten en scripts uit:

- Als Adobe Commerce **niet geïnstalleerd**, wordt geïnstalleerd met `bin/magento setup:install`, de implementatieconfiguratie bijwerkt, `app/etc/env.php`en de database voor de opgegeven omgeving, zoals Redis en URL&#39;s van websites. **Belangrijk:** Wanneer u de [Eerste implementatie](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/launch/overview.html) tijdens de installatie werd Adobe Commerce geïnstalleerd en geïmplementeerd in alle omgevingen.

- If Adobe Commerce **is geïnstalleerd**, voer de benodigde upgrades uit. De looppas van het plaatsingsmanuscript `bin/magento setup:upgrade` het databaseschema en de gegevens (die nodig zijn na de extensie- of kerncode-updates) bij te werken en ook de implementatieconfiguratie bij te werken; `app/etc/env.php`en de database voor uw omgeving. Tot slot wist het plaatsingsmanuscript het geheime voorgeheugen van de Handel van Adobe.

- Het script genereert optioneel statische webinhoud met de opdracht `magento setup:static-content:deploy`.

- Gebruikt bereik (`-s` markering in bouwstijlmanuscripten) met het gebrek plaatsen van `quick` voor een strategie voor de implementatie van statische inhoud. U kunt de strategie aanpassen met de omgevingsvariabele [`SCD_STRATEGY`](../environment/variables-deploy.md#scd_strategy). Zie voor meer informatie over deze opties en functies [Statische strategieën voor bestandsimplementatie](../deploy/static-content.md) en de `-s` markering voor [Statische weergavebestanden gebruiken](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html).

>[!NOTE]
>
>Het plaatsingsmanuscript gebruikt de waarden die door configuratiedossiers in worden bepaald `.magento` en verwijdert het script de map en de inhoud ervan. Dit heeft geen invloed op uw lokale ontwikkelomgeving.

### Post-plaatsing: vorm het verpletteren

Terwijl de plaatsing loopt, stopt het proces inkomend verkeer op het ingangspunt voor 60 seconden en past het verpletteren aan zodat uw Webverkeer bij uw pas gecreëerde cluster aankomt.

Met een geslaagde implementatie wordt de onderhoudsmodus verwijderd om normale toegang mogelijk te maken en worden back-upbestanden (BAK-bestanden) gemaakt voor de `app/etc/env.php` en de `app/etc/config.php` configuratiebestanden.

Het genereren van statische inhoud inschakelen met de opdracht `SCD_ON_DEMAND` variabele en configureer de [`post_deploy` haak](../application/hooks-property.md) zodat de cache wordt gewist en de cache vooraf wordt geladen (warms) _na_ de container begint met het accepteren van verbindingen en _tijdens_ normaal, inkomend verkeer.

Om logboeken te herzien bouwen en op te stellen, zie [Logboeken weergeven](../test/log-locations.md#view-and-manage-logs).
