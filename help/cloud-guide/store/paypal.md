---
title: PayPal-betalingsmethoden instellen
description: PayPal-betalingsmethoden instellen voor Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Checkout, Payments
exl-id: e52fd719-f936-4e8b-8222-af133389d9e2
source-git-commit: aa1a334ca1383559194ca75247679c6fb5411802
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# PayPal-betalingsmethoden instellen

Adobe Commerce on cloud Infrastructure biedt een instaphulpmiddel om PayPal Express Checkout-accounts rechtstreeks via de beheerder te configureren. Dit gereedschap is beschikbaar voor ECE 2.1.8 en hoger. Om live te gaan en PayPal-betalingsmethoden te testen, kunt u uw PayPal Express Checkout-account inschakelen en configureren voor sandbox- of productierekeningen.

U kunt de sandbox- of productieaccount in elke omgeving configureren:

* Stel Sandbox-referenties in voor integratie- en staging-omgevingen.
* Stel voor uw productieomgeving Sandbox-referenties in voor de eerste test en vervang deze gegevens door de live productiegegevens voor een gestarte winkel.

## PayPal-rekening

Het is het beste om een PayPal Merchant-account te gebruiken dat is voorbereid en geconfigureerd, maar u kunt een account maken of een persoonlijke account upgraden via Beheer.

[!DNL PayPal onboarding] ondersteunt het verbinden met de volgende accounts:

* PayPal Business-account
* Persoonlijke PayPal-rekening, converteren naar een zakelijke account. Als u een bestaand persoonlijk PayPal-account hebt, kunt u zich aanmelden met deze gegevens en dit account upgraden naar een zakelijke account wanneer u de synchronisatie hebt voltooid.

Als u geen bestaande PayPal-rekening hebt, maakt u er een. Voer een e-mailadres in voor een nieuwe account. Als er geen overeenkomend PayPal-account wordt gevonden, volgt u de aanwijzingen om een PayPal Business-account te maken. U kunt ook rechtstreeks via [PayPal](https://www.paypal.com/us/webapps/mpp/account-selection).

### Paypal-beperkingen

PayPal biedt ondersteuning voor het verbinden van PayPal Express Checkout voor landen over de hele wereld, behalve voor de volgende beperkingen:

* India en Japan (toekomstige PayPal-updates kunnen deze accounts ondersteunen)
* Israël

Voor Brazilië moet je een bestaande PayPal-zakelijke account hebben om verbinding te maken. Tijdens dit proces kunt u geen bestaande persoonlijke PayPal-rekening voor Brazilië converteren. Als u een account nodig hebt, [een zakelijke PayPal-rekening maken](https://www.paypal.com/us/webapps/mpp/account-selection).

## PayPal Express-afhandeling configureren

PayPal Express Checkout configureren:

1. Open de Admin voor het milieu.
1. Selecteer in de navigatie aan de linkerkant de optie **Winkels** > **Configuratie** selecteert u vervolgens **Verkoop** > **Betalingsmethoden**.
1. Selecteer bij PayPal de optie **Configureren**. De gebieden van de configuratie tonen in uitbreidbare secties voor Uitdrukkelijke Afhandeling, Adverteer PayPal Krediet, en Basis en Geavanceerde montages.
1. Sluit uw Paypal-account aan. Totdat de account is verbonden, zijn de opties die moeten worden ingeschakeld uitgeschakeld. Zie voor meer informatie over beschikbare en ondersteunde accounts om verbinding te maken met en beperkingen op te geven [PayPal-rekening](#paypal-account).

   * Klik op Verbinding maken met PayPal en volg de aanwijzingen om verbinding te maken met uw PayPal-account. Aankopen door klanten met behulp van een live PayPal-rekening zijn voltooid en brengen klanten in een live winkel actief in rekening.
   * Als u uw sandboxaccount wilt koppelen voor testdoeleinden, klikt u op Sandboxreferenties en volgt u de aanwijzingen. Aankopen door klanten met behulp van een sandbox PayPal voltooid zonder klanten actief in rekening te brengen.

1. Configureer de instellingen voor Express Checkout om de PayPal-API te verifiëren en te gebruiken:

   * **E-mail gekoppeld aan PayPal Merchant Account** (Optioneel) Voer het e-mailadres in dat aan uw PayPal-zakelijke account is gekoppeld. Deze e-mail is hoofdlettergevoelig.
   * **API-verificatiemethoden** als API-handtekening of API-certificaat.
   * Gebruikersnaam, wachtwoord en handtekening van de API die zijn vastgelegd via uw Paypal-account.
   * **Sandbox-modus** Selecteer Ja of Nee om aan te geven of de ingevoerde gegevens betrekking hebben op een sandbox. Als u productiereferenties hebt ingevoerd, selecteert u Nee.
   * **API gebruikt proxy** Selecteer Ja of Nee om in te stellen of het systeem een proxyserver gebruikt om een verbinding tot stand te brengen tussen Adobe Commerce en het PayPal-betalingssysteem. Als ja, ga de volmachtsgastheer en de haven in.

1. Voor gedetailleerde informatie en stappen voor het configureren van uw account raadpleegt u [PayPal Express-afhandeling](https://docs.magento.com/user-guide/payment/paypal-express-checkout.html) Vanaf Stap 2 voltooi de vereiste instellingen.

Als de account is geconfigureerd en geverifieerd, kunt u PayPal-betalingsopties in- en uitschakelen bij Vereiste PayPal-instellingen:

* **Deze oplossing inschakelen** geeft de PayPal-betalingsmethode via de website aan klanten weer.
* **In-Context Checkout-ervaring inschakelen**
* **PayPal-krediet inschakelen** biedt klanten de mogelijkheid om PayPal-kredietfinanciering te bieden zonder extra kosten. PayPal betaalt de bestelling vooraf en verwerkt alle aflossingen voor het krediet rechtstreeks bij de klant.

## PayPal-variabelen

Als u het PayPal-programma voor instapcontrole gebruikt met Adobe Commerce op een cloudinfrastructuur, voegt u de volgende variabele toe aan de `variables:env` van de `magento.app.yaml` bestand.

```yaml
# Environment variables
variables:
  env:
    CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
```

Als u aan 2.2 van 2.1.8 of later bevordert, moet u nog deze variabele toevoegen.
