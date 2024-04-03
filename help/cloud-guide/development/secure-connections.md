---
title: Beveiligde verbindingen
description: Leer hoe u SSH-toetsen op uw Adobe Commerce kunt toepassen op een cloudinfrastructuurproject en u kunt aanmelden bij externe omgevingen.
role: Developer
feature: Cloud, Security
topic: Security
exl-id: b5780e8e-e3da-4b10-8ca3-2778085acd4a
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 0%

---

# Beveiligde verbindingen met externe omgevingen

Veilig Shell (SSH) is een gemeenschappelijk protocol dat wordt gebruikt om veilig in verre servers en systemen te registreren. U kunt SSH gebruiken om toegang te krijgen tot uw externe omgevingen voor het beheer van de Adobe Commerce-toepassing en het openen van logbestanden voor externe omgevingen. Adobe ondersteunt alleen Secure FTP-verbindingen (sFTP) met behulp van de openbare SSH-sleutel. FTP-verbindingen worden niet ondersteund.

## Een SSH-sleutelpaar genereren

Creeer een SSH zeer belangrijk paar op elke machine en werkruimte die toegang tot uw code en milieu&#39;s van de projectbron vereist. De sleutel van SSH staat u toe om met GitHub te verbinden om broncode te beheren en met wolkenservers te verbinden zonder het moeten uw gebruikersbenaming en wachtwoord constant leveren. Zie [Verbinding maken met GitHub met SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) voor verdere instructies bij het creëren van een SSH zeer belangrijk paar.

- De _openbare sleutel_ is veilig om tot een plaats, SSH, en sFTP toegang te hebben.
- De _persoonlijke sleutel_ blijft privé op het werkstation.

>[!CAUTION]
>
>**Deel nooit uw persoonlijke sleutel.** Voeg het niet toe aan een kaartje, kopieer het aan een praatje, of maak het aan e-mails vast.

## Een SSH-openbare sleutel toevoegen aan uw account

Nadat u de openbare SSH-sleutel aan uw Adobe Commerce hebt toegevoegd op een cloud-infrastructuuraccount, dient u alle actieve omgevingen op uw account opnieuw te implementeren om de sleutel te installeren.

U kunt SSH-sleutels toevoegen aan uw account met een van de volgende methoden: Cloud CLI of [!DNL Cloud Console].

>[!BEGINTABS]

>[!TAB CLI]

### De SSH-toets toevoegen met de Cloud CLI

1. Wijzig op uw lokale werkstation de projectmap.

1. Meld u aan bij uw project:

   ```bash
   magento-cloud login
   ```

1. Voeg de openbare sleutel toe.

   ```bash
   magento-cloud ssh-key:add ~/.ssh/id_rsa.pub
   ```

>[!TIP]
>
>U kunt SSH-toetsen weergeven en verwijderen met de Cloud CLI-opdrachten `ssh-key:list` en `ssh-key:delete`.

>[!TAB Console]

### De SSH-toets toevoegen met de [!DNL Cloud Console]

**Om een sleutel van SSH aan een nieuw project toe te voegen**:

