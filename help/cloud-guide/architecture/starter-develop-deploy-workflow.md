---
title: Starter-projectworkflow
description: Leer hoe u de workflows voor Starter-ontwikkeling en -implementatie kunt gebruiken.
feature: Cloud, Paas
exl-id: f334047a-1e0d-45c7-bf96-5c2964741951
source-git-commit: 08f43a3b0a50cdb2a5e8a45bd2e2448bc6dbca2b
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 0%

---

# Starter-projectworkflow

De Adobe Commerce on cloud-infrastructuur omvat één Git-opslagplaats met een `master` vertakking voor het productiemilieu dat kan worden vertakt om een opvoerende en veelvoudige integratiemilieu&#39;s voor test en ontwikkelingswerk tot stand te brengen. U kunt maximaal vier actieve omgevingen hebben, waaronder een `master` omgeving voor uw productieserver. Zie [Starter-architectuur](starter-architecture.md) voor een overzicht.

Volg voor uw omgevingen de [!UICONTROL Development > Staging > Production] werkwijze voor het ontwikkelen en implementeren van uw site.

- **Productieomgeving (livesite)**—Verstrekt een volledig productiemilieu met alle diensten die worden gebouwd en van de code op worden opgesteld `master` vertakking.
- **Stationele omgeving**—Verstrekt een volledig het opvoeren milieu dat het productiemilieu met alle diensten aanpast die van worden gebouwd en worden opgesteld `staging` vertakking die u maakt door te klonen van `master`.
- **Integratieomgevingen**—Biedt maximaal twee actieve ontwikkelomgevingen die u maakt van de `staging` vertakking. De `integration` -omgeving biedt geen ondersteuning voor services van derden zoals Fastly en New Relic.

Voor uw takken, kunt u om het even welke ontwikkelingsmethodologie volgen. U kunt bijvoorbeeld een gangbare methode volgen, zoals scrum, om vertakkingen te maken voor elke sprint.

Vanuit elke sprint kunt u vertakkingen maken voor elk gebruikersartikel. Alle verhalen worden testbaar. U kunt voortdurend samenvoegen tot de verftak en die vertakking doorlopend valideren. Wanneer de sprint eindigt, kunt u de sprintvertakking samenvoegen tot `master` alle wijzigingen in de productie van sprot te implementeren zonder een testknelpunt aan te pakken.

## Ontwikkelingsworkflow

De ontwikkeling en de plaatsing op de plannen van de Aanzet beginnen met uw aanvankelijke project. U maakt uw project met de &quot;lege site&quot;, een Adobe Commerce on cloud-infrastructuursjablooncode met een volledig voorbereide winkel. Hiermee maakt u een `master` vertakken met een exemplaar van de code van uw productiemilieu.

De ontwikkelingsworkflow omvat het volgende:

