---
title: Pro-architectuur
description: Leer meer over de omgevingen die worden ondersteund door de Pro-architectuur.
feature: Cloud, Auto Scaling, Iaas, Paas, Storage
topic: Architecture
exl-id: d10d5760-44da-4ffe-b4b7-093406d8b702
source-git-commit: 6807b572366d28fd54fbec89e7c119ec158b5e10
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 0%

---

# Pro-architectuur

Uw Adobe Commerce on cloud Infrastructure Pro-architectuur ondersteunt meerdere omgevingen die u kunt gebruiken om uw winkel te ontwikkelen, te testen en te starten.

- **Master**—Biedt een `master` tak die aan Platform als de dienstcontainers (PaaS) wordt opgesteld.
- **Integratie**—Verstrekt één enkele `integration` vertakking voor ontwikkeling, hoewel u één extra tak kunt tot stand brengen. Dit maakt maximaal twee _actief_ de takken die aan Platform als de dienstcontainers (PaaS) worden opgesteld.
- **Staging**—Verstrekt één enkele `staging` tak die aan specifieke Infrastructuur als dienstcontainers (IaaS) wordt opgesteld.
- **Productie**—Verstrekt één enkele `production` tak die aan specifieke Infrastructuur als dienstcontainers (IaaS) wordt opgesteld.

De volgende tabel geeft een overzicht van de verschillen tussen omgevingen:

|                                        | INTEGRATIE | STAGING | PRODUCTIE |
| -------------------------------------- | ----------- | ----------------- | -------------------- |
| Ondersteunt het instellingenbeheer in het dialoogvenster [!DNL Cloud Console] | Ja | Beperkt | Beperkt |
| Ondersteunt meerdere takken | Ja | Nee (alleen Staging) | Nee (alleen productie) |
| Gebruikt YAML-bestanden voor configuratie | Ja | Nee | Nee |
| Wordt uitgevoerd op toegewezen IaaS-hardware | Nee | Ja | Ja |
| Inclusief snel CDN | Nee | Ja | Ja |
| Inclusief New Relic-service | Nee | APM | APM + NRI |
| Automatische back-ups | Nee | Ja | Ja |

>[!NOTE]
>
>Adobe biedt het hulpprogramma Cloud Docker for Commerce voor het implementeren naar een lokale Cloud Docker-omgeving zodat u Adobe Commerce-projecten kunt ontwikkelen en testen. Zie [Dockingontwikkeling](../dev-tools/cloud-docker.md).

## Omgevingsarchitectuur

Uw project is één Git-opslagplaats met drie belangrijke omgevingsvertakkingen: `integration`, `staging`, en `production`. Het volgende diagram toont de hiërarchische verhouding van Pro milieu&#39;s:

![Weergave op hoog niveau van de Pro-omgevingsarchitectuur](../../assets/pro-branch-architecture.png)

### Hoofdomgeving

Bij Pro-projecten worden de `master` de tak verstrekt een actieve milieu van PaaS met uw productiemilieu. Een kopie van de productiecode altijd naar de `master` milieu zodat u het productiemilieu kunt zuiveren zonder de diensten te onderbreken.

**Voorbehouden:**

- Do **niet** een vertakking maken op basis van de `master` vertakking. Gebruik de integratieomgeving om actieve vertakkingen voor ontwikkeling te maken.

- Gebruik de `master` omgeving voor ontwikkelings-, UAT- of prestatietests

### Integratieomgeving

De integratieomgeving wordt uitgevoerd in een Linux-container (LXC) op een raster met servers die PaaS wordt genoemd. Elke omgeving bevat een webserver en database waarmee u uw site kunt testen. Zie [Regionale IP-adressen](../project/regional-ip-addresses.md) voor een lijst van AWS en Azure IP adressen.

**Aanbevolen gebruiksgevallen:**

De milieu&#39;s van de integratie worden ontworpen voor beperkte test en ontwikkeling alvorens veranderingen in het opvoeren en productiemilieu&#39;s te bewegen. U kunt bijvoorbeeld de integratieomgeving gebruiken om de volgende taken uit te voeren:

- Ervoor zorgen dat wijzigingen in processen voor continue integratie (CI) compatibel zijn met de cloud

- Kritieke workflows testen op sleutelpagina&#39;s zoals Home, Categorie, pagina met productdetails (PDP), Afhandeling en Beheer

Voor de beste prestaties in de integratieomgeving volgt u de volgende aanbevolen procedures:

- Catalogusgrootte beperken

- Gebruik beperken tot een of twee gelijktijdige gebruikers

- Snijtaken uitschakelen en indien nodig handmatig uitvoeren

