---
title: Gebruikerstoegang beheren
description: Leer hoe u de toegang van gebruikers tot Adobe Commerce kunt beheren voor projecten en omgevingen met cloudinfrastructuur.
role: Admin
feature: Cloud, Roles/Permissions
last-substantial-update: 2023-06-27T00:00:00Z
topic: Security
exl-id: 3357a3ea-bf86-4a65-95d1-6b24f1152248
source-git-commit: b85a163ff62f8a63430dff7c96b5cf391cf38d79
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 0%

---

# Gebruikerstoegang beheren

Adobe Commerce-projecten voor cloudinfrastructuur maken gebruik van rolgebaseerde toegang. Er zijn twee rollen beschikbaar op het projectniveau:

- **Projectbeheerder**—Schrijf toegang tot alle projectmilieu&#39;s en kan gebruikers, duw code, en update projectmontages beheren.
- **Projectviewer**—Alleen-weergeven toegang tot alle projectomgevingen.

De kijkers van het project kunnen geen taken op om het even welk milieu uitvoeren; nochtans, kunt u projectkijkers toegang tot een specifiek milieutype verlenen schrijven.

Toegang op milieuniveau is gebaseerd op het type milieu: productie, staging en ontwikkeling. Een gebruiker verlenen _viewer_ toestemming om _ontwikkeling_ omgevingen betekent dat ze kunnen bekijken **alles** ontwikkelomgevingen in het project. In de volgende tabel worden de mogelijkheden voor elk machtigingsniveau verduidelijkt:

| Machtigingsniveau | Toegang | SSH-toegang |
| ------------------ | ----------- | :----------: |
| **Beheerder** | Voer beheerderstaken uit, zoals veranderingsmontages, dupcode, voer taken, en takbeheer uit, met inbegrip van het samenvoegen met het oudermilieu | Ja |
| **Medewerker** | Code duwen en de omgeving vertakken; kan instellingen niet wijzigen of acties uitvoeren | Ja |
| **Viewer** | Alleen-weergeven toegang tot het omgevingstype | Nee |
| **Geen toegang** | Geen toegang tot het omgevingstype | Nee |

{style="table-layout:auto"}

U kunt gebruikers toevoegen en rollen toewijzen met behulp van de `magento-cloud` CLI of de [!DNL Cloud Console].

>[!BEGINSHADEBOX]

**Vereisten:**

