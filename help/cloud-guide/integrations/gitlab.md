---
title: GitLab-integratie
description: Leer hoe u uw Adobe Commerce in een cloud-infrastructuurproject kunt integreren met GitLab.
feature: Cloud, Integration
exl-id: 37fda8a0-7274-422f-9049-243f2e409f26
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---

# GitLab-integratie

U kunt een gegevensopslagplaats vormen GitLab om automatisch een milieu te bouwen en op te stellen wanneer u codeveranderingen duwt. Deze integratie synchroniseert uw GitLab-opslagplaats met uw Adobe Commerce op cloudinfratuuropportaccount.

{{private-repository}}

Dankzij deze integratie kunt u:

- Een omgeving maken wanneer u een vertakking maakt
- Implementeer de omgeving opnieuw wanneer u een pull-verzoek samenvoegt
- De omgeving verwijderen wanneer u de vertakking verwijdert

U moet een GitLab-token en een webhaak verkrijgen om het proces voort te zetten.

## Vereisten

- Beheerderstoegang tot de Adobe Commerce in het infrastructuurproject voor de cloud
- [`magento-cloud` CLI](../dev-tools/cloud-cli-overview.md) in uw lokale omgeving
- Een GitLab-account
- Een GitLab persoonlijk toegangstoken met schrijven-toegang tot de bewaarplaats GitLab, moet het geselecteerde werkingsgebied minstens zijn: `api` en `read_repository`.

## De opslagplaats voorbereiden

Clone your Adobe Commerce on cloud Infrastructure project from an existing environment and migrate the project branches to a new, empty GitLab repository, preserve the same tak names. Het is **kritisch** om een identieke Git-structuur te behouden, zodat u geen bestaande omgevingen of vertakkingen in uw Adobe Commerce verliest voor het infrastructuurproject van de cloud.

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
   magento-cloud project:get <project-id>
   ```

1. Voeg uw GitLab-opslagplaats toe als een externe opslagplaats (ervan uitgaande dat GitLab wordt gebruikt in de SaaS-versie).

   ```bash
   git remote add origin git@gitlab.com:<user-name>/<repo-name>.git
   ```

   De standaardnaam voor de externe verbinding kan `origin` of `magento`. Indien `origin` bestaat, kunt u een verschillende naam kiezen of u kunt de bestaande verwijzing anders noemen of schrappen. Zie [documentatie op afstand](https://git-scm.com/docs/git-remote).

1. Controleer of u de GitLab-afstandsbediening correct hebt toegevoegd.

   ```bash
   git remote -v
   ```

   Verwacht antwoord:

   ```terminal
   origin git@gitlab.com:<user-name>/<repo-name>.git (fetch)
   origin git@gitlab.com:<user-name>/<repo-name>.git (push)
   ```

1. Verplaats de projectbestanden naar de nieuwe GitLab-opslagplaats. Vergeet niet alle vertakkingsnamen gelijk te houden.

   ```bash
   git push -u origin master
   ```

   Als u begint met een nieuwe GitLab-opslagplaats, moet u mogelijk `-f` omdat de externe opslagplaats niet overeenkomt met uw lokale kopie.

1. Controleer of uw GitLab-opslagplaats al uw projectbestanden bevat.

## De integratie met GitLab inschakelen

Gebruik de `magento-cloud integration` gebruiken om de integratie met GitLab mogelijk te maken en de Payload-URL voor de GitLab-webhaak te krijgen om updates van GitLab naar uw Adobe Commerce te verzenden via het cloudinfragment-infrastructuurproject.

```bash
magento-cloud integration:add --type=gitlab --project=<project-ID> --token=<your-GitLab-token> [--base-url=<GitLab-url> --server-project=<GitLab-project> --build-merge-requests={true|false} --merge-requests-clone-parent-data={true|false} --fetch-branches={true|false} --prune-branches={true|false}]
```

| Optie | Beschrijving |
| ------ | ----------- |
| `<project-ID>` | Projectid Adobe Commerce on cloud Infrastructure |
| `<your-GitLab-token>` | Het persoonlijke toegangstoken dat u voor GitLab produceerde |
| `--base-url` | URL van GitLab (`https://gitlab.com/` als GitLab wordt gebruikt in de SaaS-versie) |
| `--server-project` | Projectnaam in GitLab (onderdeel na de basis-URL) |
| `--build-merge-requests` | An _optioneel_ parameter die Adobe Commerce op cloudinfrastructuur opdraagt een nieuwe omgeving te bouwen voor elke samenvoegaanvraag (`true` standaard) |
| `--merge-requests-clone-parent-data` | An _optioneel_ parameter die Adobe Commerce op cloudinfrastructuur opdraagt de gegevens van de bovenliggende omgeving te klonen voor samenvoegaanvragen (`true` standaard) |
| `--fetch-branches` | An _optioneel_ parameter die ervoor zorgt dat Adobe Commerce op de cloudinfrastructuur alle vertakkingen van de externe omgeving ophaalt (als inactieve omgevingen) (`true` standaard) |
| `--prune-branches` | An _optioneel_ parameter die Adobe Commerce instructies geeft over cloudinfrastructuur om vertakkingen te verwijderen die niet op de externe server bestaan (`true` standaard) |