**Voorbehouden:**

- Snelle CDN- en New Relic-services zijn niet toegankelijk in een integratieomgeving

- De architectuur van het integratiemilieu past niet de Staging en architectuur van de Productie aan

- Gebruik de `integration` omgeving voor het testen van de ontwikkeling, het testen van de prestaties, of het testen van de gebruikersacceptatie (UAT)

- Gebruik de `integration` omgeving om B2B voor Adobe Commerce-functionaliteit te testen

- U kunt de database niet terugzetten in de integratieomgeving vanuit de databaseproductie of -staging

{{enhanced-integration-envs}}

### Stationele omgeving

De testomgeving biedt een omgeving voor bijna-productie om uw site te testen. Deze omgeving, die wordt gehost op toegewezen IaaS-hardware, omvat alle services, zoals Fastly CDN, New Relic APM en zoeken.

**Aanbevolen gebruiksgevallen:**

De omgeving komt overeen met de productiearchitectuur en is ontworpen voor UAT, inhoudstaging en definitieve revisie voordat de functies naar de `production` milieu. U kunt bijvoorbeeld de opdracht `staging` omgeving om de volgende taken uit te voeren:

- Regressietest aan de hand van productiegegevens

- Prestaties testen met snelle caching ingeschakeld

- Nieuwe builds testen in plaats van patching in Production

- UAT testen voor nieuwe builds

- Test B2B voor Adobe Commerce

- De configuratie van de uitsnede aanpassen en de taken voor uitsnijden testen

