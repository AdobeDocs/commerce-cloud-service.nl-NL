---
title: De takken met CLI beheren
description: Leer hoe u de vertakkingen voor Adobe Commerce op cloudinfrastructuur beheert met de Cloud CLI.
role: Developer
feature: Cloud, Install
exl-id: a871c7e2-4506-4a05-8fc2-fc5ef2afe609
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# De takken met CLI beheren

Als u het dialoogvenster `magento-cloud` CLI, zie [Cloud CLI-verwijzing](../dev-tools/cloud-cli-overview.md). Nadat u de `magento-cloud` CLI en SSH-sleutels instellen voor externe toegang tot uw cloudinfrastructuur `magento-cloud` CLI bevelen om de milieu&#39;s voor uw projecten te beheren. Voor informatie over de omgevingsarchitectuur raadpleegt u [Starter-architectuur](../architecture/starter-architecture.md) of [Pro-architectuur](../architecture/pro-architecture.md).

De vertakkingen en omgevingen beheren met de [!DNL Cloud Console], zie [Vertakkingen beheren met de [!DNL Cloud Console]](../project/console-branches.md).

## CLI-opdrachten gebruiken

De `magento-cloud` CLI-opdrachten zijn vergelijkbaar met Git-opdrachten. U kunt ze gebruiken om verbinding te maken met uw project en uw omgevingen te beheren. Hoewel u de bevelen van om het even welke folder kunt in werking stellen, adviseert men dat u hen van een projectfolder in werking stelt. Wanneer u vanuit een projectmap uitvoert, kunt u de opdracht `-p <project-ID>` parameter. Zie de [Cloud CLI-verwijzing](../dev-tools/cloud-cli-overview.md).

## Het project klonen

In de volgende instructies wordt een combinatie van `magento-cloud` CLI bevelen en de bevelen van het Git om uw project aan uw lokaal werkstation te klonen. Een volledige lijst met `magento-cloud` CLI-opdrachten gebruiken `magento-cloud list` gebruiken.

