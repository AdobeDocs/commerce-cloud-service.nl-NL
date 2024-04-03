---
title: Distribueren naar Staging en Productie
description: Leer hoe u uw Adobe Commerce-code voor cloudinfrastructuur kunt implementeren in de Staging- en Productomgevingen voor verdere tests.
feature: Cloud, Console, Deploy, SCD, Storage
exl-id: 4b82289f-ee04-4b14-a0ed-7a8a19fc6a6a
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 0%

---

# Distribueren naar Staging en Productie

Het proces voor het opstellen en het gaan leven begint met ontwikkeling, blijft het Opvoeren, en eindigt met het leven in Productie. De Adobe verstrekt een milieu-oplossing van begin tot eind om verenigbare configuraties te verzekeren. Elke milieu steunt directe toegang URL tot de storefront en Admin en toegang SSH voor CLI bevelen.

Wanneer u klaar bent om uw opslag op te stellen, moet u plaatsing en het testen op het Opvoeren milieu voltooien alvorens aan Productie op te stellen. Deze sectie bevat diepgaande instructies en informatie over het proces voor het maken en implementeren, het migreren van gegevens en inhoud en het testen.

>[!TIP]
>
>Adobe beveelt aan een [back-up](../storage/snapshots.md) van de omgeving vóór implementatie.

Ook kunt u [Implementaties bijhouden met New Relic](../monitor/track-deployments.md) om plaatsingsgebeurtenissen te controleren en u te helpen prestaties tussen plaatsingen analyseren.

## Startimplementatiestroom

Adobe beveelt aan een `staging` vertakking van `master` vertakking om uw het planontwikkeling en plaatsing van de Aanzet het best te steunen. Dan hebt u twee van uw vier actieve milieu&#39;s klaar: `master` voor productie en `staging` voor Staging.

Zie voor meer informatie over het proces [Starter Developer and Deploy Workflow](../architecture/starter-develop-deploy-workflow.md).

## Pro-implementatiestroom

Pro wordt geleverd met een grote integratieomgeving met twee actieve vertakkingen, een wereldwijd `master` vertakkingen, Staging en Productie. Wanneer u uw project creeert, is de code klaar om zich te vertakken, te ontwikkelen, en te duwen voor de bouw van en het opstellen van uw plaats. Hoewel de integratieomgeving vele vertakkingen kan hebben, hebben het Staging en de Productie slechts één tak voor elk milieu.

Zie voor meer informatie over het proces [Pro-workflow voor ontwikkelen en implementeren](../architecture/pro-develop-deploy-workflow.md).

## Code implementeren naar fasering

De het Staging milieu verstrekt een bijna-productiemilieu dat een gegevensbestand, Webserver, en alle diensten met inbegrip van Fastly en New Relic omvat. U kunt volledig duwen, samenvoegen en opstellen door [[!DNL Cloud Console]](../project/overview.md) of [Cloud CLI-opdrachten](../dev-tools/cloud-cli-overview.md) via een terminaltoepassing.

### Code implementeren met de [!DNL Cloud Console]

De [!DNL Cloud Console] biedt functies voor het maken, beheren en implementeren van code in integratie-, staging- en productieomgevingen voor Starter- en Pro-plannen.

**Implementeer voor Pro-projecten de integratiesector in de testfase**:

1. [Aanmelden](https://accounts.magento.cloud) naar uw project.
1. Selecteer de `integration` vertakking.
1. Selecteer de **Samenvoegen** optie voor implementatie in Staging.

   ![Samenvoegen](../../assets/button-merge.png){width="150"}

1. Alles voltooien [testen](../test/staging-and-production.md) in de testomgeving.
1. Selecteer de optie **Samenvoegen** optie om in Productie op te stellen.

**Voor Starter, stel de ontwikkelingstak aan het opvoeren op**:

1. [Aanmelden](https://accounts.magento.cloud) naar uw project.
1. Selecteer de voorbereide codevertakking.
1. Selecteer de **Samenvoegen** optie voor implementatie in Staging.

   ![Samenvoegen](../../assets/button-merge.png){width="150"}

1. Alles voltooien [testen](../test/staging-and-production.md) in de testomgeving.
1. Selecteer de optie **Samenvoegen** optie om in te zetten op productie (`master`).

### Code implementeren met de opdrachtregel

De Cloud CLI bevat opdrachten voor het implementeren van code. U hebt SSH en Git toegang tot uw project nodig.

#### Stap 1: Implementeer en test de integratieomgeving

1. Na het registreren in het project, controleer het integratiemilieu:

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

1. Synchroniseer uw lokale integratieomgeving met de externe omgeving:

   ```bash
   magento-cloud environment:synchronize <environment-ID>
   ```

1. Maak een momentopname van de omgeving als back-up:

   ```bash
   magento-cloud snapshot: create -e <environment-ID>
   ```

1. Werk de code in uw lokale vertakking naar wens bij.

1. Wijzigingen aan de omgeving toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add -A && git commit -m "Commit message" && git push origin <environment-ID>
   ```

1. Volledige sitetests.

#### Stap 2: De veranderingen van de fusie in het Staging en stelt op

1. Bekijk de testomgeving:

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

1. Synchroniseer uw lokale Staging-omgeving met de externe omgeving:

   ```bash
   magento-cloud environment:synchronize <environment-ID>
   ```

1. Maak een momentopname van de omgeving als back-up:

   ```bash
   magento-cloud snapshot: create -e <environment-ID>
   ```

1. Voeg de integratieomgeving samen tot Staging om te implementeren:

   ```bash
   magento-cloud environment:merge <integration-ID>
   ```

1. Volledige sitetests.

#### Stap 3: Distribueren naar productie

1. U kunt een momentopname van uw lokale productieomgeving uitchecken, synchroniseren en maken.

1. Voeg de het Staging milieu aan Productie samen om op te stellen:

   ```bash
   magento-cloud environment:merge <staging-ID>
   ```

1. Volledige sitetests.

## Statische bestanden migreren

[Statische bestanden](https://experienceleague.adobe.com/docs/commerce-operations/operational-playbook/glossary.html) worden opgeslagen in `mounts`. Er zijn twee methoden voor het migreren van bestanden van een bronmontagelocatie, zoals uw lokale omgeving, naar een doellocatie. Beide methoden gebruiken de `rsync` nut, maar de Adobe adviseert het gebruiken van `magento-cloud` CLI voor het verplaatsen van bestanden tussen de lokale en externe omgeving. En Adobe raadt u aan de `rsync` methode voor het verplaatsen van bestanden van een externe bron naar een andere externe locatie.

### Bestanden migreren met CLI

U kunt de `mount:upload` en `mount:download` CLI bevelen om dossiers tussen het lokale en verre milieu te migreren. Beide opdrachten gebruiken de `rsync` nut, maar de CLI bevelen verstrekken opties en herinneringen die aan de Adobe Commerce op het milieu van de wolkeninfrastructuur worden aangepast. Bijvoorbeeld, als u het eenvoudige bevel zonder opties gebruikt, vraagt CLI u om te selecteren welke optelling of ophangingen om te uploaden of te downloaden.

```bash
magento-cloud mount:download
```

Monsterrespons:

```terminal
Enter a number to choose a mount to download from:
  [0] app/etc
  [1] pub/static
  [2] var
  [3] pub/media
  [4] All mounts
 > 3

Target directory: ~/pub/media/

Downloading files from the remote mount pub/media to pub/media

Are you sure you want to continue? [Y/n] Y
```

**Bestanden uploaden van een lokale `pub/media/` naar de externe map `pub/media/` map voor de huidige omgeving**:

```bash
magento-cloud mount:upload --source /path/to/project/pub/media/ --mount pub/media/
```

Monsterrespons:

```terminal
Uploading files from pub/media to the remote mount pub/media

Are you sure you want to continue? [Y/n] Y

  building file list ...   done
  ./
  sample-file.jpeg

  sent 8.43K bytes  received 48 bytes  3.39K bytes/sec
  total size is 154.57K  speedup is 18.23
```

Gebruik de `--help` voor de `mount:upload` en `mount:download` voor meer opties. Er is bijvoorbeeld een `--delete` om tijdens de migratie overbodige bestanden te verwijderen.

### Bestanden migreren via synchroniseren

U kunt ook de opdracht `rsync` gebruiken om bestanden te migreren.

```bash
rsync -azvP <source> <destination>
```

Voor deze opdracht worden de volgende opties gebruikt:

- `a`-archive
- `z`-bestanden comprimeren tijdens de migratie
- `v`-verbose
- `P`gedeeltelijke voortgang

Zie [rsync](https://linux.die.net/man/1/rsync) help.

>[!NOTE]
>
>Om media van ver-aan-verre milieu&#39;s direct over te brengen, moet u de agent van SSH toelaten door:sturen, zie [GitHub-richtlijnen](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/using-ssh-agent-forwarding).

**Statische bestanden rechtstreeks migreren van externe naar externe omgevingen (snelle benadering)**:

1. Gebruik SSH om u aan te melden bij de bronomgeving. Gebruik de `magento-cloud` CLI. Met de `-A` de optie is belangrijk omdat het door:sturen van de verbinding van de authentificatieagent toelaat.

   >[!TIP]
   >
   >Als u de **SSH-toegang** koppeling in uw [!DNL Cloud Console], selecteert u de omgeving en klikt u op **Site openen**.

   ```bash
   ssh -A <environment_ssh_link@ssh.region.magento.cloud>
   ```

1. Gebruik de `rsync` de opdracht kopiëren `pub/media` van uw bronomgeving naar een andere externe omgeving.

   ```bash
   rsync -azvP pub/media/ <destination_environment_ssh_link@ssh.region.magento.cloud>:pub/media/
   ```

1. Meld u aan bij de andere externe omgeving om te controleren of de bestanden correct zijn gemigreerd.

## De database migreren

>[!WARNING]
>
>Het importeren en exporteren van databases kan veel tijd in beslag nemen. Dit kan de prestaties en beschikbaarheid van de site beïnvloeden. Plan de invoer en de uitvoerverrichtingen tijdens off-piekuren om langzame prestaties of stroomonderbrekingen op de plaatsen van de Productie te verhinderen.

>[!BEGINSHADEBOX]

**Vereiste:** Een gegevensbestandstortplaats (zie Stap 3) zou gegevensbestandtrekkers moeten omvatten. Bevestig dat u de [TRIGGER-bevoegdheid](https://dev.mysql.com/doc/refman/5.7/en/privileges-provided.html#priv_trigger).

>[!IMPORTANT]
>
>De gegevensbank van het integratiemilieu is strikt voor ontwikkelingstests en kan gegevens omvatten die u niet in het Opvoeren en Productie wilt migreren.

Voor continue integratie-implementaties, Adobe **adviseert niet** migrerende gegevens van Integratie aan het Opvoeren en Productie. U kunt testgegevens doorgeven of belangrijke gegevens overschrijven. Om het even welke vitale configuraties worden overgegaan gebruikend [configuratiebestand](../store/store-settings.md) en `setup:upgrade` bevel tijdens bouwstijl en opstellen.

>[!ENDSHADEBOX]

Adobe **beveelt aan** Gegevens migreren van Productie naar Staging om uw site volledig te testen en op te slaan in een vrijwel productieomgeving met alle services en instellingen.

>[!NOTE]
>
>Om media van ver-aan-verre milieu&#39;s rechtstreeks over te brengen moet u ssh agent het door:sturen toelaten, zie [GitHub-richtlijnen](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/using-ssh-agent-forwarding).

### Back-up maken van de database

U kunt het beste een back-up van de database maken. In de volgende procedure worden de richtsnoeren van [Back-up maken van de database](../storage/database-dump.md).

**Om het gegevensbestand te dumpen**:

1. [SSH gebruiken om u aan te melden bij de externe omgeving](../development/secure-connections.md#use-an-ssh-command) die de te kopiëren database bevat.

1. Maak een lijst van de omgevingsverhoudingen en neem nota van de gegevens van de gegevensbestandlogin.

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]))->database);'
   ```

   Voor Pro Staging en Productie staat de naam van de database in het dialoogvenster `MAGENTO_CLOUD_RELATIONSHIPS` variabele (doorgaans dezelfde naam als de toepassingsnaam en gebruikersnaam).

1. Maak een back-up van de database. Om een doelfolder voor de stortplaats van DB te kiezen, gebruik `--dump-directory` -optie.

   Voor Starter-omgevingen en Pro-integratieomgevingen kunt u `main` als naam van de database:

   ```bash
   php vendor/bin/ece-tools db-dump main
   ```

   Snelopties:
   - `--dump-directory=<dir>`—Kies een doeldirectory voor de databasedumpel
   - `--remove-definers`—Verwijder DEFINER-instructies uit de databasedumpit

1. Hoewel de ECE-Hulpmiddelen methode de voorkeur heeft, moet een andere methode een dossier van de gegevensbestandstortplaats creëren gebruikend inheems MySQL in formaat GZIP.

   ```bash
   mysqldump -h <database-host> --user=<database-username> --password=<password> --single-transaction --triggers <database-name> | gzip - > /tmp/database.sql.gz
   ```

   Als u tweefelige authentificatie op het doelmilieu hebt gevormd, is het beter om verwante 2FA lijsten uit te sluiten om het te vermijden opnieuw vormend na gegevensbestandmigratie:

   ```bash
   mysqldump -h <database-host> --user=<database-username> --password=<password> --single-transaction --triggers --ignore-table=<database-name>.tfa_user_config --ignore-table=<database-name>.tfa_country_codes <database-name> | gzip - > /tmp/database.sql.gz
   ```

1. Type `logout` om de verbinding van SSH te eindigen.

### De database neerzetten en opnieuw maken

Bij het importeren van gegevens moet u een database neerzetten en maken.

**De database neerzetten en opnieuw maken**:

1. Een [SSH-tunnel](../development/secure-connections.md#ssh-tunneling) naar de externe omgeving.

1. Maak verbinding met de databaseservice.

   ```bash
   mysql --host=127.0.0.1 --user='<database-username>' --pass='<user-password>' --database='<name>' --port='<port>'
   ```

1. Bij de `MariaDB [main]>` vragen, de database neerzetten.

   Voor Starter- en Pro-integratie:

   ```shell
   drop database main;
   ```

   Voor productie:

   ```shell
   drop database <cluster-id>;
   ```

   Voor opmaken:

   ```shell
   drop database <cluster-ID_stg>;
   ```

1. Maak de database opnieuw.

   Voor Starter- en Pro-integratie:

   ```shell
   create database main;
   ```

   Invoer voor productie:

   ```shell
   zcat <cluster-ID>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <database-username> <database-name>;
   ```

   Importeren voor faseren:

   ```shell
   zcat <cluster-ID_stg>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <database-username> <database-name>;
   ```