- [Klonen en vertakking](#clone-and-branch) van de `master` om `staging` en ontwikkelingsbijkantoren
- [Code ontwikkelen](#develop-code) en installeer extensies lokaal in een ontwikkelingsvertakking, inclusief [!DNL Composer] updates
- [Configureren](#configure-store) uw opslag- en extensie-instellingen
- [Configuratie genereren](#generate-configuration-management-files) beheerbestanden
- [Push-code](#push-code-and-test) en configuratie om aan te bouwen en op te stellen `staging` en `production` omgevingen

![Workflow ontwikkelen en implementeren](../../assets/starter/workflow.png)

U hebt ook een paar optionele stappen om u te helpen uw code en uw opslaggegevens te ontwikkelen en te testen:

- [Voorbeeldgegevens installeren](#optional-install-sample-data) in uw winkel
- [Gegevens in de productieopslagplaats volledig opvullen](#optional-pull-production-data) tot omgevingen

Hierbij wordt ervan uitgegaan dat u uw [lokale ontwikkelaarswerkruimte](../development/overview.md).

### Klonen en vertakking

Voor een nieuw project van het Plan van de Aanzet, a `master` vertakking is gekloond vanuit de Adobe Commerce op de Git-opslagplaats voor cloudinfrastructuur. Als u vertakking wilt starten en wilt werken met code, kloont u de opdracht `master` vertakken naar uw lokale omgeving.

De indeling van de opdracht Git-kloon is:

```bash
git fetch origin
```

```bash
git pull origin <environment-ID>
```

De eerste keer dat u in vertakkingen voor uw Starter-project begint te werken, maakt u een `staging` vertakking. Hiermee maakt u een codevertakking die overeenkomt met de `master` tak die aan een het Opvoeren milieu aan testconfiguratie en codeveranderingen alvorens aan het productiemilieu opstelt op te stellen.

Volgende, vertakkingen maken van `staging` om code te ontwikkelen, uitbreidingen toe te voegen, en derdesintegratie te vormen. Telkens als u douanecode ontwikkelt, voegt uitbreidingen toe, integreert met de derdedienst, het werk in een ontwikkelingstak die van wordt gecreeerd `staging` vertakking. U hebt vier actieve integratieomgevingen beschikbaar. Wanneer u een actieve vertakking duwt, stelt één van deze integratiemilieu&#39;s automatisch uw code aan test op.

De indeling van de opdracht voor de Git-vertakking is:

```bash
git checkout <branch-name>
```

De indeling van de Cloud CLI `branch` opdracht is:

```bash
magento-cloud environment:branch <environment-name> <parent-environment-ID>
```

![Vertakking van stramien](../../assets/starter/branching.png)

### Code ontwikkelen

Met de basisvertakking van Adobe Commerce op code voor de cloud-infrastructuur kunt u extensies installeren, aangepaste code ontwikkelen, thema&#39;s toevoegen en nog veel meer.

Gebruik een vertakkende strategie met uw ontwikkelingswerk. Het gebruik van één vertakking om al uw werk in één keer uit te voeren kan het testen bemoeilijken. U kunt bijvoorbeeld de methoden voor continue integratie en sprint volgen om te werken:

- Voeg een paar uitbreidingen toe en vorm hen met uw eerste tak
- Druk deze code, test en fusie aan het Staging toen Productie
- Configureer uw services volledig in `services.yaml` en voeg een thema toe
- Druk deze code, test en fusie aan het Staging toen Productie
- Integreren met een service van derden
- Druk deze code, test en fusie aan het Staging toen Productie

Totdat uw winkel volledig is gebouwd, geconfigureerd en klaar is om te worden gestart. Maar blijf lezing, zijn er vele opties voor uw opslag en codeconfiguratie.

>[!NOTE]
>
>Voer nog geen configuraties in uw lokale werkstation uit.

![Code vanuit lokaal netwerk duwen](../../assets/starter/push-code.png)

### Winkel configureren

Wanneer u klaar bent om uw opslag te vormen, duw al uw code aan `integration` milieu. Configureer uw opslaginstellingen vanuit de beheerfunctie voor de integratieomgeving, niet in uw lokale omgeving. U kunt de URL vinden door op **Toegang tot site** in de [!DNL Cloud Console]

Raadpleeg de documentatie voor Adobe Commerce en de geïnstalleerde extensies voor de beste informatie over configuraties. Hier volgen enkele koppelingen en ideeën die u helpen om aan de slag te gaan:

- [Aanbevolen procedures voor winkelconfiguratie](../store/best-practices.md) voor specifieke best practices in de cloud
- [Basisconfiguratie](https://docs.magento.com/user-guide/configuration/configuration-basic.html) voor toegang tot opslagbeheerders, naam, talen, valuta&#39;s, branding, sites, winkelweergaven en meer
- [Thema](https://docs.magento.com/user-guide/design/design-theme.html) voor uw visie op de site en winkels, waaronder CSS en lay-outs
- [Systeemconfiguratie](https://docs.magento.com/user-guide/system/system.html) voor rollen, hulpmiddelen, berichten en uw encryptiesleutel voor uw gegevensbestand
- Instellingen voor extensies gebruiken in de documentatie

Buiten enkel opslagmontages, kunt u veelvoudige plaatsen en opslag, de gevormde diensten, en meer verder vormen. Zie [Uw winkel configureren](../store/overview.md).

### Configuratiebeheerbestanden genereren

Als u vertrouwd bent met Adobe Commerce, kunt u zich zorgen maken over hoe te om uw configuratiemontages van uw gegevensbestand in ontwikkeling aan de het opvoeren en productiemilieu&#39;s te krijgen. Eerder, moest u al uw configuratiemontages neer op papier of aan een dossier kopiëren, en dan manueel de montages toepassen op andere milieu&#39;s. Of u hebt uw database mogelijk gedumpt en deze gegevens naar een andere omgeving geduwd.

Adobe Commerce on cloud Infrastructure biedt twee [Configuratiebeheer](../store/store-settings.md) opdrachten waarmee u configuratie-instellingen vanuit uw omgeving kunt exporteren naar een bestand. Deze opdrachten zijn alleen beschikbaar voor **Adobe Commerce over cloudinfrastructuur 2.2 en hoger**.

- `php .vendor/bin/ece-tools config:dump`—Exporteert alleen de configuratie-instellingen die u hebt ingevoerd of gewijzigd vanuit standaardinstellingen in een configuratiebestand. _Aanbevolen_.
- `php bin/magento app:config:dump`—Exporteert elke configuratie-instelling, inclusief gewijzigd en standaard, naar een configuratiebestand.

Het gegenereerde bestand is `app/etc/config.php`.

Genereer het bestand in de integratieomgeving waarin u Adobe Commerce hebt geconfigureerd. Stap door het proces om het dossier te produceren, het toe te voegen aan uw tak, en het op te stellen.

**Belangrijke opmerkingen** over configuratiebeheer:

- Elke configuratie-instelling die is opgenomen in het bestand dat is gegenereerd op basis van de `app:config:dump` opdracht is vergrendeld voor het bewerken of alleen-lezen in de geïmplementeerde omgeving. Dit is een van de redenen waarom de Adobe aanbeveelt de `.vendor/bin/ece-tools config:dump` gebruiken.

  U installeert bijvoorbeeld een module voor Snel in uw ontwikkelomgeving. U kunt deze module in het opvoeren en productiemilieu slechts vormen. Met de `.vendor/bin/ece-tools config:dump` houdt het bevel die standaardgebieden editable wanneer u uw ontwikkelingsveranderingen in het het Opvoeren en productiemilieu opstelt.

- Het gegenereerde bestand kan lang zijn, afhankelijk van de grootte van uw implementatie. De `.vendor/bin/ece-tools config:dump` wordt een kleiner bestand gegenereerd dan het bestand dat wordt gegenereerd door de opdracht `app:config:dump` gebruiken.

Als u Adobe Commerce versie 2.2 of hoger gebruikt, bieden de opdrachten voor configuratiebeheer een extra functie om vertrouwelijke gegevens te beschermen, zoals referenties van sandboxen voor een PayPal-module. Tijdens het exportproces worden alle waarden met vertrouwelijke gegevens geëxporteerd naar een afzonderlijk configuratiebestand—`env.php` in de `app/etc/` directory. Dit bestand blijft in uw lokale omgeving en wordt niet gekopieerd wanneer u de code naar een andere vertakking verplaatst. U kunt ook omgevingsvariabelen maken met CLI-opdrachten in alle Adobe Commerce-versies van cloudinfrastructuur.

![Omgevingsvariabelen genereren](../../assets/starter/env-variables.png)

Zie [Configuratiebeheer](../store/store-settings.md).

### Pushcode en test

Op dit punt zou u een ontwikkelde codetak met een configuratiedossier moeten hebben (`config.local.php` of `config.php`) klaar om te testen.

Telkens als u code van uw lokale milieu duwt, bouwt een reeks en stelt manuscripten in werking in werking. Deze manuscripten produceren nieuwe code en stellen het aan het verre milieu op. Bijvoorbeeld, als u een ontwikkelingstak van uw lokale milieu aan de verre tak duwt, werkt een passende milieu de diensten, code, en statische inhoud bij.

U hebt rechtstreeks toegang tot deze omgeving via een winkel-URL, een Admin-URL en een SSH. Deze milieu&#39;s omvatten een Webserver, gegevensbestand, en de gevormde diensten. Als u klaar bent, kunt u beginnen met het implementeren en testen in de testomgeving.

Zie voor meer informatie [Implementatieworkflow](#deployment-workflow).

### Optioneel: voorbeeldgegevens installeren

Als u voorbeeldgegevens nodig hebt bij het ontwikkelen van uw winkel, kunt u voorbeeldgegevens installeren. Deze gegevens simuleren een actieve opslag, met inbegrip van klanten, producten, en andere gegevens. Deze voorbeeldgegevens werken het best met een &quot;lege site&quot; Adobe Commerce op de sjablooninstallatie van de cloudinfrastructuur wanneer u uw project maakt. U kunt het beste de voorbeeldgegevens verwijderen voordat u live gaat. Zie [Optionele voorbeeldgegevens installeren](../test/sample-data.md).

![Optionele voorbeeldgegevens installeren](../../assets/starter/sample-data.png)

### Optioneel: volledige productiegegevens

Voeg al uw producten, catalogi, site-inhoud enzovoort rechtstreeks toe aan de `production` milieu. Door deze gegevens toe te voegen aan de productieomgeving, kunt u bijgewerkte prijzen, coupons, voorraad, verkoopmededelingen, informatie over toekomstig aanbod en meer voor uw klanten verstrekken. Deze gegevens omvatten geen uitbreidingsconfiguraties, die u in uw lokale ontwikkelingstak vormt.

Als u functies ontwikkelt, extensies toevoegt en thema&#39;s ontwerpt, is het handig om echte gegevens te gebruiken. U kunt op elk gewenst moment [een databasedumpdump maken](../storage/database-dump.md) van de productieomgeving en druk die naar uw Staging- en integratieomgeving als dat nodig is.

Productiegegevens exporteren als testgegevens voor gebruik in staging- en integratieomgevingen:

- [Voer de hulpprogramma&#39;s voor ondersteuning uit](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/run-support-utilities.html) CLI-opdrachten (aanbevolen) bij het exporteren van een beveiligde back-up van klanten en het opslaan van gegevens met behulp van de Adobe Commerce-coderingssleutel

- [Gegevensverzameling](https://docs.magento.com/user-guide/system/support-data-collector.html) hulpmiddel voor het genereren en exporteren van gegevens

Als u deze gegevens wilt migreren, raadpleegt u [Statische bestanden en gegevens migreren en implementeren](../deploy/staging-production.md#migrate-static-files).

![Productiegegevens aftrekken en ontsmetten](../../assets/starter/data-code-process.png)

>[!NOTE]
>
>Voordat u de gegevens naar een andere omgeving verplaatst, moet u overwegen de gegevens te ontsmetten. U hebt een aantal opties, waaronder [gebruiken, hulpprogramma&#39;s](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/run-support-utilities.html) of het ontwikkelen van een manuscript om klantengegevens te schrobben.

>[!WARNING]
>
>Verplaats een database niet van een integratie- of testomgeving naar een productieomgeving. Als u, de gegevens van de integratie of het opvoeren milieu uw levende productiegegevens, met inbegrip van verkoop, orden, nieuwe en bijgewerkte klanten, en meer overschrijft.

## Implementatieworkflow

Zoals beschreven in de architectuurinformatie, wordt Adobe Commerce op cloudinfrastructuur aangestuurd door Git. Adobe Commerce implementeren op cloudinfrastructuur maakt deel uit van uw Git-pushprocessen voor vertakkingen.

Wanneer u vertakte code van uw lokale milieu aan de verre tak duwt, begint een reeks bouwstijl en stelt manuscripten op.

Scripts maken:

- De site in de doelomgeving blijft actief tijdens een build

- Adobe Commerce controleren en uitvoeren op patches en hotfixes voor cloudinfrastructuur

- Compileer uw code met een bouwstijl en stel logboek op

- Controleren op configuratiebeheer als de implementatie van statische inhoud tijdens deze fase plaatsvindt

- Een witruimte maken of gebruiken als ongewijzigde code voor een sneller proces

- Alle back-endservices en -toepassingen aanbieden

Scripts implementeren:

- Zet uw site in de modus Onderhoud op de doelomgeving

- Statische inhoud implementeren als deze niet is voltooid tijdens de build

- Adobe Commerce installeren of bijwerken op cloudinfrastructuur

- Vorm het verpletteren voor verkeer

Wanneer uw winkel volledig is voltooid, kunt u online terugkeren, live, met al uw bijgewerkte code en configuraties.

Zie [Implementatieproces](../deploy/process.md).

### Naar testfase duwen en testen

Pers altijd uw code in herhalingen aan `staging` omgeving voor volledige testen. De eerste keer dat u deze omgeving gebruikt, moet u een aantal services configureren, waaronder [Snel](/help/cloud-guide/cdn/fastly.md) en [New Relic](../monitor/new-relic-service.md). Configureer ook betaalgateways, verzendingen, meldingen en andere essentiële services met sandbox- of testgegevens.

Staging is een omgeving vóór de productie die alle services en instellingen zo dicht mogelijk bij de productie biedt. Test grondig elke dienst, verifieer uw prestaties testende hulpmiddelen, voer het testen van UAT als beheerder en als klant uit, tot u uw opslag klaar voor productie voelt.

Zie [Je winkel implementeren](../deploy/staging-production.md).

### Verschuiven naar productie

Wanneer u op de knop `master` vertakt, duikt u naar `production` milieu. Voltooi configuratie- en testactiviteiten in de productieomgeving, net als in de testomgeving, met één belangrijk verschil. Gebruik in de productieomgeving live referenties voor configuratie en testen. Wanneer u uw site start, kunnen klanten hun aankopen voltooien en kunnen beheerders de live winkel beheren.

Zie [Je winkel implementeren](../deploy/staging-production.md).

### Site starten

Er is een duidelijke doorloop om met uw site te gaan wonen. Nadat u deze stappen hebt uitgevoerd, kan uw winkel producten in uw aangepaste thema meteen verkopen.

Zie [Site starten](../launch/overview.md).

## Continue integratie

Na uw vertakkings en ontwikkelingsmethodologieën, kunt u nieuwe eigenschappen gemakkelijk ontwikkelen, veranderingen vormen, en uitbreidingen toevoegen om updates onophoudelijk te ontwikkelen en op te stellen.

Alle omgevingen met cloudinfrastructuren ondersteunen continue integratie voor constante updates. Deze workflow biedt ondersteuning voor releases die meerdere keren per dag of volgens een vast tijdschema worden uitgevoerd.

- Ontwikkeltakken maken met toekomstige functies en wijzigingen

- Test de code in uw `integration` milieu

- Implementeren en testen in `staging` milieu

- Distribueren naar de `production` milieu