>[!IMPORTANT]
>
>Met sommige opdrachten van Git kunt u geen actie in uw Adobe Commerce uitvoeren voor een infrastructuurproject in de cloud. U kunt bijvoorbeeld een vertakking maken met de opdracht Git, maar u kunt geen nieuwe omgeving maken en activeren. U moet een omgeving maken met `magento-cloud environment:branch <branch-name>` bevel voor het milieu worden _actief_. U kunt ook de opdracht [!DNL Cloud Console] om actieve omgevingen te maken. Zie [Cloud CLI-verwijzing](../dev-tools/cloud-cli-overview.md#git-commands).

**Een project klonen `master` milieu**:

1. Meld u aan bij uw lokale werkstation met een [eigenaar van bestandssysteem](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html) account.

1. Wijzigen in webserver of virtuele host _docroot_ directory.

1. Meld u aan met de `magento-cloud` CLI.

   ```bash
   magento-cloud login
   ```

1. Maak een lijst van uw projecten.

   ```bash
   magento-cloud project:list
   ```

1. Een project klonen.

   ```bash
   magento-cloud project:get <project-ID>
   ```

   Geef een mapnaam op wanneer hierom wordt gevraagd.

1. Wijzigen in de `magento2` directory.

1. Maak een lijst van beschikbare milieu&#39;s voor het project.

   ```bash
   magento-cloud environment:list
   ```

   >[!IMPORTANT]
   >
   >De `magento-cloud environment:list` toont milieu hiërarchieën, terwijl het bevel `git branch` niet wordt uitgevoerd.

1. De externe vertakkingen ophalen.

   ```bash
   git fetch origin
   ```

1. Pas de bijgewerkte code aan.

   ```bash
   git pull origin <environment-ID>
   ```

>[!TIP]
>
>Zie [Integraties](../integrations/overview.md) voor informatie over het gebruik van Git-gebaseerde hostingservices met Adobe Commerce op cloudinfrastructuur.

## Een vertakking maken voor ontwikkeling

Nadat u uw project hebt gekloond en de configuratie van de Adobe Commerce-beheerdersaccount hebt bijgewerkt, kunt u zich vertakken voor ontwikkeling. Zoals eerder vermeld, moet u een omgeving maken die de `magento-cloud environment:branch <branch-name>` of de [!DNL Cloud Console] voor het milieu _actief_.

- Voor [Starter](../architecture/starter-develop-deploy-workflow.md#clone-and-branch)kunt u een vertakking maken voor `staging`en maakt u vervolgens een ontwikkelingsvertakking op basis van de `staging` vertakking.
- Voor [Pro](../architecture/pro-develop-deploy-workflow.md#development-workflow), ontwikkelingstakken maken op basis van de `Integration` vertakking.

**Een ontwikkelingsvertakking maken**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Maak een omgeving op basis van de vertakking die wordt aanbevolen voor de projectworkflow.

   ```bash
   magento-cloud branch <new-environment-name> integration
   ```

1. Afhankelijkheden bijwerken.

   ```bash
   composer --no-ansi --no-interaction install --no-progress --prefer-dist --optimize-autoloader
   ```

1. [_optioneel_] Een [back-up](../storage/snapshots.md) van het milieu

### Een vertakking samenvoegen

Voeg deze vertakking na het voltooien van de ontwikkeling samen met het bovenliggende element:

1. Wijzigingen in de code vastleggen en doorvoeren:

   ```bash
   git add -A && git commit -m "Add message here"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Samenvoegen met de bovenliggende omgeving:

   ```bash
   magento-cloud environment:merge <environment-ID>
   ```

### Een omgeving verwijderen

Verwijder een omgeving alleen als u zeker weet dat u deze niet meer nodig hebt. U kunt een omgeving niet herstellen nadat u deze hebt verwijderd.

>[!WARNING]
>
>U kunt het dialoogvenster `master` tak van elk project.

U moet een projectbeheerder, een milieubeheerder, of de Eigenaar van de Rekening zijn om deze taak uit te voeren. Zie [Toegang van gebruikers tot Cloud-projecten beheren](../project/user-access.md).

Wanneer u een omgeving verwijdert, wordt de omgeving ingesteld op _inactief_. De code is nog beschikbaar in de tak van het Git, maar bevat niet meer de diensten of het gegevensbestand. Als u de omgeving volledig wilt verwijderen, moet u ook de bijbehorende externe Git-vertakking verwijderen.

**Een omgeving verwijderen**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Updates ophalen van de externe server.

   ```bash
   git fetch
   ```

1. Verwijder de omgevingsvertakking.

   ```bash
   magento-cloud environment:delete <environment-ID>
   ```

   U kunt desgewenst meer dan één omgeving tegelijk verwijderen door meerdere milieu-id&#39;s toe te voegen aan de opdracht Verwijderen.

   ```bash
   magento-cloud environment:delete <environment-1-ID> <environment-2-ID>
   ```

1. Reageer op de vragen om de lokale omgeving en de bijbehorende externe omgeving te verwijderen.

   ```terminal
   The environment <environment-ID> is currently active: deleting it will delete all associated data.
   Are you sure you want to delete the environment <environment-ID>? [Y/n]
   ```

   Als u de omgeving verwijdert, wordt deze in een _inactief_ status.

   ```terminal
   Delete the remote Git branch too? [Y/n]
   ```

   Als u de externe Git-vertakking verwijdert, wordt de omgeving van het project verwijderd.

1. Wacht tot de omgeving is verwijderd.

   ```terminal
   Deleting environment <environment-ID>
   Waiting for the activity...
     Deleting environment <project-id>-<environment-ID>-xxxxxx
   
     [============================]  1 min (complete)
   Activity ID succeeded
   Deleted remote Git branch <environment-ID>
   Run git fetch --prune to remove deleted branches from your local cache.
   ```

>[!TIP]
>
>Als u een niet-actieve omgeving wilt activeren, gebruikt u de opdracht `magento-cloud environment:activate` gebruiken.

## Interactie met externe omgevingen

Na u [SSH-toetsen instellen](../development/secure-connections.md), kunt u [verbinding maken met een externe omgeving vanuit uw lokale werkruimte](../development/secure-connections.md#connect-to-a-remote-environment) en communiceert u met uw projectservices en wijzigt u instellingen.
