---
title: Back-up maken van de database
description: Leer hoe u met ECE-tools een back-up kunt maken van de database voor een Adobe Commerce on cloud-infrastructuurproject.
feature: Cloud, Iaas, Storage
exl-id: 8a96effe-a587-4edf-b0c7-e73ca8d3b56c
source-git-commit: 4d790bff2ba5d02ef10de5c36a2f0d140e31a407
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Back-up maken van de database

U kunt een kopie van uw database maken met de `ece-tools db-dump` bevel zonder alle omgevingsgegevens van de diensten en de steunen te vangen. Met deze opdracht maakt u standaard back-ups in het dialoogvenster `/app/var/dump-main` directory voor alle databaseverbindingen die in de omgevingsconfiguratie zijn opgegeven. De de stortplaatsverrichting van DB schakelt de toepassing aan onderhoudswijze, houdt de processen van de consumentenrij tegen, en maakt cron banen onbruikbaar alvorens de stortplaats begint.

Overweeg de volgende richtlijnen voor stortplaats van DB:

- Voor Productomgevingen, adviseert de Adobe de verrichtingen van de gegevensbestandstortplaats tijdens off-peak uren te voltooien om de dienstverstoringen te minimaliseren die voorkomen wanneer de plaats op onderhoudswijze is.
- Als een fout tijdens de stortplaatsverrichting voorkomt, schrapt het bevel het stortplaatsdossier om schijfruimte te besparen. Bekijk de logboeken voor meer informatie (`var/log/cloud.log`).
- Voor ProProductie-omgevingen wordt deze opdracht alleen dumpt vanuit _één_ van de drie high-availability knopen, zodat zouden de productiegegevens die aan een verschillende knoop tijdens de stortplaats worden geschreven niet kunnen worden gekopieerd. De opdracht genereert een `var/dbdump.lock` bestand om te voorkomen dat de opdracht op meer dan één knooppunt wordt uitgevoerd.
- Voor een back-up van alle milieuservices raadt de Adobe aan een [back-up](snapshots.md).

U kunt verkiezen aan file veelvoudige gegevensbestanden door de gegevensbestandnamen aan het bevel toe te voegen. In het volgende voorbeeld wordt een back-up gemaakt van twee databases: `main` en `sales`:

```bash
php vendor/bin/ece-tools db-dump main sales
```

Gebruik de `php vendor/bin/ece-tools db-dump --help` voor meer opties:

- `--dump-directory=<dir>`—Kies een doeldirectory voor de databasedumpel
- `--remove-definers`—Verwijder DEFINER-instructies uit de databasedumpit

**Om een gegevensbestandstortplaats in het Opvoeren of het milieu van de Productie te creëren**:

1. [SSH gebruiken om u aan te melden of een tunnel te maken om verbinding te maken met de externe omgeving](../development/secure-connections.md) die de te kopiëren database bevat.

1. Maak een lijst van de omgevingsverhoudingen en neem nota van de gegevens van de gegevensbestandlogin.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   of

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]))->database);'
   ```

1. Maak een back-up van de database. Om een doelfolder voor de stortplaats van DB te kiezen, gebruik `--dump-directory` -optie.

   ```bash
   php vendor/bin/ece-tools db-dump -- main
   ```

   Monsterrespons:

   ```terminal
   The db-dump operation switches the site to maintenance mode, stops all active cron jobs and consumer queue processes, and disables cron jobs before starting the dump process.
   Your site will not receive any traffic until the operation completes.
   Do you wish to proceed with this process? (y/N)? y
   2020-01-28 16:38:08] INFO: Starting backup.
   [2020-01-28 16:38:08] NOTICE: Enabling Maintenance mode
   [2020-01-28 16:38:10] INFO: Trying to kill running cron jobs and consumers processes
   [2020-01-28 16:38:10] INFO: Running Magento cron and consumers processes were not found.
   [2020-01-28 16:38:10] INFO: Waiting for lock on db dump.
   [2020-01-28 16:38:10] INFO: Start creation DB dump for main database...
   [2020-01-28 16:38:10] INFO: Finished DB dump for main database, it can be found here: /tmp/qxmtlseakof6y/dump-main-1580229490.sql.gz
   [2020-01-28 16:38:10] INFO: Backup completed.
   [2020-01-28 16:38:11] NOTICE: Maintenance mode is disabled.
   ```

1. De `db-dump` maakt een opdracht `dump-<timestamp>.sql.gz` archiefbestand in de externe projectmap.

>[!TIP]
>
>Als u deze gegevens naar een specifieke omgeving wilt verplaatsen, raadpleegt u [Gegevens en statische bestanden migreren](../deploy/staging-production.md#migrate-static-files).
