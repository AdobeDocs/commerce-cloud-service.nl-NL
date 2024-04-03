---
title: Implementatie zonder downtime
description: Leer hoe u de algemene downtime kunt verminderen bij de implementatie van Adobe Commerce op cloudinfrastructuuroplossingen.
feature: Cloud, Deploy, SCD, Themes
exl-id: ff89d2e1-dfc8-4f6d-bd98-947559af13f0
source-git-commit: 225fba1acfd8b3ce4d7ce989c7851e7b0b218680
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Implementatie zonder downtime

Adobe Commerce on cloud Infrastructure voert de toepassing uit in [_onderhoud_ mode](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html#production-mode) tijdens de opstellen fase, die uw plaats offline neemt tot de plaatsing volledig is. De tijdsduur uw plaats van de Productie is op onderhoudswijze hangt van de grootte van de plaats, het aantal veranderingen af die tijdens de plaatsing worden toegepast, en de configuratie voor statische inhoudsplaatsing. Het is mogelijk om uw project te vormen zodat het met een **nul** downtime.

Tijdens het plaatsingsproces, staan alle verbindingen voor maximaal 5 minuten het bewaren van om het even welke actieve zittingen en hangende acties, zoals het toevoegen aan karretje of controle in de rij. Na plaatsing, wordt de rij vrijgegeven en de verbindingen blijven zonder onderbreking. Om dit te gebruiken _verbindingsgreep_ tot uw voordeel en verlaag de implementatie tot _nul_ downtime, moet u uw project configureren om de meest efficiënte implementatiestrategie te gebruiken.

Gebruik de volgende stappen om de hoeveelheid tijd te verminderen die uw winkel nodig heeft om een update naar Production te implementeren:

1. [Upgrade naar `ece-tools` package](../dev-tools/install-package.md) of [de update `ece-tools` versie](../dev-tools/update-package.md)
Uw Adobe Commerce on cloud-infrastructuurproject moet beschikken over de nieuwste `ece-tools` pakket zodat u de beschikbare hulpmiddelen hebt om een optimale plaatsing te vormen. Als u over de nieuwste `ece-tools`, gaat u door met de volgende stap.

   >[!NOTE]
   >
   >Hoewel het de beste praktijk is om de nieuwste `ece-tools` pakket, de nul-onderbreking plaatsingsmethode werkt met `ece-tools` [versie 2002.0.13](../release-notes/cloud-release-archive.md#v2002013) en later.

1. [Implementatie van statische inhoud configureren](static-content.md)
Als de statische plaatsing van inhoud in de plaatsingsfase ontbreekt, wordt uw plaats geplakt op onderhoudswijze. Wanneer een mislukking tijdens de bouwstijlfase voorkomt, vermijdt het proces onderbreking omdat het nooit begint opstellen fase. [Het produceren van statische inhoud tijdens de bouwstijlfase met geminificeerde HTML](static-content.md#setting-the-scd-on-build)- ook wel de ideale status genoemd - is de optimale configuratie voor implementaties zonder downtime en _voorkomt_ downtime als er een fout optreedt.

1. [Vorm de post-opstellen haak](../application/hooks-property.md)
U moet de naimplementatiehaak vormen om de cache op te schonen en op te warmen. Door gebrek, komt het geheime voorgeheugen schoon tijdens de opstellen fase voor wanneer de plaats neer is. Als u het cachegeheugen naar de fase na implementatie verplaatst, blijft de cache actief totdat de implementatiefase is voltooid en kunt u de cache veilig opschonen.

   De lijst met pagina&#39;s aanpassen die worden gebruikt om de cache vooraf te laden met de [WARM_UP_PAGES omgevingsvariabele](../environment/variables-post-deploy.md#warmuppages).

1. [Themabestanden verkleinen](../environment/variables-deploy.md#scdmatrix)
U kunt het aantal onnodige themabestanden verminderen door de SCD\_MATRIX-omgevingsvariabele te configureren.

1. [Implementatie van statische inhoud versnellen](../environment/variables-deploy.md#scdthreads)
U kunt het plaatsingsproces versnellen door de SCD\_THREADS milieuvariabele bij te werken om het aantal draden voor statische inhoudsplaatsing te verhogen.

>[!NOTE]
>
>U kunt uw projectconfiguratie voor optimale plaatsing bevestigen door [uitvoeren van de wizard voor ideale status](smart-wizards.md#verifying-an-ideal-configuration).
