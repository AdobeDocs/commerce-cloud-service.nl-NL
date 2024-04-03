---
title: Bitmap-integratie
description: Leer hoe u uw Adobe Commerce in een cloud-infrastructuurproject kunt integreren met Bitbucket.
feature: Cloud, Integration
exl-id: cd3cffbe-268f-429b-a2ea-0306159f4a6b
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---

# Bitmap-integratie

U kunt uw opslagplaats van Bitbucket vormen om automatisch een milieu te bouwen en op te stellen wanneer u codeveranderingen duwt. Deze integratie synchroniseert uw Bitmap-opslagplaats met uw Adobe Commerce op een cloud-infrastructuuraccount.

{{private-repository}}

## Vereisten

- Beheerderstoegang tot de Adobe Commerce in het infrastructuurproject voor de cloud
- [`magento-cloud` CLI](../dev-tools/cloud-cli-overview.md) in uw lokale omgeving
- Een Bitmap-account
- Beheerderstoegang tot de opslagplaats van Bitmap
- Een SSH-toegangstoets voor de Bitmap-opslagplaats

## De opslagplaats voorbereiden

Clone your Adobe Commerce on cloud Infrastructure project from an existing environment and migrate the project Branches to a new, empty Bitbucket repository, preserve the same taknames. Het is **kritisch** om een identieke Git-structuur te behouden, zodat u geen bestaande omgevingen of vertakkingen in uw Adobe Commerce verliest voor het infrastructuurproject van de cloud.

1. Meld u vanaf de terminal aan bij uw Adobe Commerce voor een infrastructuurproject voor de cloud.

   ```bash
   magento-cloud login
   ```

1. Maak een lijst van uw projecten en kopieer projectidentiteitskaart

   ```bash
   magento-cloud project:list
   ```

1. Kloont het project naar uw lokale omgeving.

   ```bash
   magento-cloud project:get <project-ID>
   ```

