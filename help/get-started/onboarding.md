---
title: '''[!DNL Onboarding] aan de handel"'
description: Open uw cloud-account en stel een Adobe Commerce in voor een infrastructuurproject voor de cloud.
role: Admin
recommendations: noDisplay, catalog
exl-id: c6b768d7-d835-4a8d-aad9-1c0324f7570d
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# [!DNL Onboarding] aan de handel

Nadat de Adobe een Handel op het abonnement van de wolkeninfrastructuur activeert, zijn het aanvankelijke project en de codetoegang beschikbaar slechts aan de persoon die als Eigenaar van de Vergunning (de Eigenaar van de Rekening) wordt aangewezen.

De eigenaar van de licentie is de persoon in uw bedrijf of financiële organisatie die betalingen en andere zakelijke transacties voor de Adobe Commerce beheert op de account voor cloudinfrastructuur. Deze persoon fungeert als contactpunt met Adobe. Als u de Eigenaar van de Vergunning op uw rekening moet veranderen, moet u uw Team van de Rekening van de Adobe contacteren.

Als u snel aan boord van uw project wilt gaan, zodat u uw site kunt gaan ontwikkelen voor live implementatie, moet u de vereiste instellingen voltooien en [!DNL onboarding] taken. Doorgaans begint de Eigenaar van de licentie het proces door beheerdersrechten te beveiligen en gebruikers van Technical Admin aan te maken die hulp kunnen bieden bij het instellen, aanpassen en ontwikkelen.

## Aanmelden voor een Cloud-account

Als u geen Adobe Commerce hebt op een cloud-infrastructuuraccount, neemt u contact op met [Verkoop]. Wanneer u zich aanmeldt, maakt Adobe uw account en verzendt u een welkomstbericht met instructies over de toegang tot de projectinterface. Het e-mailbericht bevat een koppeling waarmee u zich kunt aanmelden bij uw account en de initiële projectinstelling kunt voltooien.

### Wolk [!DNL Onboarding] UI

De projectpagina Adobe Commerce on cloud Infrastructure in de ([!DNL Onboarding] UI) verstrekt een Getting Started checklist aan opstelling uw project en de diensten, bepaalt toegang, en wordt begonnen met ontwikkeling. Vanuit OBUI kunt u:

- Voeg een Technische Admin, een supergebruiker toe die uw project en takken kan beheren
- Heb toegang tot uw projectmilieu, met inbegrip van een verbinding aan [!DNL Cloud Console]
- Voltooi een snelle controlelijst voor gebruikersacceptatie (UAT) met koppelingen naar verdere tests

**De projectpagina openen**:

1. Aanmelden bij uw [Adobe Commerce-klantenaccount](https://account.magento.com/customer/account/login).

1. Op de _Mijn account_ pagina, klikt u op de **[!UICONTROL Commerce]** om de projecten in uw account weer te geven.

1. Klikken **Projectpagina weergeven** in de [Sectie Projecten](https://cloud.magento.com/cloud/project/).

1. Klik op de projectnaam en open de pagina Cloud Project ([!DNL Onboarding] UI).

   ![OBUI-projectpagina](../assets/onboarding-ui.png)

   Doorblader door het portaal voor nuttige informatie en opties beginnen uw project te plannen, code te ontwikkelen, en voorbereidingen te treffen voor UAT en plaatslancering.

## Project openen en gebruikers toevoegen

De Eigenaar van de Vergunning kan gebruikersrekeningen toevoegen om toegang tot code te verlenen, takken te beheren, kaartjes, en steunmilieu&#39;s in te gaan. Deze gebruikersaccounts kunnen interne ontwikkeling, consultants en oplossingsspecialisten omvatten.

Doorgaans is de enige gebruiker die de Eigenaar van de Licentie moet maken de _Technisch beheerder_. Technisch Admin heeft een gebruikersrekening met admin toegang nodig om gebruikersrekeningen voor ontwikkelaars tot stand te brengen, milieutoestemmingen te plaatsen, en alle takken en milieu&#39;s te beheren. De technische beheerder kan een ontwikkelaar, een consultant, en [Adobe Solution Partner](https://business.adobe.com/products/magento/partners.html), of uzelf.

U kunt een Technische Admin door het portaal van het Project tot stand brengen, van [!DNL Cloud Console]of vanaf de opdrachtregel met de opdracht `magento-cloud` CLI.

### Gebruikersregistratie

U kunt alleen geregistreerde gebruikers aan uw Adobe Commerce toevoegen op projecten en omgevingen met cloudinfrastructuur. Als u een nieuwe gebruiker hebt, vraagt u deze om [registreren voor een account](https://account.magento.com/customer/account/login/) en om het e-mailadres op te geven dat aan het accountprofiel is gekoppeld.

### Toegang tot gedeelde account

De eigenaar van de licentie kan gedeelde toegang instellen voor de account. Via gedeelde toegang kunnen vertrouwde medewerkers en serviceproviders het Help-centrum gebruiken om ondersteuningstickets voor uw Adobe Commerce in te dienen en bij te houden voor infrastructuurprojecten in de cloud. Zie voor installatie-instructies de [Gedeelde toegang] in het Help Center.

### [!DNL Cloud Console]

U kunt de [[!DNL Cloud Console]](cloud-console.md) om uw project te beheren, gebruikersrekeningen toe te voegen, en beginnen uw opslag te ontwikkelen. De eigenaar van de licentie, gebruikers van technisch beheer en ontwikkelaars kunnen de [!DNL Cloud Console] om alle milieu&#39;s en takken, milieuvariabelen, milieu montages, en routes te beheren.

**Als u toegang wilt krijgen tot[!DNL Cloud Console]**:

1. Aanmelden bij [Mijn account](https://account.magento.com/customer/account/login).

1. Op de _Mijn account_ pagina, klikt u op de **[!UICONTROL Commerce]** om de projecten in uw account weer te geven.

1. Klik op de knop **Projecten** en selecteert u een project.

1. Klikken **Toegang tot infrastructuur** en klik vervolgens op **Toegang tot project (webinterface)**.

   ![Cloud-projectportal](../assets/obui-project-access.png)

## Aanmelden voor status van Adobe

Updates over Adobe Commerce op omgevingen met cloudinfrastructuurplatforms en verwante services van de [Statuspagina].

De pagina biedt een status voor Adobe Commerce-componenten en -services, gevolgd door meldingen over incidentrapporten, serviceupgrades, geplande uitvallen en gepland onderhoud. Iedereen die aan uw project werkt, kan zich abonneren op de Adobe Commerce-statussite om gebeurtenismeldingen en updates via e-mail of Slack te ontvangen. U kunt uw abonnement op de status van uw Adobe aanpassen om specifieke producten op regio&#39;s en gebeurtenissen bij te houden.

>[!TIP]
>
> De nieuwe openen [!DNL Cloud Console] en project- en milieuactiviteiten te bekijken.
>
>**Volgende stap**: [Aanmelden bij Cl[!DNL ]oud Console](cloud-console.md)

<!-- link definitions -->

[Verkoop]: https://business.adobe.com/products/magento/get-demo.html
[Gedeelde toegang]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#shared-access
[Statuspagina]: https://status.adobe.com/products/503473
