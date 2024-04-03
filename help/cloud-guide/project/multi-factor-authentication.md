---
title: Meervoudige verificatie voor SSH-toegang inschakelen
description: Leer hoe u de verificatievereisten voor SSH-toegang tot Adobe Commerce in cloudinframingevingen beheert.
feature: Cloud, Security
topic: Security
exl-id: 754b2c22-f197-49be-a699-fb3bedf053fc
source-git-commit: ec1e59c3aafae6452ad1590fdb9de37c68b94ed9
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 0%

---

# Meervoudige verificatie voor SSH-toegang inschakelen

Voor extra beveiliging biedt Adobe Commerce op cloudinfrastructuur multifactorverificatie (MFA)-handhaving om de verificatievereisten voor SSH-toegang tot cloudomgevingen te beheren.

Wanneer MFA op een project wordt toegelaten, vereisen alle gebruikersrekeningen met de toegang van SSH of een twee-factor authentificatie (TFA) code of een API teken en het certificaat van SSH om tot het milieu toegang te hebben.

>[!NOTE]
>
>MFA is niet standaard ingeschakeld voor Cloud-projecten. De eigenaar van de account voor het Adobe Commerce-infrastructuurproject voor cloud [Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om het mogelijk te maken. Wanneer MFA wordt toegelaten, moeten alle gebruikers dubbel-factor authentificatie (TFA) hebben die op hun Adobe Commerce op de rekening van de wolkeninfrastructuur voor de toegang van SSH tot de projectmilieu&#39;s wordt toegelaten.

## Certificaten voor SSH-toegang

Met MFA kunnen gebruikers een OAUTH-toegangstoken uitwisselen met een kortstondig SSH-certificaat dat is gegenereerd door de Adobe Cloud Certifier API. Als de gebruiker de rol Admin of Medewerker, een geldige SSH-sleutel en een geldige TFA-code of API-token heeft, gebruikt Adobe Commerce op de cloud-infrastructuur deze referenties om het tijdelijke SSH-certificaat te genereren. De vervaldatum van het certificaat wordt ingesteld op één uur, maar wordt tijdens de huidige sessie automatisch vernieuwd.

Na het registreren in een project met MFA, moeten de gebruikers gebruiken `magento-cloud` CLI voor het genereren van het SSH-certificaat:

```bash
magento-cloud ssh-cert:load
```

De `ssh-cert:load` het bevel produceert het certificaat van SSH en installeert het in de agent van SSH van de lokale gebruiker.

### Certificaat automatisch genereren bij aanmelden

U kunt uw lokale milieu vormen om het certificaat van SSH automatisch te produceren wanneer u aan verifieert `magento-cloud` CLI.

**Automatisch genereren van SSH-certificaat toevoegen aan uw `magento-cloud` CLI-configuratie**:

1. Maak op uw lokale werkstation een bestand met de naam `config.yaml` in de `.magento-cloud` in uw thuismap als deze niet bestaat.

   ```bash
   touch ~/.magento-cloud/config.yaml
   ```

1. Voeg de volgende configuratie aan toe `config.yaml` bestand.

   ```yaml
   api:
      auto_load_ssh_cert: true
   ```

1. Gebruik de `magento-cloud` CLI voor opnieuw verifiëren:

   >Afmelden:

   ```bash
   magento-cloud logout
   ```

   >Aanmelden:

   ```bash
   magento-cloud login
   ```

   >Volg het antwoord:

   ```terminal
   Please open the following URL in a browser and log in:
   http://127.0.0.1:5000
   
   Help:
     Leave this command running during login.
     If you need to quit, use Ctrl+C.
   
     To log in using an API token, run: magento-cloud auth:api-token-login
   
   Login information received. Verifying...
   You are logged in.
   
   Generating SSH certificate...
   A new SSH certificate has been generated.
   It will be automatically refreshed when necessary.
   The certificate is included in your SSH configuration: /Users/<user-name>/.ssh/config
   ```

## Verbinding maken met een omgeving die SSH gebruikt met TFA

Wanneer MFA op een project wordt toegelaten, moet u TFA op uw rekening worden toegelaten alvorens u met een verre milieu kunt verbinden gebruikend SSH. Zie [TFA inschakelen](user-access.md#enable-tfa-for-cloud-accounts).

>[!BEGINSHADEBOX]

**Vereisten:**

Voor projecten die met MFA handhaving worden toegelaten, vereist de toegang van SSH de volgende toestemmingen en rekeningsmontages:

- [Toegang tot de omgeving voor beheerders of contribuanten](user-access.md)
- [SSH-toegangstoets geconfigureerd voor account](../development/secure-connections.md#add-an-ssh-public-key-to-your-account)
- [TFA ingeschakeld op account](user-access.md#enable-tfa-for-cloud-accounts)

>[!ENDSHADEBOX]

**Om het gebruiken van SSH met de geloofsbrieven van de gebruikersrekening van TFA te verbinden**:

1. Aanmelden bij [uw account](https://console.adobecommerce.com).

1. Gebruik op uw lokale werkstation de `magento-cloud` CLI om het SSH-certificaat te genereren.

   ```bash
   magento-cloud ssh-cert:load
   ```

   > Monsterrespons:

   ```terminal
   Generating SSH certificate...
     Expires at: 2020-07-13T15:28:13-04:00
     Multi-factor authentication: verified
     Mode: interactive
   The certificate will be automatically refreshed when necessary.
   Checking SSH configuration file: /Users/<user-name>/.ssh/config
   Do you want to update the file automatically? [Y/n] Y
   Configuration file updated successfully: /Users/<user-name>/.ssh/config
   ```

1. Gebruik een SSH om verbinding te maken met de externe omgeving.

   ```bash
   ssh abcdef7uyxabce-master-7rqtwti--mymagento@ssh.us-5.magento.cloud
   ```

   ```terminal
    __  __                   _          ___ _             _
   |  \/  |__ _ __ _ ___ _ _| |_ ___   / __| |___ _  _ __| |
   | |\/| / _` / _` / -_) ' \  _/ _ \ | (__| / _ \ || / _` |
   |_|  |_\__,_\__, \___|_||_\__\___/  \___|_\___/\_,_\__,_|
               |___/
   
    Welcome to Magento Cloud.
   
    This is environment master-7rqtwti
    of project abcdef7uyxabce.
   
   web@mymagento.0:~$
   ```

## Broncode beheren met behulp van SSH met TFA

Wanneer u broncode voor Adobe Commerce beheert voor cloud-infrastructuurprojecten, gebruikt u SSH om te verifiëren bij de Git-opslagplaats voor het project. Als voor uw project de MFA-handhaving is ingeschakeld, moet u een SSH-certificaat genereren voordat u opdrachtregelbewerkingen kunt uitvoeren met behulp van de Git-gegevensopslagruimte.

**Om het gebruiken van SSH met de geloofsbrieven van de gebruikersrekening van TFA te verbinden**:

1. Aanmelden bij [uw account](https://console.adobecommerce.com) en verifiëren met TFA.

   >[!NOTE]
   >
   >Als u geen TFA hebt toegelaten op uw rekening, moet u het toelaten. Zie [TFA inschakelen op cloudaccounts](user-access.md#enable-tfa-for-cloud-accounts).

1. Gebruik op uw lokale werkstation de `magento-cloud` CLI om het SSH-certificaat te genereren.

   ```bash
   magento-cloud ssh-cert:load
   ```

   > Monsterrespons:

   ```terminal
   Generating SSH certificate...
     Expires at: 2020-07-13T15:28:13-04:00
     Multi-factor authentication: verified
     Mode: interactive
   The certificate will be automatically refreshed when necessary.
   Checking SSH configuration file: /Users/<user-name>/.ssh/config
   Do you want to update the file automatically? [Y/n] Y
   Configuration file updated successfully: /Users/<user-name>/.ssh/config
   ```

1. Kloont de Git-opslagplaats voor uw projectomgeving:

   ```bash
   git clone --branch integration abcdef7uyxabce@git.us-3.magento.cloud:abcdef7uyxabce.git myproject
   ```

   > Monsterrespons:

   ```terminal
   Cloning into 'myproject'...
   Connection to git.us-3.magento.cloud port 22 [tcp/ssh] succeeded!
   remote: counting objects: 22, done.
   Receiving objects: 100% (22/22), 82.42 KiB | 16.48 MiB/s, done.
   ```

## Verbinding maken met een omgeving die SSH gebruikt met een API-token

Wanneer MFA op een project wordt toegelaten, vereisen de geautomatiseerde processen die de toegang van SSH tot een milieu van de Wolk vereisen een API teken. U kunt het token genereren via een Adobe Commerce op een cloud-infrastructuuraccount met toegang tot Admin of Contributor voor het project.

Voor verificatie met een API-token moet nog steeds een SSH-certificaat worden gegenereerd. Geautomatiseerde processen moeten ook de productie van een SSH-certificaat automatiseren.

>[!BEGINSHADEBOX]

**Vereisten:**

- [Toegang tot de Adobe Commerce voor beheerders of contribuanten in de cloud-infrastructuur](user-access.md)
- [Geldige API-token beschikbaar voor account](user-access.md#create-an-api-token)

>[!ENDSHADEBOX]

**Verbinding maken met SSH via een API-tokenreferentie**:

1. Meld u aan bij het Cloud-project met API-sleutelverificatie.

   ```bash
   magento-cloud auth:api-token
   ```

1. Voer bij de prompt de waarde voor een geldig API-token in.

   ```terminal
   Please enter an API token:
   >
   
   The API token is valid.
   You are logged in.
   ```

### Voorbeeld: geautomatiseerd SSH-script

Er zijn twee opties voor het opslaan van de API-token.

>[!NOTE]
>
>Als een API-token wordt opgeslagen, wordt het `magento-cloud` CLI verifieert automatisch en er is geen behoefte om uit te voeren `magento-cloud login` gebruiken.

**Optie 1**: Maak een omgevingsvariabele om het API-token op te slaan

Schrijf de token naar uw bash_profile

```bash
echo "export MAGENTO_CLOUD_CLI_TOKEN=<your api token>" >> ~/.bash_profile
```

**Optie 2**: Voeg het token toe aan de `config.yaml` file

1. Maak op uw lokale werkstation een bestand met de naam `config.yaml` in de `.magento-cloud` in uw thuismap als deze niet bestaat.

   ```bash
   touch ~/.magento-cloud/config.yaml
   ```

1. Voeg de volgende configuratie aan toe `config.yaml` bestand.

   ```yaml
   api:
      token: <your api token>
   ```

>Voorbeeld-basscript

```shell
#!/bin/bash
magento-cloud ssh-cert:load
ssh abcdef7uyxabce-master-7rqtabc--mymagento@ssh.us-3.magento.cloud "tail -n 10 ~/var/log/cloud.log"
```

## Problemen oplossen

Gebruik de volgende informatie om de mislukkingen van SSH-verbindingsverzoeken als gevolg van verificatiefouten op te lossen `access requires MFA` of `permission denied`.

### Uw aanvraag bevat geen geldig certificaat

Als uw verzoek geen geldig certificaat oplevert, wordt een bericht weergegeven dat lijkt op het volgende:

```terminal
to Hello user-test (UUID: abaacca12-5cd1-4b123-9096-411add578998), you successfully
authenticated, but could not connect to service abcdef7uyxabce-master-7rqtabc--mymagento@ssh.us-3.magento.cloud:>
(reason: access requires MFA)
```

Probeer de volgende het oplossen van problemenprocedures om de verbindingskwestie op te lossen:

- De TFA-configuratie van de account verifiëren
- Verifieer opnieuw, en laad dan het certificaat opnieuw

**Om de configuratie en de authentificatie van TFA te verifiëren**:

1. Aanmelden bij [uw account](https://console.adobecommerce.com).

1. Klik in het accountmenu rechtsboven op **[!UICONTROL My Profile]**.

1. Op de _Mijn profiel_ pagina, klikt u op de **[!UICONTROL Security]** tab.

   Als TFA wordt toegelaten, verstrekt de sectie van de Veiligheid opties om de configuratie van TFA te beheren.

1. Als TFA niet is ingesteld, klikt u **[!UICONTROL Set up application]** en volgt u de instructies om deze in te schakelen. Zie [TFA inschakelen](user-access.md#enable-tfa-for-cloud-accounts).

1. Als TFA wordt gevormd, probeer opnieuw voor authentiek te verklaren.

**Het SSH-certificaat verifiëren en opnieuw laden**:

1. Gebruik de `magento-cloud` CLI voor opnieuw verifiëren:

   ```bash
   magento-cloud logout
   ```

   ```bash
   magento-cloud login
   ```

1. Laad het SSH-certificaat opnieuw:

   ```bash
   magento-cloud ssh-cert:load
   ```

### Toestemming geweigerd

Als de SSH-sleutel ontbreekt of ongeldig is, retourneert de SSH-verbindingsaanvraag een `Permission denied (publickey)` fout.

```terminal
Hello user-test (UUID: abaacca12-5cd1-4b123-9096-411add578998), you successfully authenticated, but could not connect to service oh2wi6klp5ytk-mc-35985-integration-nnulm4a--mymagento (reason: service doesn't exist or you do not have access to it)
oh2wi6klp5ytk-mc-35985-integration-nnulm4a--mymagento@ssh.eu-3.magento.cloud: Permission denied (publickey).
```

Om het probleem te bevestigen, voeg de sleutel van SSH aan uw huidige zitting toe, of werk het de configuratiedossier van SSH bij om uw sleutels van SSH automatisch te laden. Zie [Een openbare SSH-toets toevoegen](../development/secure-connections.md#add-an-ssh-public-key-to-your-account).

### Kan geen toegang krijgen tot projecten zonder MFB

Als u aan een project met toegelaten multi-factor authentificatie (MFA) voor authentiek verklaart, zou u de volgende fout kunnen ontvangen wanneer het verbinden met andere projecten die geen MFA vereisen:

```bash
ssh abcdef7uyxabce-master-7rqtabc--mymagento@ssh.us-3.magento.cloud
```

Monsterrespons:

```terminal
abcdef7uyxabce-master-7rqtabc--mymagento@ssh.us-3.magento.cloud: Permission denied (publickey).
```

Tijdens het genereren van het SSH-certificaat `magento-cloud` CLI voegt een extra sleutel van SSH aan uw lokale milieu toe. Die sleutel wordt gebruikt door gebrek als uw lokale configuratie SSH niet de sleutel van SSH voor projecttoegang omvat.

**Om uw sleutel van SSH aan de lokale configuratie toe te voegen**:

1. Maak de `config` bestand als dit niet bestaat.

   ```bash
   touch ~/.ssh/config
   ```

1. Een `IdentityFile` configuratie.

   ```yaml
   Host *
     IdentityFile ~/.ssh/id_rsa
   ```

>[!NOTE]
>
>U kunt meerdere SSH-toetsen opgeven door meerdere SSH-toetsen toe te voegen `IdentityFile` vermeldingen in uw configuratie.
