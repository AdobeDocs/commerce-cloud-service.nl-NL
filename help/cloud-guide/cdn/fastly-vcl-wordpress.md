---
title: Reroute-aanvragen naar een CMS-backend
description: Leer hoe u binnenkomende aanvragen van een Adobe Commerce-winkel kunt omleiden naar een aparte WordPress-site met de module Snelst.
feature: Cloud, Configuration, Routes
exl-id: 5bd9c56f-4412-4643-89b6-590a8ec65ac0
source-git-commit: 7a181af2149eef7bfaed4dd4d256b8fa19ae1dda
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Reroute-aanvragen naar een CMS-backend

Reroute inkomende verzoeken van een opslag van Adobe Commerce aan een afzonderlijke plaats WordPress gebruikend de Fastly Module van Edge _Andere integratie CMS/backend_ met een Woordenboek van Edge. U kunt een gelijkaardig proces volgen om verzoeken aan andere CMS achtergronden om te leiden.

Gebruik snel Edge Modules om aangepaste VCL-code van de Admin te maken en te uploaden in plaats van de VCL-code handmatig te schrijven en te uploaden met de snelheids-API.

>[!NOTE]
>
>Wij adviseren toevoegend de configuraties van douaneVCL aan een het Opvoeren milieu waar u hen kunt testen alvorens de Fastly de dienstconfiguratie in het milieu van de Productie bij te werken.

**Eerste vereisten**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

**om verzoeken van Adobe Commerce aan WordPress** om te leiden:

1. Schakel Fastly Edge Modules in de Staging- of Productieomgeving in.

   - Meld u aan bij de beheerder.

   - Navigeer aan **Opslag** > Montages > **Configuratie** > **Geavanceerd** > **Systeem** > **Volledige het Geheime voorgeheugen van de Pagina** > **de Snelle Configuratie** > **Geavanceerde Configuratie**.

   - Plaats de waarde voor **snelste Modules van Edge** aan **ja**.

   - Sla de configuratie op.

1. Identificeer de wegen URL naar de steun WordPress terug te keren.

1. Voltooi de volgende taken om de Snelle dienst te vormen en de code van douaneVCL te creëren voor het terugsturen van verzoeken aan de achtergrond WordPress.

   - Maak een Edge-woordenboek dat de paden opgeeft die van de Adobe Commerce-winkel naar de achtergrond moeten worden omgeleid.

   - Voeg de steun WordPress aan de Fastly de dienstconfiguratie toe en maak de verzoekvoorwaarde voor URL toe herschrijft.

   - Vorm de _Andere Module van CMS/backend integratie_ Edge om URL te behandelen herschrijft van Adobe Commerce aan de WordPress achterkant.

     Voor gedetailleerde instructies, zie {de Modules van 0} Snelle Edge - Andere integratie CMS/Backend ](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-OTHER-CMS-INTEGRATION.md) in de _Snelle CDN module voor Magento 2_ documentatie.[

1. Nadat u de configuratie van de Fastly-service hebt bijgewerkt, test u de Adobe Commerce-winkel om te controleren of de opgegeven URL-aanvragen voor WordPress correct zijn uitgevoerd.