1. Voeg uw opslagplaats van Bitmap toe als ver.

   ```bash
   git remote add origin git@bitbucket.org:<user-name>/<repo-name>.git
   ```

   De standaardnaam voor de externe verbinding kan `origin` of `magento`. Indien `origin` bestaat, kunt u een verschillende naam kiezen of u kunt de bestaande verwijzing anders noemen of schrappen. Zie [documentatie op afstand](https://git-scm.com/docs/git-remote).

1. Controleer of u de optie Bitmap op de juiste manier hebt toegevoegd.

   ```bash
   git remote -v
   ```

   Verwacht antwoord:

   ```terminal
   origin git@bitbucket.org:<user-name>/<repo-name>.git (fetch)
   origin git@bitbucket.org:<user-name>/<repo-name>.git (push)
   ```

1. Verplaats de projectbestanden naar de nieuwe Bitmap-opslagplaats. Vergeet niet alle vertakkingsnamen gelijk te houden.

   ```bash
   git push -u origin master
   ```

   Als u begint met een nieuwe opslagplaats voor bitmaps, moet u mogelijk de `-f` omdat de externe opslagplaats niet overeenkomt met uw lokale kopie.

1. Controleer of uw Bitmap-opslagplaats al uw projectbestanden bevat.

## Een OAuth-consument maken

Voor de integratie met Bitmap is een [OAuth Consumer](https://support.atlassian.com/bitbucket-cloud/docs/use-oauth-on-bitbucket-cloud/). U hebt de OAuth nodig `key` en `secret` van deze consument om de volgende sectie in te vullen.

**Een OAuth-consument maken in Bitbucket**:

1. Aanmelden bij uw [Bitmap](https://id.atlassian.com/login) account.

1. Klikken **Instellingen** > **Toegangsbeheer** > **OAuth**.

1. Klikken **Consumenten toevoegen** en configureren als volgt:

   ![Configuratie van bitemmer voor OAuth-gebruik](../../assets/oauth-consumer-config.png)

   >[!WARNING]
   >
   >Een geldige **URL voor terugbellen** is niet vereist, maar u moet een waarde in dit veld invoeren om de integratie te voltooien.

1. Klikken **Opslaan**.

1. Klik op de consument **Naam** om uw OAuth te onthullen `key` en `secret`.

1. OAuth kopiëren `key` en `secret` voor het configureren van de integratie.

## De integratie configureren

1. Navigeer vanaf de terminal naar uw Adobe Commerce op het infrastructuurproject voor de cloud.

1. Een tijdelijk bestand maken met de naam `bitbucket.json` en voeg het volgende toe: vervang de variabelen tussen punthaken door uw waarden:

   ```json
   {
     "type": "bitbucket",
     "repository": "<bitbucket-user-name/bitbucket-repo-name>",
     "app_credentials": {
       "key": "<oauth-consumer-key>",
       "secret": "<oauth-consumer-secret>"
     },
     "prune_branches": true,
     "fetch_branches": true,
     "build_pull_requests": true,
     "resync_pull_requests": true
   }
   ```

   >[!TIP]
   >
   >Zorg ervoor dat u de naam van de opslagplaats voor bitmaps gebruikt en niet de URL. De integratie mislukt als u een URL gebruikt.

1. Voeg de integratie aan uw project toe gebruikend `magento-cloud` CLI-gereedschap.

   >[!WARNING]
   >
   >De volgende opdracht overschrijft _alles_ code in uw Adobe Commerce over een wolkeninfrastructuurproject met code uit uw Bitbucket-opslagplaats. Dit omvat alle vertakkingen, inclusief de `production` vertakking. Deze handeling gebeurt onmiddellijk en kan niet ongedaan worden gemaakt. Het is belangrijk dat u alle vertakkingen van uw Adobe Commerce op het infrastructuurproject van de cloud kloont en deze naar uw Bitbucket-opslagplaats duwt **voor** toevoegen van de integratie met Bitmap.

   ```bash
   magento-cloud project:curl -p '<project-ID>' /integrations -i -X POST -d "$(< bitbucket.json)"
   ```

   Dit retourneert een lange HTTP-respons met headers. Een geslaagde integratie retourneert een 200- of 201-statuscode. De status 400 of hoger geeft aan dat er een fout is opgetreden.

1. Tijdelijk verwijderen `bitbucket.json` bestand.

1. Controleer de projectintegratie.

   ```bash
   magento-cloud integrations -p <project-ID>
   ```

   ```terminal
   +----------+-----------+--------------------------------------------------------------------------------+
   | ID       | Type      | Summary                                                                        |
   +----------+-----------+--------------------------------------------------------------------------------+
   | <int-id> | bitbucket | Repository: bitbucket_Account/magento-int                                      |
   |          |           | Hook URL:                                                                      |
   |          |           | https://magento-url.cloud/api/projects/<project-id>/integrations/<int-id>/hook |
   +----------+-----------+--------------------------------------------------------------------------------+
   ```

   Noteer de **Hook-URL** om een webhaak in BitBucket te vormen.

### Webhaak toevoegen in BitBucket

Als u gebeurtenissen, zoals een push-systeem, wilt communiceren met uw Cloud Git-server, is het dan nodig om een webhaak voor uw BitBucket-opslagplaats te hebben. Als u een op de juiste wijze gevolgde Bitmap-integratie instelt, wordt automatisch een webhaak gemaakt. Het is belangrijk dat u de webhaak controleert om te voorkomen dat er meerdere integraties ontstaan.

1. Aanmelden bij uw [Bitmap](https://id.atlassian.com/login) account.

1. Klikken **Opslagplaatsen** en selecteer uw project.

1. Klikken **Instellingen voor opslagplaats** > **Workflow** > **Webhaken**.

1. Controleer de webhaak voordat u verdergaat.

   Als de haak actief is, slaat u de resterende stappen over en [Integratie testen](#test-the-integration). De haak moet een naam hebben die lijkt op **&quot;Adobe Commerce over cloudinfrastructuur &lt;project_id>&quot;** en een formaat van haak URL gelijkend op: `https://<zone>.magento.cloud/api/projects/<project_id>/integrations/<id>/hook`

1. Klikken **Webhaak toevoegen**.

1. In de _Nieuwe webhaak toevoegen_ Bewerk de volgende velden:

   - **Titel**: Adobe Commerce-integratie
   - **URL**: Gebruik de URL van de pagina `magento-cloud` integratielijst
   - **Triggers**: De standaardwaarde is een basis _Push in opslagplaats_

1. Klikken **Opslaan**.

### Integratie testen

Na het vormen van de integratie Bitbucket kunt u verifiëren dat de integratie operationeel is gebruikend `magento-cloud` CLI:

```bash
magento-cloud integration:validate
```

U kunt het ook testen door een eenvoudige wijziging door te drukken in de opslagplaats van het Bitmap-object.

1. Maak een testbestand.

   ```bash
   touch test.md
   ```

1. Leg de wijziging vast en duw deze naar de opslagplaats voor bitmaps.

   ```bash
   git add . && git commit -m "Testing Bitbucket integration" && git push
   ```

1. Aanmelden bij de [[!DNL Cloud Console]](../project/overview.md) en verifieer dat uw commit bericht wordt getoond en uw project het opstellen.

   ![De integratie van het bitemenu testen](../../assets/bitbucket-integration.png)

## Een Cloud-vertakking maken

De integratie met Bitmap kan geen nieuwe omgevingen in uw Adobe Commerce activeren voor een infrastructuurproject in de cloud. Als u een omgeving maakt met Bitmap, moet u de omgeving handmatig activeren. Om deze extra stap te vermijden, is het aan te raden om omgevingen te maken met de `magento-cloud` CLI-gereedschap of de [!DNL Cloud Console].

**Een vertakking activeren die is gemaakt met Bitmap**:

1. Gebruik de `magento-cloud` CLI om de vertakking te duwen.

   ```bash
   magento-cloud environment:push from-bitbucket
   ```

   ```terminal
   Pushing from-bitbucket to the new environment from-bitbucket
   Activate from-bitbucket after pushing? [Y/n] y
   Parent environment [master]: integration
   --- (Validation and activation messages)
   ```

1. Controleer of de omgeving actief is.

   ```bash
   magento-cloud environment:list
   ```

   ```terminal
   Your environments are:
   +---------------------+----------------+--------+
   | ID                  | Name           | Status |
   +---------------------+----------------+--------+
   | master              | Master         | Active |
   |  integration        | integration    | Active |
   |    from-bitbucket * | from-bitbucket | Active |
   +---------------------+----------------+--------+
   * - Indicates the current environment
   ```

Nadat u een omgeving hebt gemaakt, kunt u de corresponderende vertakking met de reguliere opdrachten voor Git naar de externe opslagplaats voor bitmaps duwen. Als u daarna een vertakking wijzigt in Bitbucket, wordt de omgeving automatisch gemaakt en geïmplementeerd.

## Integratie verwijderen

U kunt de integratie met Bitmap veilig verwijderen uit uw project zonder dat dit van invloed is op uw code.

**De integratie met Bitmap verwijderen**:

1. Meld u vanaf de terminal aan bij uw Adobe Commerce voor een infrastructuurproject voor de cloud.

1. Maak een lijst van uw integratie. U hebt de integratie-id Bitmap nodig om de volgende stap te voltooien.

   ```bash
   magento-cloud integration:list
   ```

1. De integratie verwijderen.

   ```bash
   magento-cloud integration:delete <int-ID>
   ```

Bovendien kunt u de integratie met Bitmap verwijderen door u aan te melden bij uw Bitmap-account en de OAuth-subsidie voor de account in te trekken _Instellingen_ pagina.

## Integratie van bitmapserver

Als u de integratie met de Bitmap-server wilt gebruiken, hebt u het volgende nodig:

- [Toegangstoken bitmap](https://confluence.atlassian.com/bitbucketserver/http-access-tokens-939515499.html)—Genereer een token dat Project subsidieert `read` toegang en opslagplaats `admin` toegang
- [URL van bitmapserver](https://confluence.atlassian.com/bitbucketserver/specify-the-bitbucket-base-url-776640392.html)—Voeg de basis-URL van de Bitmap-instantie toe

Hoewel u de CLI van de Wolk kunt gebruiken om door de stappen van de de serverintegratie van Bitbucket te lopen, kijkt het volledige bevel gelijkaardig aan het volgende:

```bash
magento-cloud integration:add --type=bitbucket_server --base-url=<bitbucket-url> --username=<username> --token=<bitbucket-access-token> --project=<project-ID>
```

Gebruik de Help-opdracht voor meer gebruiksvereisten en -opties: `magento-cloud integration:add --help`
