---
title: Commerce voor levering op cloud
description: Leer hoe u een technische adviseur van de klant van de Adobe voorbereidt om uw Adobe Commerce op het project van de wolkeninfrastructuur te leveren.
recommendations: noDisplay, catalog
role: Admin
exl-id: cfb354b0-c255-4b6e-94aa-c5a6bf7230d6
source-git-commit: 89c57a486545d6165e0407f913f4fa4cf6c95abe
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---

# Handel in voorwaarden voor levering in de cloud

Laten we aan de slag en uw Commerce-project initialiseren op cloudinfrastructuur!

Voordat u de Adobe van uw handel in cloudprojectomgevingen gaat regelen, is het raadzaam de volgende strategieën in overweging te nemen en antwoorden voor te bereiden voor uw eerste overleg met het accountteam van uw Adobe. Gebruik de volgende secties als checklist om u voor uw gesprek met een Technische Adviseur van de Klant voor te bereiden om een wolkenproject te verstrekken:

## Domeindefinitie

**Vraag 1**: _Welk domein of welke domeinen wilt u gebruiken voor het starten van de site?_

Bereid u voor om de services Fastly en nginx te integreren door uw domeinen en subdomeinen op hoofdniveau te definiëren voor de omgevingen met Pro Staging en Production. Na de eerste installatie kunt u alleen domeinen toevoegen door een Adobe Commerce Support-ticket in te dienen. Het wordt daarom aangeraden dat u over de domeingegevens beschikt.

Voorbeelden voor de domeinen Productie en Staging:

- `www.your-store.com`
- `your-store.com`
- `mcprod.your-store.com`
- `mcstaging.your-store.com`

Zie [Meerdere websites of winkels instellen](../cloud-guide/store/multiple-sites.md) in de _Handel in Cloud-infrastructuur_ gids voor verdere begeleiding op veelvoudige of unieke domeinen.

## Transactioneel e-maildomein

**Vraag 2**: _Welk domein of welke domeinen wilt u gebruiken voor transactie-e-mails?_

Adobe Commerce on Cloud gebruikt de SendGrid Simple Mail Transfer Protocol (SMTP)-proxyservice, die services biedt voor uitgaande e-mailverificatie en controle van de reputatie. SendGrid verzendt namens u transactie-e-mails, zodat er domeininformatie voor nodig is.

Voorbeeld voor SendGrid-domein: `example@your-store.com`

Zie [SendGrid-mailservice](../cloud-guide/project/sendgrid.md) in de _Handel in Cloud-infrastructuur_ gids voor verdere begeleiding over transactie e-mail en domeinmontages.

## Opslagtoewijzing

**Vraag 3**: _Hoeveel van uw gecontracteerde opslag bent u van plan om voor dossierupload en voor gegevensbestand toe te wijzen?_

Adobe Commerce on cloud Infrastructure gebruikt opslag voor de bestandsstructuur, zoekindexering en de database. U kunt de opslagruimte naar behoefte verdelen vanaf 10 GB voor elke partitie.

De hoeveelheid opslagruimte die u hebt gecontracteerd voor uw cloudproject, vertegenwoordigt de totale opslagcapaciteit voor elke omgeving. Als u bijvoorbeeld 50 GB opslagruimte hebt gekocht, hebt u 50 GB opslagruimte voor elke omgeving. Er is 50 GB aan afzonderlijke opslag voor productie, het opvoeren, en elke integratiemilieu respectievelijk.

U kunt uw gecontracteerde opslag op elk ogenblik verhogen. Voor Pro Production- en Staging-omgevingen moet u een Adobe Commerce Support-ticket indienen om de toewijzing van schijfruimte te wijzigen. Een grootteverhoging van de milieu&#39;s van de Proproductie en van het Staging kan slechts met bepaalde intervallen voorkomen. Afhankelijk van uw huidige gebruik van schijfruimte, zou het steunteam kunnen adviseren om de toewijzing van schijfruimte met een minimum van 10 GB te verhogen. Als de opslagruimte eenmaal is toegewezen, kan de opslagverhoging voor Pro Staging en Production **niet** worden teruggezet.

Zie [Schijfruimte beheren](../cloud-guide/storage/manage-disk-space.md) in de _Handel in Cloud-infrastructuur_ hulplijn.

## Cloud-servicegebied

**Vraag 4**: _Welk Cloud-servicegebied is het meest geschikt voor uw omgeving?_

Kies Amazon Web Services (AWS) of Microsoft Azure als uw IaaS-stichting (Infrastructure as a Service) voor uw Adobe Commerce op cloudinfrasinfrastructuurPro-projecten. Elke dienstverlener werkt in veelvoudige gebieden en verstrekt veelvoudige beschikbaarheidsstreken. Selecteer een gebied dat u op uw locatie handig vindt en verminder de mogelijkheden voor latentie en hogere kosten.

Zie [een kaart van Adobe Commerce-wolkengebieden](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/infrastructure/cloud/regions.html) in de _Afspeelmap voor implementatie_.

## Verbindingsservice

**Vraag 5**: _Hebt u de dienst PrivateLink nodig? Zo ja, in welk gebied is de PrivateLink-verbinding?_

Adobe Commerce on cloud Infrastructure ondersteunt integratie met de AWS Private Link of Azure Private Link-service. Hoewel deze service optioneel is, wordt PrivateLink gebruikt om een veilige, persoonlijke communicatie tot stand te brengen tussen cloudinframingevingen met services en toepassingen die op externe systemen worden gehost.

Het is belangrijk dat u rekening houdt met uw cloudservicestrategie (AWS of Azure), zodat het Adobe Commerce-exemplaar binnen dezelfde regio toegankelijk is. Zie [PrivateLink-service](../cloud-guide/development/privatelink-service.md) in de _Handel in Cloud-infrastructuur_ gids voor meer duidelijkheid over de toegankelijkheid van de regio .

## Doelsite starten

**Vraag 6**: _Wat is de geplande startdatum van uw project?_

Voor het starten van een site is iteratieve configuratie en tests vereist om te kunnen garanderen dat de site correct wordt gestart. Door een doeldatum in te stellen, kunnen u en uw accountteam van de Adobe voorbereidingen treffen voor de laatste, aan de lancering voorafgaande activiteiten, die een oproep omvatten om de laatste stappen te coördineren.

Zie de [Site-overzicht starten](../cloud-guide/launch/overview.md) in de _Handel in Cloud-infrastructuur_ handleiding voor het controleren van het volledige proces en het downloaden van een kopie van de controlelijst voor starten.

>[!TIP]
>
> Bekijk de Cloud-portal en open uw nieuwe cloud-project.
>
>**Volgende stap**: [Onboarding voor handel](onboarding.md)
