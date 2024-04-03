---
title: Testinstructies
description: Lees meer over testtypen en best practices voor het starten van Adobe Commerce op cloudinfrastructuur.
exl-id: 1d7897a2-af97-46ab-89c0-2ec54284190e
source-git-commit: aae285d85188bfadd73d5b4e1fea16afa5beb117
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Testinstructies

Nadat u uw Adobe Commerce hebt geconfigureerd en aangepast voor het infrastructuurproject voor de cloud, kunt u het beste uw toepassing grondig testen voordat u de website van de winkel start. Testen helpt de verwachtingen ten aanzien van de clustergrootte op de juiste wijze te beheren en schaalt naar behoren voor toekomstige bedrijfsbehoeften.

## Functionele tests

Tijdens de ontwikkeling is het belangrijk om end-to-end functionele tests uit te voeren op uw Adobe Commerce voor het infrastructuurproject van de cloud. Zie de volgende richtlijnen voor het uitvoeren van functionele tests in de Docker-omgeving:

- **Toepassingen testen**—Gebruik de [Kader voor functionele tests van Magento&#39;s (MFTF)](https://developer.adobe.com/commerce/cloud-tools/docker/test/application-testing/) voor het testen van toepassingen in de Cloud Docker-omgeving.

- **Code testen**—Gebruik de [Codeception testing framework for PHP](https://developer.adobe.com/commerce/cloud-tools/docker/test/code-testing/) voor het valideren van code die bedoeld is voor een bijdrage aan de opslagplaatsen van Cloud-pakketten.

## Tips en trucs voor het starten

U kunt de volgende testtypen het beste gebruiken voordat u de site start:

- **Belastingtest**—Een belastingstest uitvoeren om het gedrag van het systeem onder een verwachte belasting te begrijpen. Test bijvoorbeeld een gelijktijdig aantal actieve gebruikers in de toepassing, waarbij elke gebruiker een specifiek aantal transacties binnen de ingestelde duur uitvoert. Deze test onthult de reactietijd van belangrijke zaken-kritieke transacties, zoals het gegevensbestand of het gedrag van de toepassingsserver. Een belastingstest kan helpen knelpunten op te sporen.

- **Stresstest**—De bovengrenzen van de capaciteit binnen het systeem uitdagen om te bepalen of het systeem voldoende presteert wanneer de huidige belasting ver boven het verwachte maximum ligt.

- **Beveiligingsscan**—Adobe biedt een gratis [Beveiligingsscan](../launch/overview.md#set-up-the-security-scan-tool) voor uw sites.

- **Penetratietest**—Is een toegelaten gesimuleerde cyberaanval op een computersysteem dat wordt ontworpen om de veiligheid van het systeem te evalueren. De penetratietest helpt zwakke plekken of kwetsbaarheden te identificeren, waaronder de mogelijkheid voor onbevoegde partijen om toegang te krijgen tot systeemfuncties en gegevens.

>[!WARNING]
>
>Klanten mogen geen beveiligingsbeoordelingen uitvoeren van de AWS-infrastructuur of de AWS-services zelf. Als u een beveiligingsprobleem ontdekt binnen een van de AWS-services die in uw beveiligingsevaluatie worden waargenomen, [contact opnemen met AWS Security](mailto:aws-security@amazon.com) onmiddellijk. Zie [AWS-beleid voor klanten voor het testen van pensioenen](https://aws.amazon.com/security/penetration-testing/).
