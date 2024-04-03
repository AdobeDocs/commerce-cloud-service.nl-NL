---
title: Activiteitenstroom
description: Leer hoe u de activiteitsstroom leest in het dialoogvenster [!DNL Cloud Console] of de Cloud CLI voor Adobe Commerce op Cloud-infrastructuur.
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: ffef5ab4-ef40-4073-adc8-a44c61c0d77b
source-git-commit: 85ff1283f773823ff2c6e6ab8f391fd5b4aa00e4
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Activiteitenstroom

In de hoofdweergave van elke omgeving wordt een **Activiteit** lijst met historische gebeurtenissen, vergelijkbaar met een Git-logbestand. De lijst Activiteit is een stroom van de recente gebeurtenissen voor actieve milieu&#39;s. Hieronder volgt een lijst met de activiteitstypen en de bijbehorende pictogrammen die in de activiteitsstroom worden weergegeven:

![Typen activiteiten](../../assets/activity-types.svg){width="500" align="center"}

## Logboeken weergeven

Klik in de lijst Activiteit op het statuspictogram van een activiteit om het logboek weer te geven. U kunt ook op de knop ![Meer](../../assets/icon-more.png){width="32"} (_meer_) voor meer opties voor het beheer van de activiteit. Hieronder ziet u een kort logboek waarin een back-up wordt gemaakt. U kunt [Cloud CLI gebruiken](#activity-stream-with-cloud-cli) om hetzelfde logboek weer te geven.

![Logboekweergave](../../assets/log-view.png)

## Een activiteit beheren

Sommige activiteiten bevinden zich in een _uitvoeren_ of _hangend_ status. U kunt op een lopende activiteit, zoals het annuleren van een lopende plaatsing handelen. In de volgende tabbladen ziet u twee methoden voor het annuleren van een activiteit: de [!DNL Cloud Console] of de Cloud CLI.

>[!BEGINTABS]

>[!TAB Console]

**Als u een activiteit in het dialoogvenster[!DNL Cloud Console]**:

U kunt op een lopende activiteit handelen door tot ![Meer](../../assets/icon-more.png){width="32"} (_meer_) en selecteert u een handeling, zoals `Cancel` of `View log`. Selecteer in dit voorbeeld de optie **Annuleren** om de actieve activiteit te stoppen.

Niet alle activiteiten hebben de annuleringsoptie. De optie om de implementatie van de toepassing te annuleren wordt bijvoorbeeld alleen weergegeven tijdens de _build_ fase. Nadat de toepassing naar de _inzetten_ en kunt u de activiteit niet meer annuleren. Zie [Implementatieproces](../deploy/process.md) over de verschillende fasen.

![Actie annuleren](../../assets/activity-icons/cancel-activity.png){width="450" align="center"}

Als u een terminal hebt die de plaatsingsactiviteit in werking stelt, annuleert in [!DNL Cloud Console] resulteert in de annulering van de terminal:

![Activiteit geannuleerd in terminal](../../assets/activity-icons/activity-cancelled.png){width="300"}

>[!TAB CLI]

**Een activiteit annuleren in de Cloud CLI**:

1. Identificeer de lopende activiteiten en selecteer een activiteit-id.

   ```bash
   magento-cloud activity:list --state=in_progress
   ```

1. Annuleer de activiteit met de activiteit-id:

   ```bash
   magento-cloud activity:cancel wvl5wm7s5vkhy
   ```

>[!ENDTABS]

## Filter Activiteitsstroom

De mogelijkheid om de activiteitenlijst te filteren is nuttig wanneer u op zoek bent naar een specifieke gebeurtenis, zoals een back-up of een samenvoeggebeurtenis.

**De activiteitslijst filteren in het dialoogvenster[!DNL Cloud Console]**:

1. Selecteer een omgeving en kies de activiteit **[!UICONTROL All]** om de volledige gebeurtenisgeschiedenis op te nemen.

1. Klikken ![Filteren op](../../assets/icon-filterby.png){width="32"} en selecteert u de **[!UICONTROL Filter by]** opties:

   ![Filteractiviteiten](../../assets/activity-filter.png)

1. Kies de activiteit **[!UICONTROL Recent]** de lijst weergeven en opnieuw instellen.

## Stream weergeven met Cloud CLI

De `magento-cloud` CLI verstrekt het grootste deel van de zelfde capaciteiten zoals [!DNL Cloud Console]. De `activity` kan:

- `list` de stroom van activiteiten voor een milieu
- `get` bijzonderheden over een specifieke activiteit
- de `log` voor een specifieke activiteit
- `cancel` een activiteit

**De activiteitsstroom weergeven met de Cloud CLI**:

1. Vermeld de activiteiten voor de huidige omgeving.

   ```bash
   magento-cloud activity:list
   ```

1. Elke activiteit heeft een unieke id. Selecteer een id in de vorige lijst en bekijk de details voor die activiteit.

   ```bash
   magento-cloud activity:get wvl5wm7s5vkhy
   ```

1. Bekijk het volledige logboek voor die activiteit.

   ```bash
   magento-cloud activity:log wvl5wm7s5vkhy
   ```

   Monsterrespons:

   ```bash
   Activity ID: wvl5wm7s5vkhy
   Type: environment.backup
   Description: User created a backup of Master
   Created: 2023-09-08T14:03:33+00:00
   State: complete
   Log:
   Creating backup of master
   Created backup eg5pu63egt2dcojkljalzjdopa
   ```
