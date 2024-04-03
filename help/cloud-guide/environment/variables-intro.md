---
title: Omgevingsvariabelen
description: Zie een lijst met omgevingsvariabelen die specifiek zijn voor Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Build, Configuration, Deploy
exl-id: bfee2f69-93a6-4d26-bb9e-be8acc5673c3
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Omgevingsvariabelen

Met Adobe Commerce on cloud Infrastructure kunt u omgevingsvariabelen toewijzen om configuratieopties te overschrijven. De `ece-tools` pakket stelt waarden in in de `env.php` bestand op basis van waarden van [Cloud-variabelen](variables-cloud.md), variabelen die zijn ingesteld in het [!DNL Cloud Console]en de `.magento.env.yaml` configuratiebestand.

De omgevingsvariabelen in de `.magento.env.yaml` de Cloud-omgeving aanpassen door de bestaande Commerce-configuratie te overschrijven. Als een standaardwaarde is `Not Set`en vervolgens de `ece-tools` pakket neemt **NEE** handeling en gebruikt de [!DNL Commerce] standaard of de waarde van de `MAGENTO_CLOUD_RELATIONSHIPS` configuratie. Als de standaardwaarde is ingesteld, wordt `ece-tools` Deze standaardinstelling wordt ingesteld door het pakket.

De typen omgevingsvariabelen zijn:

- [ADMIN](variables-admin.md)—variabelen overschrijven ADMIN-variabelen van project
- [MAGENTO_CLOUD](variables-cloud.md)—specifieke variabelen voor cloudinfrastructuur
- Variabelen gebruikt in het dialoogvenster `.magento.env.yaml` bestand:
   - [Algemeen](variables-global.md)—variabelen beïnvloeden bouw, opstellen, en post-implementatiefasen
   - [Opbouwen](variables-build.md)—variabelen: besturingselementen voor het samenstellen van handelingen
   - [Implementeren](variables-deploy.md)—variabelen besturen implementatiehandelingen
   - [Na implementatie](variables-post-deploy.md)—variabelen: besturingsacties na implementatie

Variabelen zijn _hiërarchisch_, wat betekent dat als een variabele niet wordt overschreven, deze wordt overgeërfd van de bovenliggende omgeving.

U kunt instellen [ADMIN-variabelen](variables-admin.md) van de [!DNL Cloud Console] of met de Adobe Commerce CLI. U kunt andere omgevingsvariabelen beheren vanuit de [`.magento.env.yaml`](configure-env-yaml.md) bestand voor het beheer van ontwikkelings- en implementatieacties in al uw omgevingen, inclusief Pro Staging en Productie, zonder dat een ondersteuningsticket vereist is.

>[!TIP]
>
>YAML-bestanden zijn hoofdlettergevoelig en staan geen tabs toe. Wees voorzichtig met het gebruik van consistente inspringing in de gehele `.magento.env.yaml` of uw configuratie werkt mogelijk niet zoals verwacht. De voorbeelden in deze documentatie en in het voorbeeldbestand gebruiken _met twee spaties_ inspringing. Gebruik de [ece-tools validate, opdracht](configure-env-yaml.md#validate-configuration-file) om uw configuratie te controleren.