Zie [Implementatieworkflow](pro-develop-deploy-workflow.md#deployment-workflow) en [Implementatie testen](../test/staging-and-production.md).

**Voorbehouden:**

- Na het lanceren van de productielocatie, gebruik het het opvoeren milieu hoofdzakelijk om flarden voor productie-kritieke insectenmoeilijke situaties te testen.

- U kunt geen vertakking maken van de `staging` vertakking. In plaats daarvan voert u wijzigingen in de code uit `integration` vertakken naar `staging` vertakking.

### Productieomgeving

De productieomgeving voert uw openbare, naar wens enkelvoudige en multisite winkels uit. Deze omgeving wordt uitgevoerd op toegewezen IaaS-hardware met redundante knooppunten met hoge beschikbaarheid voor continue toegang en failover-beveiliging voor uw klanten. De productieomgeving omvat alle services in de testomgeving, plus de [New Relic Infrastructure (NRI)](../monitor/new-relic-service.md#new-relic-infrastructure) service, die automatisch verbinding maakt met de toepassingsgegevens en prestatieanalyses voor dynamische serverbewaking.

**Voorbehoud:**

U kunt geen vertakking maken van de `production` vertakking. In plaats daarvan voert u wijzigingen in de code uit `staging` vertakken naar `production` vertakking.

### Stapel productietechnologie

De productieomgeving heeft drie virtuele machines (VM&#39;s) achter een Elastic Load Balancer die wordt beheerd door een HAProxy per VM. Elke VM bevat de volgende technologieën:

- **Fastly CDN**—HTTP-caching en CDN

- **NGINX**—webserver met PHP-FPM, één instantie met meerdere workers

- **GlusterFS**—bestandsserver voor het beheer van alle implementaties van statische bestanden en synchronisatie met vier directorymontageprogramma&#39;s:

   - `var`
   - `pub/media`
   - `pub/static`
   - `app/etc`

- **Redis**—één server per VM met slechts één actief en de andere twee als replica&#39;s

- **Elasticsearch**—Adobe Commerce zoeken naar cloudinfrastructuur 2.2 tot 2.4.3-p2

- **OpenSearch**—Adobe Commerce zoeken naar cloudinfrastructuur 2.3.7-p3, 2.4.3-p2, 2.4.4 en hoger

- **Galera**—databasecluster met één MariaDB MySQL-database per knooppunt met een automatisch verhogende instelling van drie voor unieke id&#39;s voor elke database

De volgende afbeelding toont de technologieën die in de productieomgeving worden gebruikt:

![Stapel productietechnologie](../../assets/az-stack-diagram.png)

## Redundante hardware

In plaats van een traditioneel, actief-passief `master` Voor een primaire secundaire configuratie voert Adobe Commerce op cloudinfrastructuur een _redundante architectuur_ waarbij alle drie instanties lezen en schrijven accepteren. Deze architectuur biedt geen onderbreking wanneer het schrapen aan en verstrekt gewaarborgde transactionele integriteit.

Vanwege de unieke, redundante hardware kan Adobe drie gatewayservers leveren. De meeste externe diensten laten u toe om veelvoudige IP adressen aan een lijst van gewenste personen toe te voegen, zodat heeft meer dan één vast IP adres geen probleem is. De drie gateways wijzen aan de drie servers in uw cluster van het productiemilieu toe en behouden statische IP adressen. Het is volledig overtollig en hoogst beschikbaar op elk niveau:

- DNS
- Content Delivery Network (CDN)
- Elastic Load balancer (ELB)
- Drieservercluster bestaande uit alle Adobe Commerce-services, inclusief de database en webserver

## Back-up en noodherstel

Adobe Commerce op cloudinfrastructuur maakt gebruik van een architectuur met hoge beschikbaarheid die elk Pro-project repliceert op drie aparte AWS- of Azure-beschikbaarheidszones, elke zone met een afzonderlijk datacenter. Naast deze overtolligheid, ontvangen de Pro het opvoeren en productiemilieu&#39;s regelmatige, levende steunen die voor gebruik in gevallen van worden ontworpen _catastrofale fout_.

**Automatische back-ups** bevat permanente gegevens van alle actieve services, zoals de MySQL-database en bestanden die zijn opgeslagen op de gekoppelde volumes. De back-ups worden opgeslagen in gecodeerde EBS (Elastic Block Storage) in hetzelfde gebied als de productieomgeving. De automatische steunen zijn niet openbaar toegankelijk omdat zij in een afzonderlijk systeem worden opgeslagen.

{{pro-backups}}

U kunt een **handmatige back-up** van het gegevensbestand voor uw het Opvoeren en milieu&#39;s van de Productie die CLI bevelen gebruiken. Zie [Back-up maken van de database](../storage/database-dump.md). Voor `integration` Adobe raadt u aan een back-up te maken als eerste stap nadat u uw Adobe Commerce hebt benaderd voor een infrastructuurproject in de cloud en voordat u belangrijke wijzigingen aanbrengt. Zie [Back-upbeheer](../storage/snapshots.md).

### Doelstelling herstelpunt

RPO is zes uren maximumtijd aan laatste steun (bijvoorbeeld bij 06:00, toen 12:00, toen 18:00). De frequentie van back-ups is afhankelijk van het back-upschema van uw abonnement en het volume van de wijzigingen dat naar de opslagservice moet worden geschreven.

### Retentiebeleid

Met Adobe blijven automatische back-ups behouden volgens het volgende beleid voor gegevensopslag:

| Tijdsperiode | Retoucheringsbeleid voor back-up |
| ------------------ | ----------------------- |
| Dag 1 tot en met 3 | Eén back-up per uur |
| Dagen 4 tot en met 7 | Eén back-up per dag |
| Week 2 tot en met 6 | Eén back-up per week |
| Week 8 tot en met 12 | Eén back-up per twee weken |
| Maand 3 tot en met 5 | Eén back-up per maand |

Dit beleid kan afhankelijk van uw plan van de wolkeninfrastructuur variëren.

### Doelstelling hersteltijd

RTO is afhankelijk van de grootte van de opslag. Grote EBS-volumes hebben meer tijd nodig om te herstellen. De hersteltijden kunnen variëren afhankelijk van de grootte van uw database:

- Een grote database (200+ GB) kan 5 uur duren
- Een middelgrote database (150 GB) kan 2 1/2 uur in beslag nemen
- Een kleine database (60 GB) kan 1 uur duren

{{pro-backups}}

## Schalen in Pro-clusters

De grootte van de Pro-cluster en _berekenen_ afhankelijk van de gekozen cloudprovider (AWS, Azure), regio en serviceafhankelijkheden. De de wolkeninfrastructuur van de Adobe kan Pro clusters schrapen om verkeersverwachtingen en de dienstvereisten aan te passen aangezien de vraag verandert.

De overtollige architectuur laat de Adobe wolkeninfrastructuur toe om zonder onderbreking te verhogen. Bij upscaling roteert elk van de drie instanties om de capaciteit te upgraden zonder dat dit invloed heeft op de sitebewerking. U kunt bijvoorbeeld extra webservers toevoegen aan een bestaande cluster als de beperking zich op PHP-niveau bevindt in plaats van op databaseniveau. Dit biedt _horizontale schaling_ om de verticale schaling aan te vullen die wordt geboden door extra CPU&#39;s op databaseniveau. Zie [Schaalbare architectuur](scaled-architecture.md).

Als u een significante toename van verkeer voor een gebeurtenis of een andere reden verwacht, kunt u om een tijdelijke verhoging van capaciteit verzoeken. Zie [Een tijdelijke upgrade aanvragen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-request-temporary-magento-upsize.html) in de _Hulp-centrum voor handel_.
