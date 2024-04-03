---
title: Cloud CLI
description: Leer meer over de magento-cloud CLI en hoe u hiermee lokale ontwikkelomgevingen voor uw Adobe Commerce kunt beheren op het infrastructuurproject voor de cloud.
exl-id: 70dddd62-0269-4af4-bd2a-1a4fbf11a131
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---


# Cloud CLI

De `magento-cloud` Met het CLI-hulpprogramma kunnen ontwikkelaars en systeembeheerders Cloud-projecten en -omgevingen beheren, routines uitvoeren en automatiseringstaken uitvoeren. De `magento-cloud` CLI breidt de eigenschappen en de functionaliteit van uit [[!DNL Cloud Console]](../../get-started/cloud-console.md). Nadat u de `magento-cloud` CLI op uw lokale werkstation, kunt u het gebruiken om uw Adobe Commerce op de milieu&#39;s van de Aanzet en van de integratie van de wolkeninfrastructuur te beheren Pro.

**Als u het dialoogvenster `magento-cloud` CLI**:

1. Wijzig op uw lokale werkstation de directory waarin u het Cloud-project wilt klonen en waar de [eigenaar van bestandssysteem](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html) heeft _schrijven_ toegang.

1. Installeer de `magento-cloud` CLI.

   ```bash
   curl -sS https://accounts.magento.cloud/cli/installer | php
   ```

1. Toevoegen `magento-cloud` CLI naar het basisprofiel.

   ```bash
   export PATH=$PATH:$HOME/.magento-cloud/bin
   ```

1. Laad het bijgewerkte basisprofiel opnieuw.

   ```bash
   . ~/.bash_profile
   ```

1. Om CLI in werking te stellen, roep `magento-cloud` en voer uw aanmeldingsgegevens voor uw Cloud-account in wanneer hierom wordt gevraagd.

   ```bash
   magento-cloud
   ```

   ```terminal
   Welcome to Magento Cloud!
   Please log in using your Magento Cloud account.
   Your email address or username:
   ```

1. Controleer de `magento-cloud` bevindt zich in uw pad. In het volgende voorbeeld worden de beschikbare opdrachten weergegeven.

   ```bash
   magento-cloud list
   ```

## Algemene opdrachten

Adobe heeft deze opdrachten ontworpen om omgevingen voor cloudintegratie te beheren en raadt u aan de `magento-cloud` CLI van een projectfolder zodat kunt u weglaten `-p <project-ID>` parameter.

De volgende lijst met veelgebruikte `magento-cloud` CLI-opdrachten bevatten alleen de vereiste opties. U kunt de `--help` optie met om het even welk bevel om meer informatie te zien.

| Opdracht | Beschrijving |
| ------------------------------------ | -------------------------------------------------- |
| `magento-cloud login` | Meld u aan bij het project. |
| `magento-cloud list` | Maak een lijst van de beschikbare bevelen voor CLI hulpmiddel. |
| `magento-cloud environment:list` | Maak een lijst van de milieu&#39;s in het huidige project. |
| `magento-cloud environment:checkout` | Ontdek een bestaande omgeving. |
| `magento-cloud environment:merge -e` | Wijzigingen in deze omgeving samenvoegen met het bovenliggende element. |
| `magento-cloud variables` | Variabelen weergeven in deze omgeving. |
| `magento-cloud ssh` | Gebruik SSH om verbinding te maken met de externe omgeving. |
| `magento-cloud url` | Open de Adobe Commerce storefront in een browser. |
| `magento-cloud web` | Open de [!DNL Cloud Console]. |

## Omgeving, opdrachten

Het milieu _name_ verschilt van het milieu _ID_ alleen als u spaties of hoofdletters in de omgevingsnaam gebruikt. Een milieu-id bestaat uit alle kleine letters, getallen en toegestane symbolen. Hoofdletters in een omgevingsnaam worden omgezet in kleine letters in de id. Spaties in een omgevingsnaam worden omgezet in streepjes.

Een omgevingsnaam _kan_ include-tekens die zijn gereserveerd voor uw Linux-shell of voor reguliere expressies. Verboden tekens bevatten accolades (`{ }`), ronde haakjes, asterisk (`*`), punthaken (`< >`), ampersand (`&`), percentage (`%`) en andere tekens.

