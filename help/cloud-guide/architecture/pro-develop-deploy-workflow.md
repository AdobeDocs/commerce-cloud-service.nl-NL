---
title: Workflow voor Pro-projecten
description: Leer hoe u de workflows voor ontwikkeling en implementatie van Pro gebruikt.
feature: Cloud, Iaas, Paas
exl-id: 103e90d5-2ef2-4fef-845c-439344666b00
source-git-commit: 08f43a3b0a50cdb2a5e8a45bd2e2448bc6dbca2b
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---

# Workflow voor Pro-projecten

Het Pro-project bevat één Git-opslagplaats met een globale `master` vertakking en drie hoofdomgevingen:

1. **Productie** omgeving voor het lanceren en onderhouden van de livesite
1. **Staging** omgeving voor testen met alle services
1. **Integratie** omgeving voor ontwikkeling en testen

![Pro-omgevingslijst](../../assets/pro-environments.png)

Deze omgevingen zijn `read-only`, waarbij geïmplementeerde codewijzigingen worden geaccepteerd vanuit vertakkingen die vanuit uw lokale werkruimte worden doorgegeven. Zie [Pro-architectuur](pro-architecture.md) voor een volledig overzicht van de Pro-omgevingen. Zie [[!DNL Cloud Console]](../project/overview.md#cloud-console) voor een overzicht van de lijst met Pro-omgevingen in de projectweergave.

In de volgende afbeelding ziet u hoe de workflow voor het ontwikkelen en implementeren van Pro is gebaseerd op een eenvoudige, vertakkende aanpak. U [ontwikkelen](#development-workflow) code die een actieve vertakking gebruikt die op `integration` milieu, _duwen_ en _trekken_ de code verandert in en van uw verre, Actieve tak. U implementeert geverifieerde code door _samenvoegen_ de verre tak aan de basistak, die een geautomatiseerde [bouwen en implementeren](#deployment-workflow) proces voor die omgeving.

![Weergave op hoog niveau van de workflow voor de ontwikkeling van Pro-architectuur](../../assets/pro-dev-workflow.png)

## Ontwikkelingsworkflow

De integratieomgeving biedt één basis `integration` vertakking met uw Adobe Commerce op code voor de cloud-infrastructuur. U kunt één extra actieve omgevingsvertakking maken. Dit staat voor maximaal twee actieve takken toe die aan Platform als de dienstcontainers (PaaS) worden opgesteld. Het aantal niet-actieve omgevingen is onbeperkt.

{{enhanced-integration-envs}}

De projectmilieu&#39;s steunen een flexibel, ononderbroken integratieproces. Begin met het klonen van de `integration` vertakken naar uw lokale projectmap. Creeer een tak, of veelvoudige takken, ontwikkel nieuwe eigenschappen, vorm veranderingen, voeg uitbreidingen toe, en stel updates op:

- **Ophalen** wijzigingen van `integration`

- **Branch** van `integration`

- **Ontwikkelen** code op een lokaal werkstation, inclusief [!DNL Composer] updates

- **Push** code verandert in extern en valideert

- **Samenvoegen** tot `integration` en test

Met een ontwikkelde codetak en de overeenkomstige configuratiedossiers, zijn uw codeveranderingen klaar om aan samen te voegen `integration` vertakking voor uitgebreidere tests. De `integration` milieu is ook het beste voor :

- **Integratie van services van derden**—Niet alle services zijn beschikbaar in de PaaS-omgeving.

- **Configuratiebeheerbestanden genereren**—Sommige configuratie-instellingen zijn _Alleen-lezen_ in een geïmplementeerde omgeving.

- **Uw winkel configureren**—U zou alle opslagmontages volledig moeten vormen gebruikend het integratiemilieu. U kunt de **URL voor beheerder van winkel** op de _integratie_ de milieuweergave in de _[!DNL Cloud Console]_.

## Implementatieworkflow

Telkens als u code van uw lokale werkstation aan het verre milieu duwt of code aan een milieutak samenvoegt, bouwt en stelt manuscripten op produceren nieuwe code en levering de gevormde diensten aan het verre milieu op.

Scripthandelingen maken:

- De plaats in het doelmilieu blijft tijdens een bouwstijl lopen

- Adobe Commerce controleren en uitvoeren op patches en hotfixes voor cloudinfrastructuur

- Compileer code met een bouwstijl en stel logboek op

- Controleren op configuratiebeheer, implementatie van statische inhoud vindt plaats tijdens deze fase

- Een witruimte maken of gebruiken in ongewijzigde code om het proces te versnellen

- Alle back-endservices en -toepassingen aanbieden

Scripthandelingen implementeren:

- Plaats de site in een doelomgeving _Onderhoud_ mode

- Statische inhoud implementeren als deze niet is voltooid tijdens de build

- Adobe Commerce installeren of bijwerken op cloudinfrastructuur

- Vorm het verpletteren voor verkeer

Na het proces voor het maken en implementeren van code komt uw winkel online terug met de nieuwste codewijzigingen en -configuraties. Zie [Implementatieproces](../deploy/process.md).

### Samenvoegen tot integratie

Combineer alle geverifieerde codeveranderingen door uw actieve ontwikkelingstak in de basis samen te voegen `integration` vertakking. U kunt al uw wijzigingen testen op het tabblad `integration` vertakken voordat wijzigingen in de Staging-omgeving worden bevorderd.

### Samenvoegen tot fasering

Staging is een omgeving vóór de productie die alle services en instellingen zo dicht mogelijk bij de productieomgeving biedt. Pers altijd uw codeveranderingen van `integration` milieu voor de `staging` omgeving zodat u uitgebreide tests kunt uitvoeren met alle services. De eerste keer dat u de testomgeving gebruikt, moet u services configureren, zoals [Fastly CDN](../cdn/fastly.md) en [New Relic](../monitor/new-relic-service.md). Configureer betaalgateways, verzendingen, meldingen en andere essentiële services met sandbox- of testgegevens.

Het is best om elke dienst grondig te testen, uw prestaties testende hulpmiddelen te verifiëren, en het testen van UAT als beheerder en als klant uit te voeren, tot u vindt dat uw opslag klaar voor het productiemilieu is. Zie [Je winkel implementeren](../deploy/staging-production.md).

### Samenvoegen tot productie

Na grondig het testen in het opvoeren milieu, fusie aan het productiemilieu en grondig test gebruikend levende geloofsbrieven. Wanneer u uw productiesite start, moeten klanten hun aankopen kunnen voltooien en moeten beheerders de live winkel kunnen beheren. Zie de volgende onderwerpen voor een gedetailleerde, duidelijke looppas-door voor het opstellen van uw opslag en het gaan live:

- [Je winkel implementeren](../deploy/staging-production.md)
- [Site starten](../launch/overview.md)

### Samenvoegen tot algemene stramien

Een kopie van de productiecode altijd naar de algemene `master` in het geval er een opkomende behoefte is om de productieomgeving te zuiveren zonder de diensten te onderbreken.

Do **niet** een vertakking maken van Global `master`. Gebruik de `integration` vertakking om nieuwe, actieve takken voor ontwikkeling en moeilijke situaties te creëren.
