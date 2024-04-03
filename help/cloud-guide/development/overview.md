---
title: Overzicht van ontwikkeling
description: Voorbereiden op lokale ontwikkeling met een Adobe Commerce-project voor cloudinfrastructuur.
role: Developer
feature: Cloud, Install
topic: Development
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: d4452d7d-d3dc-4f8d-8bd7-76f05d89f545
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# Overzicht van ontwikkeling

Adobe Commerce op externe omgevingen met cloudinfrastructuur **Alleen-lezen**, inclusief alle Starter-omgevingen en alle Pro-integratie-, Staging- en Productieomgevingen. In een lokale ontwikkelomgeving kunt u code schrijven en testen voordat u deze naar een integratieomgeving duwt voor verdere tests en implementatie naar Staging en Productie.

Voordat u uw lokale werkruimte gaat voorbereiden, moet u ervoor zorgen dat u beschikt over [geloofsbrieven](../../get-started/prepare-workspace.md). Voor lokale ontwikkeling is installatie van PHP en Composer vereist, tenzij u ervoor kiest om te gebruiken [Cloud Docker voor handel](#docker-environment).

## Vereiste pakketten

Adobe Commerce on cloud Infrastructure gebruikt Composer om de afhankelijkheden en upgrades voor projecten te beheren. Voor lokale ontwikkeling moet u de PHP en Composer versies installeren die compatibel zijn met uw Cloud project. Als u bijvoorbeeld de opdracht [!DNL Commerce] 2.4.6 cloudsjabloon: [`.magento.app.yaml`](https://github.com/magento/magento-cloud/blob/2.4.6/.magento.app.yaml) configuratiebestand gebruikt **PHP 8.2** en **Composer 2.2.21**.

Composer installeert de vereiste bibliotheken en afhankelijkheden voor uw project in de `vendor` directory. De volgende vereiste Composer-bestanden bevinden zich in de hoofdmap van het project:

- `composer.json`—Gebruik de `composer.json` bestand voor het beheer van productinstallaties en upgrades.
- `composer.lock`—De `composer.lock` het dossier slaat een reeks nauwkeurige versiegebiedsdelen op die aan de versiebeperkingen van elk vereiste voor elk pakket in de gebiedsdeelboom van het project voldoen.

**Algemene opdrachten:**

| Opdracht | Beschrijving |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `composer update` | Updates van de recentste versies van de gebiedsdelen die in worden weerspiegeld `composer.json` bestand. Hiermee werkt u de `composer.lock` bestand. |
| `composer install` | Leest de `composer.lock` bestand om afhankelijkheden te downloaden. Het is aan te raden een bijgewerkt exemplaar van `composer.lock` in uw projectopslagplaats. |

{style="table-layout:auto"}

Zodra u toevoegt, begaat, en duw de bijgewerkte code, stelt het plaatsingsproces automatisch in werking `composer install` tijdens de [bouwfase](../deploy/process.md#build-phase-build-phase).

### Cloud-pakket

Adobe Commerce on cloud-infrastructuur gebruikt een pakket metapakketten dat `magento/product-enterprise-edition`. Gebruik de volgende beperkingssyntaxis om de nieuwste updates voor de nieuwste versie van Handel te verkrijgen:

```text
>=current_version <next_version
```

Als u bijvoorbeeld de nieuwste Adobe Commerce-versie 2.4.5 wilt gebruiken, stelt u `2.4.5` als de &quot;huidige&quot; versie en `2.4.6` als de &quot;volgende&quot; versie in het dialoogvenster `composer.json` bestand:

```text
"magento/magento-cloud-metapackage": ">=2.4.5 <2.4.6"
```

De belangrijkste pakketten van deze metapakket zijn:

- **leverancier/magento/ece-tools**—De `ece-tools` -pakket is compatibel met Adobe Commerce versie 2.1.4 en hoger en biedt een uitgebreide set functies die u kunt gebruiken om uw Adobe Commerce te beheren voor een infrastructuurproject in de cloud. Het bevat scripts en Adobe Commerce op instructies voor de cloud-infrastructuur die zijn ontworpen om u te helpen uw code te beheren en automatisch uw projecten te maken en te implementeren. Zie de [`ece-tools` pakketoverzicht](../dev-tools/package-overview.md).
- **leverancier/magento/product-enterprise-editie**—Dit metapakket vereist toepassingscomponenten, met inbegrip van modules, kaders, thema&#39;s, en meer.
- **leverancier/faals2/magento2**—Deze module beheert snel CDN en de diensten voor de Pro het Staging en Productie en de milieu&#39;s van de Productie van de Starter. Zie [Sneldiensten](/help/cloud-guide/cdn/fastly.md#fastly-cdn-module-for-magento-2).
- **leverancier/magento/module-paypal-on-boarding**—Deze module biedt PayPal-betalingsgateway-afhandeling door verbinding te maken met je PayPal-handelsaccount. Zie [PayPal on-boarding tool](../store/paypal.md).

>[!TIP]
>
>Zie [Cloudpakketten voor Adobe Commerce](/help/cloud-guide/release-notes/cloud-packages.md) in de _Opmerkingen bij de handelsversie_ voor een lijst van afhankelijkheden en licenties van derden.

## Dockingomgeving

Met het gereedschap Cloud Docker for Commerce kunt u de Adobe Commerce emuleren voor productie- en ontwikkelomgevingen van cloudinfrastructuur voor lokale ontwikkeling. In Cloud Docker for Commerce hoeven PHP en Composer niet lokaal te zijn geïnstalleerd.

- [Lokale ontwikkeling met Cloud Docker](https://developer.adobe.com/commerce/cloud-tools/docker/setup/) op de Adobe Developer-site
- [Docker-architectuur en algemene opdrachten](../dev-tools/cloud-docker.md)
- [Opmerkingen bij de release Cloud Docker](../release-notes/cloud-docker.md)

>[!TIP]
>
>Voor informatie over het gebruik van Git-gebaseerde hostingservices met Adobe Commerce op cloudinfrastructuur raadpleegt u [Integraties](../integrations/overview.md).