>[!WARNING]
>
>De `magento-cloud integration` overschrijvingen van opdrachten _alles_ code in uw Adobe Commerce over het infrastructuurproject voor de cloud met de code uit uw GitLab-opslagplaats. Dit omvat alle vertakkingen, inclusief de `production` vertakking. Deze handeling gebeurt onmiddellijk en kan niet ongedaan worden gemaakt. Als beste praktijken, is het belangrijk om al uw takken van uw Adobe Commerce op het project van de wolkeninfrastructuur te klonen en hen te duwen aan uw bewaarplaats GitLab alvorens de integratie GitLab toe te voegen.

**De integratie met GitLab inschakelen**:

1. Voeg vanaf de terminal de GitLab-integratie toe aan uw Adobe Commerce-project voor cloudinfrastructuur:

   ```bash
   magento-cloud integration:add --type gitlab --project=3txxjf32gtryos --token=qVUfeEn4ouze7A7JH --base-url=https://gitlab.com/ --server-project=my-agency/project-name --build-merge-requests=false --merge-requests-clone-parent-data=false --fetch-branches=true --prune-branches=true
   ```

1. Typ desgevraagd `y` om de integratie toe te voegen.

   ```terminal
   Warning: adding a 'gitlab' integration will automatically synchronize code from the external Git repository.
   This means it can overwrite all the code in your project.
   Are you sure you want to continue? [y/N] y
   ```

1. De **Hook-URL** weergegeven door de geretourneerde uitvoer.

   ```terminal
   Hook URL: https://eu-3.magento.cloud/api/projects/3txxjf32gtryos/integrations/eolmpfizzg9lu/hook
   Created integration eolmpfizzg9lu (type: gitlab)
   +----------------------------------+---------------------------------------------------------------------------------------+
   | Property                         | Value                                                                                 |
   +----------------------------------+---------------------------------------------------------------------------------------+
   | id                               | <integration-id>                                                                      |
   | type                             | gitlab                                                                                |
   | token                            | ******                                                                                |
   | base_url                         | https://gitlab.com/                                                                   |
   | project                          | my-agency/project-name                                                                |
   | fetch_branches                   | true                                                                                  |
   | prune_branches                   | true                                                                                  |
   | build_merge_requests             | false                                                                                 |
   | merge_requests_clone_parent_data | false                                                                                 |
   | hook_url                         | https://eu-3.magento.cloud/api/projects/<project-id>/integrations/<integration-id>/hook |
   +----------------------------------+---------------------------------------------------------------------------------------+
   ```

### Webhaak toevoegen in GitLab

Als u gebeurtenissen, zoals een push- of samenvoegverzoek, wilt communiceren met uw Cloud Git-server, moet u [een webhaak maken](https://docs.gitlab.com/ee/user/project/integrations/webhooks.html#overview) voor uw GitLab-opslagplaats

1. Klik in uw GitLab-opslagplaats op de knop **Instellingen** tab.

1. Klik in de linkernavigatiebalk op **Webhaken**.

1. In de _Webhaken_ bewerken, bewerkt u de volgende velden:

   - **URL**: Voer de `Hook URL` teruggekeerd toen u de integratie GitLab toeliet.
   - **Geheim token**: Voer zo nodig een verificatiegeheim in.
   - **Trigger**: Controle `Merge request events` en/of `Push events` afhankelijk van uw behoeften.
   - **SSL-verificatie inschakelen**: U moet deze optie selecteren.

1. Klikken **Webhaak toevoegen**.

### Integratie testen

Na het vormen van de integratie GitLab, kunt u verifiëren dat de integratie operationeel is gebruikend `magento-cloud` CLI:

```bash
magento-cloud integration:validate
```

Of u kunt het testen door een eenvoudige verandering in uw bewaarplaats GitLab te duwen.

1. Maak een testbestand.

   ```bash
   touch test.md
   ```

1. Leg de wijziging vast en duw deze naar uw GitLab-opslagplaats.

   ```bash
   git add . && git commit -m "Testing GitLab integration" && git push
   ```

1. Aanmelden bij de [[!DNL Cloud Console]](../project/overview.md) en verifieer dat uw commit bericht wordt getoond en uw project het opstellen.

## Een Cloud-vertakking maken

Gebruik de `magento-cloud` CLI `environment:push` gebruiken om een nieuwe omgeving te maken en te activeren. Zie [Een Cloud-vertakking maken](bitbucket.md#create-a-cloud-branch).

## Integratie verwijderen

Gebruik de `magento-cloud` CLI `integration:delete` gebruiken om de integratie te verwijderen. Zie [Integratie verwijderen](bitbucket.md#remove-the-integration).