1. Aanmelden bij de [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Klik op **[!UICONTROL No SSH key]**. Dit pictogram is rechts van het bevelgebied en is zichtbaar wanneer het project geen sleutel van SSH bevat.

1. Kopieer en plak de inhoud van de openbare SSH-toets in het dialoogvenster **Openbare sleutel** veld.

1. Volg de overige aanwijzingen.

**Een SSH-sleutel toevoegen aan uw Cloud-profiel**:

1. Aanmelden bij de [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Klik in het accountmenu rechtsboven op **Mijn profiel**.

1. In de _SSH-toetsen_ weergeven, klikken **Openbare sleutel toevoegen**.

1. In de _Een SSH-toets toevoegen_ formulier, geef uw sleutel een **Titel** en plak de openbare SSH-toets in het dialoogvenster **Sleutel** veld.

1. Klikken **Opslaan**.

>[!ENDTABS]

## Verbinding maken met een externe omgeving

U kunt verbinding maken met een externe omgeving met behulp van de `magento-cloud` CLI of een bevel van SSH. De `magento-cloud` CLI-opdrachten kunnen alleen worden gebruikt in Starter- en Pro-integratieomgevingen.

### Cloud CLI gebruiken

**Aanmelden bij een externe integratieomgeving**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Maak een lijst van de milieu&#39;s in dat project.

   ```bash
   magento-cloud environment:list -p <project-ID>
   ```

1. Gebruik SSH om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh -p <project-ID> -e <environment-ID>
   ```

### Een SSH-opdracht gebruiken

De [!DNL Cloud Console] omvat een lijst van Web en de toegangsbevelen van SSH voor elk milieu.

**Om het bevel van SSH te kopiëren**:

1. Aanmelden bij de [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Selecteer een project in het menu _Alle projecten_ lijst.

1. Selecteer een omgeving.

1. Klik op **[!UICONTROL SSH]**.

1. In de _SSH_ klikt u op de knop Copy om de volledige SSH-opdracht naar het klembord te kopiëren.

1. Open een terminal en plak de opdracht SSH om een verbinding te maken.

   ```bash
   ssh abcdefg123abc-branch-a12b34c--mymagento@ssh.us-2.magento.cloud
   ```

>[!TIP]
>
>Voor Pro het Staging en van de Productie milieu&#39;s, kan het bevel van SSH als kijken:
>
>```bash
>ssh <node>.ent-<project-ID>-<environment>-<user-ID>@ssh.<region>.magento.com
>```

## sFTP

Adobe Commerce on cloud Infrastructure ondersteunt toegang tot uw omgevingen met sFTP (Secure FTP) met SSH-verificatie. Gebruik een cliënt die de zeer belangrijke authentificatie van SSH voor sFTP steunt en uw openbare sleutel van SSH gebruiken. Uw openbare sleutel van SSH moet aan het doelmilieu worden toegevoegd. Voor Starter-omgevingen en Pro-integratieomgevingen kunt u [Voeg het toe door [!DNL Cloud Console]](#add-your-ssh-key-using-the-project-web-interface).

Alleen-lezen sFTP-verbindingen zijn _niet_ ondersteund; sFTP-toegang wordt geleverd met _schrijven_ toestemming standaard.

Wanneer het vormen sFTP, gebruik de informatie van uw bevel van het de toegangsmilieu van SSH: `<project-id>-<environment-id>--<app-name>@ssh<cloud-host>`

- **Gebruikersnaam**: Alle inhoud voor de `@` in uw SSH toegangsbestemming.
- **Wachtwoord**: U hebt geen wachtwoord nodig voor sFTP. sFTP-toegang gebruikt de SSH-sleutelverificatie.
- **Host**: Alle inhoud na de `@` in uw toegang van SSH.
- **Poort**: 22, wat de standaardhaven van SSH is.
- **SSH** Persoonlijke sleutel: geef indien nodig de locatie van de persoonlijke sleutel op voor de sFTP-client. Persoonlijke sleutels worden standaard opgeslagen in de `~/.ssh` directory.

Afhankelijk van de client zijn mogelijk aanvullende opties vereist om SSH-verificatie voor sFTP te voltooien. Controleer de documentatie voor de geselecteerde client.

Voor **Startomgevingen en Pro-integratieomgevingen** kunt u ook overwegen [toevoegen `mount`](../application/properties.md#mounts) voor toegang tot een specifieke map. U voegt de hoeveelheid toe aan uw `.magento.app.yaml` bestand. Zie voor een lijst met beschrijfbare mappen [Projectstructuur](../project/file-structure.md). Dit koppelingspunt werkt alleen in die omgevingen.

Voor **Pro Staging- en productieomgevingen** Als u geen SSH-toegang tot de omgeving hebt, moet u [een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om sFTP-toegang en een koppelingspunt aan te vragen voor toegang tot de specifieke map, bijvoorbeeld `pub/media`.

>[!NOTE]
>Voor Pro Staging en Productie, als de sFTP-verbinding een _algemeen_ gebruiker die **niet** moeten [toegevoegd aan het Cloud-project](../project/user-access.md), moet u [een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) met hun **publiek** sleutel gekoppeld. **Geef nooit uw persoonlijke SSH-sleutel op.**

## SSH-tunneling

U kunt SSH het een tunnel graven gebruiken om met de dienst van uw lokale ontwikkelomgeving te verbinden alsof de dienst lokaal was. Voordat u een tunnelverbinding maakt, configureert u uw [SSH](#add-an-ssh-public-key-to-your-account).

Gebruik een eindtoepassing aan login en geef bevelen uit.

```bash
magento-cloud login
```

Controleer of er tunnels geopend zijn.

```bash
magento-cloud tunnel:list
```

Om een tunnel te bouwen, moet u het weten [toepassingsnaam](../application/properties.md#name). U kunt de toepassingsnaam controleren gebruikend CLI:

```bash
magento-cloud apps
```

### De SSH-tunnel instellen

```bash
magento-cloud tunnel:open -e <environment-ID> --app <app-name>
```

Als u bijvoorbeeld een tunnel wilt openen voor de `sprint5` vertakken in een project met een benoemde app `mymagento`, enter

```bash
magento-cloud tunnel:open -e sprint5 --app mymagento
```

Monsterrespons:

```terminal
SSH tunnel opened on port 30004 to relationship: redis
SSH tunnel opened on port 30005 to relationship: database
Logs are written to: /home/magento_user/.magento/tunnels.log

List tunnels with: magento-cloud tunnels
View tunnel details with: magento-cloud tunnel:info
Close tunnels with: magento-cloud tunnel:close
```

**Om informatie over uw tunnel te tonen**:

```bash
magento-cloud tunnel:info -e <environment-ID>
```

### Verbinding maken met services

Na het vestigen van een tunnel van SSH, kunt u met de diensten verbinden alsof het lopen plaatselijk. Als u bijvoorbeeld verbinding wilt maken met de database, gebruikt u de volgende opdracht:

```bash
mysql --host=127.0.0.1 --user='<database-username>' --pass='<user-password>' --database='<name>' --port='<port>'
```