De `magento-cloud environment:list` bevel toont omgevingshiërarchieën, terwijl `git branch` niet. Als u een geneste omgeving hebt, gebruikt u het volgende:

```bash
magento-cloud environment:list
```

### Omgeving opnieuw implementeren

Trigger een herplaatsing zonder een duw te gebruiken. Controleer en bevestig de omgeving die opnieuw moet worden geïmplementeerd. Gebruik geen hergroepering als er een bouwstijl in een hangende staat is.

```bash
magento-cloud environment:redeploy
```

Monsterrespons:

```terminal
Are you sure you want to redeploy the environment <environment-name>? [Y/n]
```

{{redeploy-warning}}

## Opdrachten Git

Het kan zijn dat sommige van deze opdrachten lijken op de opdrachten bij Git. De `magento-cloud` maakt rechtstreeks verbinding met het op Git gebaseerde Cloud-project met extra functies. Als u een vertakking maakt zonder de opdracht `magento-cloud` CLI, wordt het niet &quot;geactiveerd&quot;en bouwt niet automatisch wanneer u veranderingen in het verre milieu duwt. De `magento-cloud` CLI-opdracht omvat activering.

Als u een vertakking wilt maken, gebruikt u de opdracht `magento-cloud` de tak wordt geactiveerd.

```bash
magento-cloud environment:branch <new-name> <parent-branch>
```

Voor de status van een vertakking:

- Gebruik de `magento-cloud env` gebruiken om een lijst weer te geven van de vertakkingen van de omgeving en hun status: actief of inactief.
- Gebruik de `magento-cloud environment:activate` gebruiken om een omgevingsvertakking te activeren.

Druk op een lege Git om een implementatie te activeren. Bijvoorbeeld:

```bash
git commit --allow-empty -m "redeploy" && git push <branch-name>
```

Sommige acties, zoals het toevoegen van een gebruiker, resulteren niet in plaatsing.

### Een omgevingsvertakking maken

De volgende stappen tonen het gebruiken van CLI en van het Git bevelen onderling verwisselbaar aan om uw lokale milieu te beheren:

1. Wijzig op uw lokale werkstation de projectmap.

1. Schakel over naar de [eigenaar van bestandssysteem](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html).

1. Meld u aan bij uw project.

   ```bash
   magento-cloud login
   ```

1. Maak een lijst van uw projecten.

   ```bash
   magento-cloud project:list
   ```

1. Maak een lijst van milieu&#39;s in het project. Elke omgeving bevat een actieve Git-vertakking die uw code, database, omgevingsvariabelen, configuraties en services bevat.

   ```bash
   magento-cloud environment:list
   ```

   >[!NOTE]
   >
   >Het is belangrijk om de `magento-cloud environment:list` gebruiken omdat er omgevingshiërarchieën worden weergegeven, terwijl de `git branch` niet wordt uitgevoerd.

1. Zoek de laatste code naar de vertakkingen van de oorsprong.

   ```bash
   git fetch origin
   ```

1. Uitchecken of overschakelen naar een specifieke vertakking en omgeving.

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

   Met Git-opdrachten kunt u alleen de Git-vertakking uitchecken. De `magento-cloud checkout` het bevel controleert de tak en schakelaars aan het actieve milieu.

   >[!TIP]
   >
   >U kunt een omgevingsvertakking maken met de opdracht `magento-cloud environment:branch <environment-name> <parent-environment-ID>` opdrachtsyntaxis. Het kan enige extra tijd duren om een omgevingsvertakking te maken en te activeren.

1. Gebruik de milieu-id om bijgewerkte code aan uw lokale computer te trekken. Dit is niet nodig als de omgevingsvertakking nieuw is.

   ```bash
   git pull origin <environment-ID>
   ```

1. (_Optioneel_) Maak een [opname](../storage/snapshots.md) van de omgeving als back-up.

   ```bash
   magento-cloud snapshot:create -e <environment-ID>
   ```

## CLI bijwerken

De `magento-cloud` CLI controleert beschikbare updates wanneer u login, maar u kunt op updates controleren gebruikend `self:update` gebruiken. Als er een update beschikbaar is, volg de instructies om CLI bij te werken.

Als uw `magento-cloud` CLI is bijgewerkt, ziet u de volgende reactie:

```bash
magento-cloud update
```

```terminal
Checking for Magento Cloud CLI updates (current version: X.XX.X)
No updates found
```