- Een geregistreerde gebruiker bij een Adobe ID. Een gebruiker moet [registreren voor een Adobe-account](https://account.adobe.com) en vervolgens [hun Cloud-account initialiseren](https://console.adobecommerce.com) voordat u ze aan een Cloud-project kunt toevoegen.
- Een gebruiker heeft de **Beheerder** rol kan gebruikers niet beheren met de `magento-cloud` CLI. Alleen gebruikers aan wie de **Eigenaar account** de rol kan gebruikers beheren.

>[!ENDSHADEBOX]

## Gebruikers beheren met de CLI

Gebruik de `magento-cloud` CLI voor het beheer van gebruikers en integratie met geautomatiseerde systemen:

- `magento-cloud user:add`- voeg een gebruiker aan het project toe
- `magento-cloud user:delete`-delete een gebruiker
- `magento-cloud user:list [users]`-list projectgebruikers
- `magento-cloud user:role`-view of verander de gebruikersrol
- `magento-cloud user:update`-update gebruikersrol op een project

In de volgende voorbeelden worden de `magento-cloud` CLI om een gebruiker toe te voegen, rollen te vormen, projecttaken te wijzigen, en gebruikersrollen toe te wijzen.

**Een gebruiker toevoegen en rollen toewijzen**:

1. Gebruik de `magento-cloud` CLI om de gebruiker toe te voegen.

   ```bash
   magento-cloud user:add
   ```

   >[!IMPORTANT]
   >
   >De gebruiker moet een Adobe ID hebben; zie [voorwaarden](#add-users-and-manage-access).

1. Volg de herinneringen: specificeer het gebruikers e-mailadres, plaats het project en milieu-type rollen, en voeg de gebruiker toe.

   > Voorbeeldaanwijzingen

   ```terminal
   Enter the user's email address: alice@example.com
   
   Email address: alice@example.com
   
   The user's project role can be admin (a) or viewer (v).
   
   Project role (default: viewer) [a/v]: viewer
   
   The user's environment type role(s) can be admin (a), viewer (v), contributor (c) or none (n).
   
   Role on type development (default: none) [a/v/c/n]: none
   Role on type production (default: none) [a/v/c/n]: admin
   Role on type staging (default: none) [a/v/c/n]: admin
   
   Adding the user alice@example.com to (project_id):
   Project role: viewer
     Role on type production: admin
     Role on type staging: admin
   
   Are you sure you want to add this user? [Y/n] y
   Adding the user to the project
   ```

   Nadat u de gebruiker hebt toegevoegd, stuurt Adobe een e-mail naar het opgegeven adres met instructies voor toegang tot de Adobe Commerce voor het infrastructuurproject in de cloud.

### De projectrol van een gebruiker weergeven

```bash
magento-cloud user:get alice@example.com
```

>Monsterrespons:

```terminal
Current role(s) of User (alice@example.com) on Production (project_id):
  Project role: admin
```

### Een gebruiker toevoegen aan meerdere omgevingen

Een gebruiker toevoegen als een `viewer` op `Production` milieu en als `contributor` op een `Integration` milieu:

```bash
magento-cloud user:add alice@example.com -r production:v -r integration:c
```

### Machtigingen voor de gebruikersomgeving bijwerken

Gebruikersomgevingsmachtigingen bijwerken naar `admin` op de `Production` milieu:

```bash
magento-cloud user:update alice@example.com -r production:a
```

## Gebruikers beheren vanuit de [!DNL Cloud Console]

U kunt de [[!DNL Cloud Console]](../../get-started/cloud-console.md) om machtigingen toe te voegen en de _Bewerken_ gebruiken om machtigingen voor een bestaande gebruiker te wijzigen.

>[!IMPORTANT]
>
>De gebruiker moet een Adobe ID hebben; zie [voorwaarden](#add-users-and-manage-access).

### Een gebruiker toevoegen aan het project

1. Aanmelden bij de [[!DNL Cloud Console]](https://console.adobecommerce.com/).

1. Selecteer een project in het menu _Alle projecten_ lijst.

1. Voor het dashboard van het Project, klik het configuratiepictogram in het hogere recht.

1. Onder _Projectinstellingen_, klikt u op **[!UICONTROL Access]**.

1. In de _Toegang_ weergeven, klikken **[!UICONTROL Add]**.

1. Voltooi de _[!UICONTROL Add User]_formulier:

   - Voer het e-mailadres van de gebruiker in.

   - **[!UICONTROL Project admin]**—Admin-rechten verlenen aan alle instellingen en omgevingstypen.

   - **[!UICONTROL Environment types and permissions]**—verleent toegang en specifieke toestemmingsniveaus aan bepaalde milieutypes. _Geen toegang_, _Beheerder_ (instellingen wijzigen, actie uitvoeren, code samenvoegen), _Medewerker_ (pushcode), of _Viewer_ (alleen weergeven).

   >[!TIP]
   >
   >Alleen een **Projectbeheerder** kan gebruikers in om het even welke milieu beheren. Om een gebruiker toegang te verlenen tot **Toegang** tab, andere **Projectbeheerder** of de **Eigenaar account** moet deze gebruiker de **Projectbeheerder** rol.

1. Klik op **[!UICONTROL Add User]**.

   >[!IMPORTANT]
   >
   >Het toevoegen van een gebruiker activeert niet automatisch een plaatsing.

1. Nadat u gebruikers hebt toegevoegd, implementeert u alle omgevingen opnieuw om de wijzigingen toe te passen. Het toevoegen van een gebruiker activeert niet automatisch een plaatsing. Herplaatsing is een belangrijke stap om ervoor te zorgen dat de gebruiker tot een milieu kan toegang hebben gebruikend SSH of beheerderstaken uitvoeren.

Nadat u de gebruiker hebt toegevoegd, stuurt Adobe een e-mail naar het opgegeven adres met instructies voor toegang tot de Adobe Commerce voor het infrastructuurproject in de cloud.

## Vereisten voor gebruikersverificatie

Voor extra veiligheid, verstrekt de Adobe project-vlakke multi-factor authentificatie (MFA) handhaving om twee-factor authentificatie (TFA) voor de toegang van SSH tot Adobe Commerce op de broncode en milieu&#39;s van het wolkeninfrastructuurproject te vereisen. Zie [MFA inschakelen voor SSH](multi-factor-authentication.md).

Wanneer MFA-handhaving is ingeschakeld op een Adobe Commerce op een cloudinfrastructuurproject, moeten alle gebruikers met SSH-toegang tot een omgeving in dat project TFA inschakelen op hun Adobe Commerce op een cloudinframeconferentieaccount. Voor geautomatiseerde processen kunt u een gebruiker van de computer en een API-token maken voor verificatie via de opdrachtregel.

Nadat u een gebruiker aan een Cloud-project hebt toegevoegd, vraagt u de gebruiker om de beveiligingsinstellingen van zijn account te controleren en de volgende beveiligingsconfiguraties toe te voegen, indien nodig:

- **TFA inschakelen**—Voldoe veiligheid en nalevingsnormen door tweefasenauthentificatie te vormen. Projecten geconfigureerd met [MFA-handhaving](multi-factor-authentication.md) vereisen TFA op rekeningen die SSH gebruiken om tot de projecten toegang te hebben.

- **SSH-toetsen inschakelen**—Gebruikers die toegang tot Adobe Commerce nodig hebben voor broncodeopslagplaatsen voor cloudinfrastructuren, moeten SSH-sleutels voor hun account inschakelen. Zie [Beveiligde verbindingen](../development/secure-connections.md).

- **Een API-token maken**—Gebruikers moeten een API-token genereren dat wordt gebruikt voor SSH-toegang tot een omgeving. U hebt het token nodig om verificatieworkflows voor geautomatiseerde processen in te schakelen.

  Bij projecten waarvoor MFA-handhaving is ingeschakeld, moet u het API-token gebruiken om SSH-toegangsverzoeken van geautomatiseerde accounts te verifiëren. Met het token kunnen geautomatiseerde processen verificatieworkflows omzeilen waarvoor TFA is vereist.

### TFA inschakelen voor Cloud-accounts

Adobe Commerce op cloud-infrastructuur ondersteunt TFA met een van de volgende toepassingen:

- [Google Authenticator (Android/iPhone)](https://support.google.com/accounts/answer/1066447?hl=en)
- [Autorisatie (Android/iPhone)](https://authy.com/features/)
- [FreeOTP (Android)](https://play.google.com/store/apps/details?id=org.fedorahosted.freeotp)
- [GAuth-verificator (Firefox OS, desktop, anderen)](https://github.com/gbraad-apps/gauth)

De instructies voor het installeren van de authentificatortoepassing en het toelaten van TFA zijn beschikbaar op _Accountinstellingen_ pagina in de [!DNL Cloud Console].

**TFA inschakelen op uw gebruikersaccount**:

1. Aanmelden bij [uw account](https://console.adobecommerce.com).

1. Klik in het accountmenu rechtsboven op **[!UICONTROL My Profile]**.

1. Op de _Beveiliging_ tabblad, klikt u op **[!UICONTROL Set up application]**.

1. Als u geen goedgekeurde verificatietoepassing op uw mobiele apparaat hebt, gebruikt u de gekoppelde instructies om een toepassing te installeren.

1. Voeg uw Adobe Commerce-account voor de cloud-infrastructuur toe aan de verificatietoepassing.

   - Open de verificatietoepassing op uw mobiele apparaat. Voeg vervolgens de instellingscode toe aan de toepassing.

   - In de [!UICONTROL **[!UICONTROL TFA set up - Application]**] pagina, typt u de TFA-code van uw mobiele apparaat in het dialoogvenster **[!UICONTROL Application verification code]** veld.

   - Klik op **[!UICONTROL Verify and save]**.

     Als de code geldig is, stuurt de Adobe een bericht naar het account-e-mailadres waarin wordt bevestigd dat de account nu TFA heeft.

1. Optioneel. Inschakelen _Vertrouwde browser_ instellingen om de verificatiecode gedurende 30 dagen in de browser in cache te plaatsen.

   Deze configuratie vermindert het aantal authentificatieuitdagingen tijdens projectlogin.

1. Klikken **Opslaan** of **Overslaan**.

1. Sla de herstelcodes op.

   - Op de _TFA-installatie - herstel_ codeert, kopieert en slaat de herstelcodes op, zodat u zich kunt aanmelden bij uw Adobe Commerce-project voor een cloudinfrastructuur wanneer u geen toegang hebt tot uw mobiele apparaat of verificatietoepassing.

   - Kopieer de herstelcodes naar een andere locatie of noteer deze voor het geval dat u de toegang tot uw apparaat of verificatietoepassing verliest.

   - Klikken **Opslaan** om de codes op te slaan op uw account, zodat u ze kunt bekijken en beheren vanuit de beveiligingsinstellingen van uw account.

     >[!WARNING]
     >
     >Als u toegang tot een rekening met TFA verliest en niet de lijst van terugwinningscodes hebt, moet u uw projectbeheerder contacteren, of [Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) de TFA-toepassing opnieuw instellen.

1. Na de voltooiing van de opstelling van TFA, klik **Opslaan** om uw account bij te werken.

1. Verifieer uw huidige zitting met TFA.

   - Afmelden bij uw account.
   - Meld u aan met uw gebruikersnaam en wachtwoord.
   - Voer desgevraagd de TFA-code in voor de `accounts.magento.cloud` invoer van de verificatietoepassing op uw mobiele apparaat.

### TFA-configuratie en herstelcodes beheren

U kunt de TFA-configuratie voor een Adobe Commerce op een cloud-infrastructuuraccount beheren via de _Beveiliging_ de _Mijn profiel_ pagina.

1. Aanmelden bij [uw account](https://console.adobecommerce.com).

1. Klik in het accountmenu rechtsboven op **[!UICONTROL My Profile]**.

1. Op de _Mijn profiel_ pagina, klikt u op de **[!UICONTROL Security]** tab.

1. Gebruik de beschikbare koppelingen om de TFA-instellingen voor uw Adobe Commerce bij te werken op uw account voor cloudinfrastructuur:

   - TFA uitschakelen
   - De verificatietoepassing herstellen
   - Vertrouwde browsers toevoegen of verwijderen
   - TFA-herstelcodes weergeven of vernieuwen op uw account

### Een API-token maken

Een API teken kan voor een OAuth 2 toegangsteken worden geruild, dat dan kan worden gebruikt om verzoeken voor authentiek te verklaren.

Bij projecten waarvoor MFA-handhaving is ingeschakeld, moet u een API-token hebben om SSH-toegang voor systeemgebruikers en geautomatiseerde processen mogelijk te maken.

>[!IMPORTANT]
>
>Protect API-tokenwaarden voor uw account. Stel de waarde niet beschikbaar in codesteekproeven, het scherm vangt, of onveilige cliënt-server mededelingen. Stel ook niet de waarde in broncode bloot die in openbare bewaarplaatsen wordt opgeslagen.

**Een API-token maken**:

1. Aanmelden bij [uw account](https://console.adobecommerce.com).

1. Klik in het accountmenu rechtsboven op **[!UICONTROL My Profile]**.

1. Op de _Mijn profiel_ pagina, klikt u op de **[!UICONTROL API tokens]** tab.

1. Klikken **[!UICONTROL Create API token]** en voer bijvoorbeeld een naam in die overeenkomt met de systeemgebruiker of het geautomatiseerde proces dat het API-token gebruikt.

   ![API-tokens](../../assets/api-token-name.png)

1. Klik op **[!UICONTROL Create API token]**.
