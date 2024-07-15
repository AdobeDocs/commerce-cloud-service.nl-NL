---
title: '[!DNL Onboarding] naar Commerce'
description: Open uw cloud-account en stel een Adobe Commerce in voor een infrastructuurproject voor de cloud.
role: Admin
recommendations: noDisplay, catalog
exl-id: c6b768d7-d835-4a8d-aad9-1c0324f7570d
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# [!DNL Onboarding] naar Commerce

Nadat de Adobe een Commerce op het abonnement van de wolkeninfrastructuur activeert, zijn het aanvankelijke project en de codetoegang beschikbaar slechts aan de persoon die als Eigenaar van de Vergunning (de Eigenaar van de Rekening) wordt aangewezen.

De eigenaar van de licentie is de persoon in uw bedrijf of financiële organisatie die betalingen en andere zakelijke transacties voor de Adobe Commerce beheert op de account voor cloudinfrastructuur. Deze persoon fungeert als contactpunt met Adobe. Als u de Eigenaar van de Vergunning op uw rekening moet veranderen, moet u uw Team van de Rekening van de Adobe contacteren.

Als u snel aan boord van uw project wilt gaan, zodat u uw site kunt gaan ontwikkelen voor live implementatie, moet u de vereiste instellingen en [!DNL onboarding] taken uitvoeren. Doorgaans begint de Eigenaar van de licentie het proces door beheerdersrechten te beveiligen en gebruikers van Technical Admin aan te maken die hulp kunnen bieden bij het instellen, aanpassen en ontwikkelen.

## Aanmelden voor een Cloud-account

Als u geen Adobe Commerce op de rekening van de wolkeninfrastructuur hebt, contacteer [ Verkoop ]. Wanneer u zich aanmeldt, maakt Adobe uw account en verzendt u een welkomstbericht met instructies over de toegang tot de projectinterface. Het e-mailbericht bevat een koppeling waarmee u zich kunt aanmelden bij uw account en de initiële projectinstelling kunt voltooien.

### UI voor cloud [!DNL Onboarding]

Adobe Commerce op de pagina van het Project van het Project van de wolkeninfrastructuur in ([!DNL Onboarding] UI) verstrekt een Begonnen het Begeleidende controlelijst aan opstelling uw project en de diensten, bepaalt toegang, en begint met ontwikkeling. Vanuit OBUI kunt u:

- Voeg een Technische Admin, een supergebruiker toe die uw project en takken kan beheren
- Toegang tot uw projectomgeving, inclusief een koppeling naar de [!DNL Cloud Console]
- Voltooi een snelle controlelijst voor gebruikersacceptatie (UAT) met koppelingen naar verdere tests

**om de projectpagina** te openen:

1. Login aan uw [ de klantenrekening van Adobe Commerce ](https://account.magento.com/customer/account/login).

1. Op de _Mijn pagina van de Rekening_, klik het **[!UICONTROL Commerce]** lusje om de projecten in uw rekening te zien.

1. Klik **de Pagina van het Project van de Mening** in de [ sectie van Projecten ](https://cloud.magento.com/cloud/project/).

1. Klik de projectnaam en open de pagina van het Project van de Wolk ([!DNL Onboarding] UI).

   ![ OBUI projectpagina ](../assets/onboarding-ui.png)

   Doorblader door het portaal voor nuttige informatie en opties beginnen uw project te plannen, code te ontwikkelen, en voorbereidingen te treffen voor UAT en plaatslancering.

## Project openen en gebruikers toevoegen

De Eigenaar van de Vergunning kan gebruikersrekeningen toevoegen om toegang tot code te verlenen, takken te beheren, kaartjes, en steunmilieu&#39;s in te gaan. Deze gebruikersaccounts kunnen interne ontwikkeling, consultants en oplossingsspecialisten omvatten.

Typisch, is de enige gebruiker de Eigenaar van de Vergunning moet tot stand brengen _Technische Admin_. Technisch Admin heeft een gebruikersrekening met admin toegang nodig om gebruikersrekeningen voor ontwikkelaars tot stand te brengen, milieutoestemmingen te plaatsen, en alle takken en milieu&#39;s te beheren. Technisch Admin kan een ontwikkelaar, een adviseur, een [ Partner van de Oplossing van de Adobe ](https://business.adobe.com/products/magento/partners.html), of uzelf zijn.

U kunt een Technische Admin door het Portaal van het Project, van [!DNL Cloud Console], of van de bevellijn tot stand brengen gebruikend `magento-cloud` CLI.

### Gebruikersregistratie

U kunt alleen geregistreerde gebruikers aan uw Adobe Commerce toevoegen op projecten en omgevingen met cloudinfrastructuur. Als u een nieuwe gebruiker hebt, vraag hen om [ register voor een rekening ](https://account.magento.com/customer/account/login/) en om het e-mailadres te verstrekken verbonden aan hun rekeningsprofiel.

### Toegang tot gedeelde account

De eigenaar van de licentie kan gedeelde toegang instellen voor de account. Via gedeelde toegang kunnen vertrouwde medewerkers en serviceproviders het Help-centrum gebruiken om ondersteuningstickets voor uw Adobe Commerce in te dienen en bij te houden voor infrastructuurprojecten in de cloud. Voor opstellingsinstructies, zie het [ Gedeelde artikel van de Toegang ] in het Centrum van de Hulp.

### [!DNL Cloud Console]

U kunt [[!DNL Cloud Console]](cloud-console.md) gebruiken om uw project te beheren, gebruikersrekeningen toe te voegen, en beginnen uw opslag te ontwikkelen. De Eigenaar van de Vergunning, de gebruikers van Technische Admin, en de ontwikkelaars kunnen [!DNL Cloud Console] gebruiken om alle milieu&#39;s en takken, milieuvariabelen, milieu montages, en routes te beheren.

**om tot[!DNL Cloud Console]** toegang te hebben:

1. Login aan [ Mijn rekening ](https://account.magento.com/customer/account/login).

1. Op de _Mijn pagina van de Rekening_, klik het **[!UICONTROL Commerce]** lusje om de projecten in uw rekening te zien.

1. Klik het **lusje van Projecten** en selecteer een project.

1. Klik **toegang van de Infrastructuur**, en klik dan **Toegang van het Project (Web UI)**.

   ![ het projectportaal van de Wolk ](../assets/obui-project-access.png)

## Aanmelden voor status van Adobe

Krijg updates over Adobe Commerce op het platformmilieu&#39;s van de wolkeninfrastructuur en de verwante diensten van de [ pagina van de Status ].

De pagina biedt een status voor Adobe Commerce-componenten en -services, gevolgd door meldingen over incidentrapporten, serviceupgrades, geplande uitvallen en gepland onderhoud. Iedereen die aan uw project werkt, kan zich abonneren op de Adobe Commerce-statussite om gebeurtenismeldingen en updates via e-mail of Slack te ontvangen. U kunt uw abonnement op de status van uw Adobe aanpassen om specifieke producten op regio&#39;s en gebeurtenissen bij te houden.

>[!TIP]
>
> Open de nieuwe [!DNL Cloud Console] en bekijk project- en omgevingsactiviteiten.
>
>**Volgende stap**: [ Login aan Cl [!DNL ]oud Console ](cloud-console.md)

<!-- link definitions -->

[Verkoop]: https://business.adobe.com/products/magento/get-demo.html
[Gedeelde toegang]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#shared-access
[Statuspagina]: https://status.adobe.com/products/503473
