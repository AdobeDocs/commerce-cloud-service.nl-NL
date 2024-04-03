---
title: Voorbereiden op ontwikkeling
description: Verzamel geloofsbrieven en leer over de hulpmiddelen beschikbaar aan opstelling een ontwikkelingswerkruimte voor gebruik met uw Handel op het project van de wolkeninfrastructuur.
recommendations: noDisplay, catalog
exl-id: 8f88161f-3580-453b-b977-2c6e3824cc02
source-git-commit: 85ff1283f773823ff2c6e6ab8f391fd5b4aa00e4
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Voorbereiden op ontwikkeling

Of u nu nieuw bent in de handel of een bestaande eigenaar van de handel bent die overgaat naar de cloudinfrastructuur, gebruik deze stappen voor het voorbereiden van een ontwikkelwerkruimte voor uw Cloud-project. Als u al een aantal van deze stappen hebt uitgevoerd of een bestaande Adobe Commerce-ontwikkelaarsomgeving hebt, kunt u het volgende controleren op verwachte resultaten en doorgaan met de volgende stap. Sommige configuraties en workflows verschillen van een standaardinstallatie op locatie.

## Credentials

Verzamel de volgende sleutels en accounttoegang voordat u een werkruimte instelt:

- **Verificatietoetsen (Composer-sleutels)**

  Verificatietoetsen zijn 32-teken verificatietokens die veilige toegang bieden tot de Adobe Commerce Composer-opslagplaats (`repo.magento.com`) en andere Git-services die vereist zijn voor toepassingsontwikkeling, zoals GitHub. Uw account kan meerdere verificatietoetsen hebben. Voor de opstelling van de werkruimte, begin met één specifieke sleutel voor uw codebewaarplaats. Als u geen sleutels hebt, contacteer de projecteigenaar, of creeer [verificatietoetsen](../cloud-guide/development/authentication-keys.md) uzelf.

- **Cloud Project-account**

  De eigenaar van het project moet u uitnodigen voor het Adobe Commerce-project voor cloudinfrastructuur. Wanneer u de e-mailuitnodiging ontvangt, klikt u op de koppeling en volgt u de aanwijzingen om uw account te maken. Zie [Onboarding](onboarding.md).

- **Adobe Commerce-coderingssleutel**

  Wanneer u alleen een bestaand systeem importeert, legt u de coderingssleutel vast die wordt gebruikt om uw toegang en gegevens voor de database te beveiligen. Zie voor meer informatie over deze sleutel [Problemen met coderingssleutel oplossen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolve-issues-with-encryption-key.html)

## Gereedschappen voor ontwikkelaars

- **Cloud CLI installeren**

  Installeer de `magento-cloud` CLI zodat u Cloud-omgevingen kunt beheren en automatiseringstaken kunt uitvoeren. Zie [Cloud CLI](../cloud-guide/dev-tools/cloud-cli-overview.md) voor installatie-instructies.

- **Docker installeren voor lokale ontwikkeling en tests**

  U kunt ook de Docker-omgeving gebruiken om de handel in cloudinfrastructuur na te bootsen `integration` omgeving voor lokale ontwikkeling. Er zijn drie essentiële componenten: een Adobe Commerce v2-sjabloon, een docker-compositie en `ece-tools` pakket.

   - [Docker-architectuur en algemene opdrachten](../cloud-guide/dev-tools/cloud-docker.md)
   - [Docker-ontwikkelomgeving starten](https://developer.adobe.com/commerce/cloud-tools/docker/setup/)
   - [ECE-gereedschapspakket](../cloud-guide/dev-tools/package-overview.md)

- **Git-gebaseerde services integreren**

  U kunt desgewenst een op Git gebaseerde hostingservice, zoals GitHub of GitLab, integreren met Adobe Commerce op cloudinfrastructuur. Zie [Integraties](../cloud-guide/integrations/overview.md).

## Projectcode

Een veilige verbinding is essentieel voor interactie met de externe omgeving. Voor een nieuw project: [aanmelden bij de [!DNL Cloud Console]](https://console.adobecommerce.com) en klik op **[!UICONTROL No SSH key]**. Dit pictogram is rechts van het bevelgebied en is zichtbaar wanneer het project geen sleutel van SSH bevat. Zie [Beveiligde verbindingen](../cloud-guide/development/secure-connections.md#add-an-ssh-public-key-to-your-account).

**Uw codeblok klonen naar uw lokale werkstation**:

1. In de [[!DNL Cloud Console]](https://console.adobecommerce.com), klikt u op **[!UICONTROL code]** en selecteert u de **[!UICONTROL Git]** tab.

   ![Uw code klonen](../assets/ui-git-code.png){width="450"}

1. De `git clone ...` opgegeven.

1. In een terminal, creeer en verander in uw het werk folder.

1. Plak en voer de `git clone ...` gebruiken.

>[!TIP]
>
>De Adobe voorziet uw aanvankelijke projectmilieu gebruikend een malplaatjebewaarplaats die pakketinstructies voor een specifieke versie van Adobe Commerce omvat. Controleer de [projectbestandsstructuur](../cloud-guide/project/file-structure.md) onderwerp en leer meer over belangrijke projectdossiers en wolkenmalplaatjes.
