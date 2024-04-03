---
title: ADMIN-variabelen
description: Zie een lijst met omgevingsvariabelen die worden gebruikt bij de installatie van Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Configuration, Install, Roles/Permissions
role: Developer
exl-id: 2829a9dc-40bb-4665-886e-a56d98468fc1
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Beheerdersvariabelen

De gebruikers die administratieve toegang tot Adobe Commerce op het project van de wolkeninfrastructuur hebben kunnen de volgende variabelen van het projectmilieu gebruiken om de configuratiemontages voor de administratieve gebruikersrekening met voeten te treden om tot Admin UI toegang te hebben.

## Beheerdersreferenties

U kunt de geloofsbrieven van de Gebruiker Admin tijdens de installatie van de Handel met de variabelen van ADMIN in de volgende lijst met voeten treden.

Als u de waarden na installatie wilt wijzigen, maakt u verbinding met uw omgeving met behulp van SSH en gebruikt u de Adobe Commerce CLI [`admin:user` command](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/admin.html) om de Admin-gebruikersgegevens te maken of te bewerken.

| Variabele | Standaard | Beschrijving |
| -------------- | --------------------------- | ----------- |
| `ADMIN_USERNAME` | E-mailadres eigenaar licentie | Een gebruikersnaam voor de administratieve gebruiker met de capaciteit om andere gebruikers, met inbegrip van administratieve gebruikers tot stand te brengen. |
| `ADMIN_EMAIL` |                             | E-mailadres voor de beheerder. Dit adres wordt gebruikt om meldingen voor het opnieuw instellen van wachtwoorden te verzenden. |
| `ADMIN_PASSWORD` |                             | Wachtwoord voor de administratieve gebruiker. Wanneer het project wordt gecreeerd, wordt een willekeurig wachtwoord geproduceerd en een e-mail verzonden naar de Eigenaar van de Vergunning. Tijdens het maken van een project had de eigenaar van de licentie het wachtwoord al moeten wijzigen. Neem contact op met de eigenaar van de licentie voor het bijgewerkte wachtwoord. |
| `ADMIN_LOCALE` | `en_US` | De standaardlandinstelling die door de beheerder wordt gebruikt. |

## URL van beheerder

Gebruik de volgende omgevingsvariabele om de toegang tot uw beheerinterface te beveiligen. Indien opgegeven, overschrijft deze waarde de standaard-URL tijdens de installatie.

`ADMIN_URL`—De relatieve URL voor toegang tot de beheerinterface. De standaard-URL is `/admin`. Om veiligheidsredenen raadt de Adobe u aan de standaardinstelling te wijzigen in een unieke, aangepaste Admin-URL die niet gemakkelijk te raden is.

### De URL van de beheerder wijzigen

Adobe raadt u aan de variabele op milieuniveau voor de URL van Admin na installatie te wijzigen. Configureer deze instelling om beveiligingsredenen voordat u vertakt vanuit de gekloonde `master` milieu. Alle vertakkingen die zijn gemaakt met de `master` de tak erft de milieu-vlakke variabelen en hun waarden.

Gebruik de `magento-cloud variable:update` gebruiken om de waarde van de variabele bij te werken. (De `variable:set` is vervangen en is niet beschikbaar.) In het volgende voorbeeld wordt de ADMIN_URL bijgewerkt naar `newAdmin_A8v10`:

```bash
magento-cloud variable:update ADMIN_URL --value newAdmin_A8v10 -e master
```

>[!NOTE]
>
>De `ADMIN_URL` Deze waarde accepteert letters (a-z of A-Z), getallen (0-9) en het onderstrepingsteken (_) voor een aangepast beheerpad. Spaties of andere tekens zijn **niet** aanvaard.

**Als u de URL wilt wijzigen met de opdracht[!DNL Cloud Console]**:

1. Aanmelden bij de [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Selecteer een project in het menu _Alle projecten_ lijst.

1. In het projectoverzicht, selecteer het milieu en klik het configuratiepictogram.

   ![Projectconfiguratie](../../assets/icon-configure.png){width="36"}

1. Selecteer de **Variabelen** tab.

1. Klikken **Variabele maken**.

1. Voer het volgende in:

   - **Naam variabele** = `ADMIN_URL`
   - **value** = Nieuwe URL. Stel bijvoorbeeld de URL van de beheerder in op `magento_A8v10`.

   Standaard, `Available during runtime` en `Make inheritable` zijn geselecteerd.

1. Klikken **Variabele maken** en wacht tot de implementatie is voltooid. Deze knop is alleen zichtbaar wanneer de vereiste velden waarden bevatten.
