---
title: Cloud-infrastructuurproject
description: Lees een overzicht van de Adobe Commerce over cloudinfrastructuur [!DNL Cloud Console] en leer hoe u de accountinstellingen kunt openen.
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: ae862898-9b4d-45ed-b370-e82cc6f99017
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# Cloud-infrastructuurproject

Het Adobe Commerce on cloud-infrastructuurproject bevat alle code in Git-vertakkingen, bijbehorende omgevingen en scripts om de [!DNL Commerce] toepassing. De milieu&#39;s bevatten diensten om de [!DNL Commerce] toepassing, inclusief een database, webserver en cacheserver.

Adobe biedt een [!DNL Cloud Console] en ontwikkelaarsgereedschappen om alle aspecten van uw project volledig te beheren. U hebt als accounteigenaar volledige toegang tot alle omgevingen.

## [!DNL Cloud Console]

De [!DNL Cloud Console] verstrekt interactieve methodes om, code van de Handel in een gebruikersvriendelijk formaat te bouwen te beheren en op te stellen. [Aanmelden bij de [!DNL Cloud Console]](https://console.adobecommerce.com) om uw projectlijst te bekijken. U kunt projecten slechts zien die u toestemming hebt om als admin of voor specifieke milieutypes toegang te hebben. Als u een Partner van de Oplossingen van de Adobe bent, kunt u veelvoudige projecten voor cliënten zien die u steunt.

>[!TIP]
>
>Als u geen projecten ziet, moet u contact opnemen met de [Accounteigenaar of projectbeheerder](../project/user-access.md) gekoppeld aan het project en toegang aanvragen. Voor nieuwe gebruikers raadpleegt u de [Instaponderwerp](../../get-started/onboarding.md#cloud-console) in de _Aan de slag_ hulplijn.

De _Alle projecten_ in de weergave worden alle projecten weergegeven waartoe u toegang hebt. U kunt op **[!UICONTROL Show filters]** en filtert uw projectlijst door type, gebied, of plan.

![Projectlijst](../../assets/ui-allprojects-list.png)

### Overzicht van project

Een project selecteren in het menu _Alle projecten_ de lijst opent het projectoverzicht. Het projectoverzicht toont altijd een bar van de projectnavigatie, die een milieuselecteur en een configuratieknoop omvat:

![Projectnavigatie](../../assets/project-nav.png)

Het projectoverzicht, zolang u geen milieu hebt geselecteerd, toont een samenvatting van projectdetails in het voorproefgebied:

- Projectnaam
- Regio, project-id
- Plan, toegewezen opslag, omgevingen, gebruikers
- Storefront-URL met **[!UICONTROL Set a custom domain]** knop

En in het hoofdprojectoverzicht:

- In de weergave Omgevingen wordt een lijst- of boomstructuurweergave weergegeven van ![actieve vertakking](../../assets/icon-active.png){width="32"} (active) and ![inactive branch](../../assets/icon-inactive.png){width="32"} (inactieve) omgevingen.
- [Activiteitenstroom](activity-stream.md) toont lopende, hangende, en recente activiteiten voor het project.
<!-- - Apps & Services—Shows a topology of service containers -->

Voor **Starter** projecten, er is een hiërarchie van takken die van begint `master` (Productie). Elke vertakking die u maakt, wordt weergegeven als onderliggende vertakking van de `master` vertakking. Adobe beveelt aan een `staging` vertakking, dan creeer een `integration` afdeling voor ontwikkeling. Zie [Starter-architectuur](../architecture/starter-architecture.md).

Voor **Pro**, bestaat er een hiërarchie van vertakkingen die begint bij `production` tot `staging` tot `integration`. De ![Speciaal pictogram](../../assets/icon-dedicated.png){width="32"} het pictogram wijst erop dat de tak aan een specifiek milieu opstelt. Alle vertakkingen die u maakt, worden weergegeven als onderliggende vertakkingen van de `integration` vertakking. Zie [Pro-architectuur](../architecture/pro-architecture.md).

![Pro-omgevingslijst](../../assets/pro-environments.png)

### Overzicht van omgeving

Wanneer u een omgeving op de projectnavigatiebalk selecteert, veranderen het overzicht en de navigatiebalk zodat deze zich richten op de geselecteerde omgeving. De navigatiebalk bevat vertakkingsbesturingselementen (Vertakking, Samenvoegen en Synchroniseren) en een configuratieknop:

![Geselecteerde omgeving](../../assets/environment-selected.png)

Het omgevingsoverzicht geeft een overzicht van de omgevingsdetails in het voorvertoningsgebied:

- Omgevingsnaam, type
- Regio, project-id
- Datum en tijdstip van laatste activiteit, inclusief back-up
- Status van HTTP-toegang en zoekmachine
- Machinenaam toegewezen aan omgeving
- Status van omgeving (actief of inactief)
- Storefront-URL met **[!UICONTROL Set a custom domain]** knop

En in het belangrijkste milieu-overzicht:

- [Activiteitenstroom](activity-stream.md) maakt het belangrijkste milieu overzicht en toont lopende, hangende, en recente activiteiten voor het geselecteerde milieu.
<!-- - Services tab shows and Apps & Services menu, including overview and configuration tabs for each service. -->
- [Tabblad Back-ups](../storage/snapshots.md#create-a-manual-backup) biedt een lijst met opgeslagen back-ups, de geschiedenis van back-uphandelingen en de knop Back-up.

### Toegang opslagruimte

Elke actieve omgeving heeft een winkelcentrum. Selecteer een omgeving in de bovenste navigatie en klik op de URL in het omgevingsoverzicht. Er is ook een **[!UICONTROL URLs]** rechts boven de lijst Activiteit.

De URL voor webtoegang kan het volgende bevatten:

```terminal
https://<branch>-<unique-ID>-<project-ID>.<region>.magentosite.cloud/
```

- **Unieke id** = 7 willekeurige alfanumerieke tekens
- **Project-id** = project-id van 13 tekens
- **Regio** = AWS of Azure regio name, zie [Regionale IP-adressen](regional-ip-addresses.md)

De milieu&#39;s van de Proproductie en van het Staging omvatten drie knopen die u tot het gebruiken van de volgende verbindingen kunt toegang hebben:

- URL van taakverdelingsmechanisme:

   - `http[s]://<your-domain>.c.<project-ID>.ent.magento.cloud`
   - `http[s]://<your-staging-domain>.c.<project-ID>.ent.magento.cloud`

- Directe toegang tot een van de drie redundante servers:

   - `http[s]://<your-domain>.{1|2|3}.<project-ID>.ent.magento.cloud`
   - `http[s]://<your-staging-domain>.{1|2|3}.<project-ID>.ent.magento.cloud`

  De productie-URL wordt gebruikt door het netwerk voor inhoudslevering (CDN).

## Instellingen

Open de _Instellingen_ door op het deelvenster ![projectpictogram configureren](../../assets/icon-configure.png){width="36"} (vorm) pictogram op de rechterkant van de projectnavigatie.

### Projectinstellingen

**[!UICONTROL Project Settings]** breidt een menu van project-vlakke controles uit om gebruikers, variabelen, en meer te beheren:

| Optie | Beschrijving |
|--------------|-------------------------------------------------------------------------------------------------------------------------------|
| Algemeen | Beheer de tijdzone voor gebruik met het plannen van steunen of onderhoud. |
| Toegang | Beheren [gebruikerstoegang](user-access.md) naar project- en omgevingstypen. |
| Certificaten | Een lijst weergeven met de SSL-certificaten die aan het project zijn gekoppeld. |
| Sleutel implementeren | Voeg en bekijk de openbare sleutel aan de bewaarplaats van de projectcode toe. |
| Domeinen | Voeg een domeinnaam aan het project toe. Zie [Domeinen beheren](../cdn/fastly-custom-cache-configuration.md#manage-domains). |
| Integraties | Toevoegen en beheren [integratie](../integrations/overview.md), zoals gezondheidsmeldingen en webhaken. |
| Variabelen | Toevoegen [variabelen op projectniveau](../environment/variable-levels.md) die beschikbaar zijn bij het samenstellen en uitvoeren in alle omgevingen. |

{style="table-layout:auto"}

### Omgevingsinstellingen

Klikken **[!UICONTROL Environments]** en selecteer een specifieke omgeving in de lijst voor besturingselementen voor het beheer van site-instellingen, omgevingsvariabelen en meer:

| Optie | Beschrijving |
| --------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Algemeen | Configureer de weergavenaam, het omgevingstype en de bovenliggende omgeving.<br>Verschillende omgevingsinstellingen in-/uitschakelen: |
|           | **Uitgaande e-mails inschakelen**: Verzenden [uitgaande e-mails](outgoing-emails.md) vanuit de omgeving met behulp van het SMTP-protocol. |
|           | **Verbergen in zoekprogramma&#39;s**: Zoekprogramma&#39;s voor zoekmachines blokkeren en vastlopen vanaf de site. |
|           | **HTTP-toegangsbeheer**: Beveiligingsconfiguratie inschakelen voor de [!DNL Cloud Console] het gebruiken van een login en IP controle van de adrestoegang. |
|           | Status `active` of `inactive`. Het grootste deel van je werk is in een actieve omgeving. U kunt de omgeving deactiveren of verwijderen. |
| Variabelen | Weergeven, maken en beheren [variabelen op milieuniveau](../environment/variable-levels.md) beschikbaar bij uitvoering. |
| Domeinen | Een lijst weergeven met [gevormde routes](../routes/routes-yaml.md). |

{style="table-layout:auto"}

>[!WARNING]
>
>**NIET** gebruik de de toegangsbeheermethode van HTTP voor het beveiligen van Pro het Staging en milieu&#39;s van de Productie. Dit verbreekt snel caching. Gebruik in plaats daarvan de opdracht [Blokkeren](../cdn/fastly-vcl-blocking.md) beschikbaar in de snelste CDN voor Adobe Commerce.

## Snelle en New Relic-gebruikersgegevens

Uw project omvat [Snel](../cdn/fastly.md) en [New Relic](../monitor/new-relic-service.md). De projectdetails tonen informatie voor uw projectplan en belangrijke vergunningen en penningen voor deze integratie. Alleen de eigenaar van de licentie heeft initiële toegang tot de referenties en services. Geef deze gegevens desgewenst door aan de technische en ontwikkelaars.

- [Snel](https://www.fastly.com/) biedt CDN (Content Delivery, content optimization, image optimization, and security services (DDoS en WAF) voor uw Adobe Commerce voor infrastructuurprojecten in de cloud. Zie [Snelle gebruikersgegevens ophalen](../cdn/fastly-configuration.md#get-fastly-credentials).

- [New Relic](../monitor/new-relic-service.md) verstrekt toepassingsmetriek en prestatiesinformatie voor het Opvoeren en de milieu&#39;s van de Productie.

Gebruik de [Cloud CLI](../dev-tools/cloud-cli-overview.md) om uw integratietokens, id&#39;s en meer te bekijken:

```bash
magento-cloud subscription:info services
```
