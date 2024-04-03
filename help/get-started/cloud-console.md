---
title: "Aanmelden bij [!DNL Cloud Console]"
description: Meer informatie over de [!DNL Cloud Console] voor Adobe Commerce on Cloud-infrastructuur.
recommendations: noDisplay, catalog
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: c19a36b6-e5e8-461c-a82c-68b7bf121999
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---


# Aanmelden bij [!DNL Cloud Console]

De [!DNL Cloud Console] verstrekt interactieve methodes om, code van de Handel te bouwen te beheren en op te stellen. De [!DNL Cloud Console] is een modernere, gebruiksvriendelijke ervaring en vormt de basis voor toekomstige interfaceverbeteringen.

[Aanmelden bij de [!DNL Cloud Console]](https://console.adobecommerce.com) om uw projectlijst te bekijken.

![Projectlijst](../assets/ui-allprojects-list.png)

## Functies

De nieuwe of verbeterde functies zijn onder meer:

- Duidelijk overzicht van project en milieu kenmerken
- Activiteitsstroom met sorteerbare geschiedenis
- Handmatig back-upbeheer en geschiedenis voor Starter-projecten
- Verbeterde logweergaven
- Sorteerbare lijsten
- Eenvoudige formulieren en richtlijnen voor het toevoegen van integratie
- WCAG-compatibiliteit (Web Content Accessibility Guidelines)

![[!DNL Cloud Console]](../assets/CloudConsole.svg)

De nieuwe of verbeterde functies zijn als volgt:

| Functie | Verbeteringen |
| -------------- | ----------------------------------- |
| [Activiteitenstroom](../cloud-guide/project/activity-stream.md) | Communiceer met een sorteerbare lijst met actieve, hangende of historische handelingen. Selecteer een activiteit en bekijk logboeken of annuleer een lopende bouwstijl. |
| [Overzichten van project en omgeving](../cloud-guide/project/overview.md#project-overview) | Open uw project en zie het overzicht van projectdetails en milieulijst. Het overzicht van het milieu verstrekt meer details over de milieustatus, toepassingstoegang, en recente activiteiten. |
| [Integratieformulieren](../cloud-guide/integrations/overview.md) | Gebruik eenvoudige formulieren en richtlijnen om integraties toe te voegen, zoals meldingen over bitmaps of Slacks. |
| [Projectlijst](../cloud-guide/project/overview.md#cloud-console) | De _Alle projecten_ in de weergave worden alle projecten weergegeven waartoe u toegang hebt. U kunt op **[!UICONTROL Show filters]** en filtert uw projectlijst door type, gebied, of plan. |
| [Zichtbaarheidsopties voor variabelen](../cloud-guide/environment/variable-levels.md) | Beperk de zichtbaarheid van een variabele op projectniveau of op milieuniveau tijdens het maken of uitvoeren. |

<!-- The following are features yet to be activated:
| **Apps and services topology** | The Apps & Services topology is visible on Project and Environment views. This interactive diagram allows you to select a service and view the relationship details, such as name, type, version, port, and more. Click **[!UICONTROL View details]** to access the overview and configuration panel for each service. | -->

## Console-vragen

**_Waar kan ik de functie Momentopnamen vinden_**?

Voor [!DNL Starter] projecten, wordt de eigenschap van Momentopnamen nu genoemd _Back-ups_. U kunt een handmatige back-up van uw [!DNL Starter] milieu van de [!DNL Cloud Console] of maak een opname via de Cloud CLI. U moet een beheerdersrol voor het milieu hebben.

Selecteer een omgeving in de projectnavigatiebalk. De omgeving moet actief zijn. Selecteer de **[!UICONTROL Backups]** tab. Deze optie is momenteel niet beschikbaar voor Pro-omgevingen.

**_Waar is de lijst van gevormde routes voor het milieu_**?

U kunt de lijst van gevormde routes op vinden _Services_ voor een omgeving.

Selecteer een omgeving in de projectnavigatiebalk. Selecteer de **[!UICONTROL Services]** tab. De **Router** het overzicht toont de gevormde routes. U kunt op dit moment geen route toevoegen uit het nieuwe [!DNL Cloud Console].

## Het menu Account

In de rechterbovenhoek bevindt zich het accountmenu. Klik op de pijl omlaag voor het menu en selecteer **[!UICONTROL My Profile]**. In de _Mijn profiel_ kunt u uw gebruikersgegevens en weergave-instellingen beheren [beveiligingsverificatie](../cloud-guide/project/user-access.md#user-authentication-requirements), [API-tokens](../cloud-guide/project/user-access.md#create-an-api-token), en [SSH-toetsen](../cloud-guide/development/secure-connections.md).
