---
title: New Relic-service
description: Meer informatie over de New Relic-service die beschikbaar is bij uw Adobe Commerce-project voor cloudinfrastructuur.
feature: Cloud, Observability
last-substantial-update: 2023-09-06T00:00:00Z
exl-id: 613f0694-5338-4037-8ee4-ac5eca376159
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Overzicht van New Relic-services

Alle Adobe Commerce-projecten op het gebied van cloudinfrastructuur bieden toegang tot de New Relic-service om de prestaties te controleren en gebeurtenissen van de [!DNL Commerce] toepassings- en cloudinfrastructuur.

De volgende New Relic-functies zijn beschikbaar voor gebruik in Productie- en Staging-omgevingen:

- [NEW RELIC APM](#new-relic-apm) (Pro en Starter)
- [New Relic-infrastructuur](#new-relic-infrastructure) (Alleen Pro)
- [New Relic-logbeheer](#new-relic-logs) (Alleen Pro)

>[!INFO]
>
>Andere New Relic-functies zijn niet beschikbaar voor Adobe Commerce-projecten.

## NEW RELIC APM

[New Relic for application performance management (APM)](https://docs.newrelic.com/introduction-apm/) is een product voor softwareanalyse dat u helpt toepassingsinteracties te analyseren en te verbeteren. New Relic APM is beschikbaar voor alle Adobe Commerce voor cloud-infrastructuurprojecten en biedt de volgende functies:

- **Focus op specifieke transacties**—U kunt actief belangrijke acties van klanten op uw site markeren en controleren, zoals toevoegen aan het winkelwagentje, uitchecken of een betaling verwerken.
- **Controle van databasequery**—Zoek en controleer databasequery&#39;s die de prestaties beïnvloeden.
- **Toepassingskaart**—Bekijk alle toepassingsgebiedsdelen binnen uw plaats, uitbreidingen, en de externe diensten.
- **[!DNL Apdex]scores**—Evalueer de prestaties en maak waarschuwingen om problemen op te sporen en meld u wanneer deze zich voordoen, zoals de prestaties van de site die worden beïnvloed door een flash-verkoop of een webgebeurtenis. Zie [Apdex score](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction/).
- **Beheerde waarschuwingen voor Adobe Commerce**- Gebruik dit New Relic-waarschuwingsbeleid om de prestaties van toepassingen en infrastructuren te controleren op basis van best practices uit de branche. Zie [Prestaties bewaken met de beheerde waarschuwingen voor het Adobe Commerce-waarschuwingsbeleid](investigate-performance.md/#monitor-performance-with-managed-alerts).
- **Implementaties bijhouden**—Implementatiegebeurtenissen bewaken en de gevolgen van de implementatie voor de algehele prestaties analyseren. Zie [Implementaties bijhouden](track-deployments.md).

Uw Adobe Commerce on cloud-infrastructuurproject bevat de software voor de New Relic APM-service, samen met een licentiecode. U hoeft geen extra software aan te schaffen of te installeren.

## New Relic-infrastructuur

Pro-projecten bevatten de [New Relic Infrastructure (NRI)](https://docs.newrelic.com/docs/infrastructure/infrastructure-monitoring/get-started/get-started-infrastructure-monitoring/) service, die automatisch verbinding maakt met de toepassingsgegevens en prestatieanalyses voor dynamische serverbewaking. Deze service is beschikbaar in Pro Production- en Staging-omgevingen.

## New Relic-logbeheer

Alle cloud-infrastructuurprojecten omvatten [New Relic-logbeheer](log-management.md). De dienst wordt pre-gevormd om alle logboekgegevens van uw het Opvoeren en milieu&#39;s van de Productie samen te voegen en het in een gecentraliseerd logboekbeheersdashboard te tonen.
