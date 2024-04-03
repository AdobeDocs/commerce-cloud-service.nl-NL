---
title: Schijfruimte beheren
description: Leer hoe u schijfruimte beheert met behulp van de opdrachtregelinterface.
feature: Cloud, Storage
exl-id: 480cb33b-ac83-441d-946e-5b4de09ad84e
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 0%

---

# Schijfruimte beheren

U kunt de totale opslagcapaciteit voor uw Cloud-project vinden in uw Adobe Commerce op basis van een cloudinfrastructuurcontract en op uw [accountpagina](https://accounts.magento.cloud/user). Op elke projectkaart in uw account wordt het aantal _omgevingen_ de _opslag_ capaciteit in GB en het aantal _gebruikers_. U kunt ook de volgende Cloud-opdracht gebruiken:

```bash
magento-cloud subscription:info | grep storage
```

Monsterrespons:

```terminal
| storage              | 51200
```

Wanneer een Pro-productie- of -testomgeving 95% van de opslagcapaciteit bereikt of overschrijdt, wordt met het hulpprogramma voor bewaking van de cloudinfrastructuur een supportwaarschuwing weergegeven waarin u op de hoogte wordt gesteld van een automatische toename van de opslagcapaciteit.

Voorbeeldmelding:

>[!BEGINSHADEBOX]

_&quot;Onze controle heeft dossieropslag op uw cluster (project-id-milieu) ontdekt bijna volledig. Het schijfgebruik bevindt zich momenteel op kritieke gebruiksniveaus met nog geen 1 GiB. Het volume van de gedeelde opslag wordt momenteel verhoogd van 60 GiB tot 70 GiB om uw diensten in gebruik te houden. Kijk eens naar het gebruik van productie- en staging-bestanden om te zien of u wat ruimte kunt opruimen.&quot;_

>[!ENDSHADEBOX]

>[!TIP]
>
>U wordt aangeraden regelmatig uw opslagcapaciteit te controleren en deze goed onder de 90% te houden om deze automatische verhogingen te voorkomen. Als deze eenmaal zijn toegewezen, kan de opslagverhoging voor Pro-opslag en -productie niet worden teruggedraaid.

## Integratieomgeving controleren

U kunt het schijfruimtegebruik voor uw integratiemilieu controleren gebruikend `magento-cloud` CLI.

**Schijfruimtegebruik bij benadering controleren**:

```bash
magento-cloud db:size
```

Monsterrespons:

```terminal
Checking database service mysql...

+----------------+-----------------+--------+
| Allocated disk | Estimated usage | % used |
+----------------+-----------------+--------+
| 2.0 GiB        | 193.3 MiB       | ~ 9%   |
+----------------+-----------------+--------+
```

Alle bevestigingen delen een schijf. U kunt met de `magento-cloud` CLI.

**Het geschatte gebruik van schijfruimte voor montage controleren**:

```bash
magento-cloud mount:size
```

Monsterrespons:

```terminal
Checking disk usage for all mounts on <project>-<environment>-mymagento@ssh.us.magento.cloud...

+------------+-----------+---------+-----------+-----------+--------+
| Mount(s)   | Size(s)   | Disk    | Used      | Available | % Used |
+------------+-----------+---------+-----------+-----------+--------+
| app/etc    | 184 KiB   | 1.9 GiB | 481.3 MiB | 1.4 GiB   | 24.7%  |
| pub/media  | 128 KiB   |         |           |           |        |
| pub/static | 158.2 MiB |         |           |           |        |
| var        | 316.7 MiB |         |           |           |        |
+------------+-----------+---------+-----------+-----------+--------+
```

## Specifieke clusters controleren

Voor Pro Staging- en Productieomgevingen kunt u het gebruik van schijfruimte in elke omgeving controleren met de `disk free` gebruiken, die de hoeveelheid schijfruimte rapporteert die door het bestandssysteem wordt gebruikt. U moet SSH gebruiken aan login aan een verre milieu.

```bash
df -h
```

De `-h` geeft het rapport weer met een leesbare indeling (KB, MB of GB).

In de volgende voorbeeldreactie wordt `/mnt/shared` de montage toont de schijfruimte voor media en `/data/mysql/` Bij monteren wordt schijfruimte voor de database weergegeven:

```terminal
Filesystem                                    Size  Used Avail Use% Mounted on
udev                                           16G     0   16G   0% /dev
tmpfs                                         3.2G  9.1M  3.2G   1% /run
/dev/xvda1                                     59G  8.9G   48G  16% /
tmpfs                                          16G   36K   16G   1% /dev/shm
tmpfs                                         5.0M     0  5.0M   0% /run/lock
tmpfs                                          16G     0   16G   0% /sys/fs/cgroup
/dev/xvdj                                     9.8G  2.3G  7.6G  23% /data/mysql
/dev/xvdi                                     9.8G  491M  9.3G   5% /data/exports
192.168.5.5:/shared                           9.8G  591M  9.3G   6% /mnt/shared
/dev/loop0                                     91M   91M     0 100% /app/project
192.168.5.5:/shared/project/var         9.8G  591M  9.3G   6% /app/project/var
192.168.5.5:/shared/project/app/etc     9.8G  591M  9.3G   6% /app/project/app/etc
192.168.5.5:/shared/project/pub/media   9.8G  591M  9.3G   6% /app/project/pub/media
192.168.5.5:/shared/project/pub/static  9.8G  591M  9.3G   6% /app/project/pub/static
```

U kunt de reactie beperken door een map op te geven. Bijvoorbeeld:

```bash
df -h var/
```

Monsterrespons:

```terminal
Filesystem                                    Size  Used Avail Use% Mounted on
192.168.5.5:/shared/project/var         9.8G  591M  9.3G   6% /app/project/var
```

## Schijfruimte toewijzen

Twee [configuratiebestanden](../environment/overview.md) de toewijzing van schijfruimte in de Cloud-omgeving regelen: de `.magento.app.yaml` en de `.magento/services.yaml` bestand. Elk bestand bevat de `disk` eigenschap, die de waarde van de schijfgrootte in MB voor de respectievelijke configuratie definieert. U kunt de toewijzing van schijfruimte alleen wijzigen in Pro-integratie- en Starter-omgevingen.

>[!IMPORTANT]
>
>Voor Pro Production- en Staging-omgevingen moet u [Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om de toewijzing van schijfruimte te wijzigen. Een grootteverhoging van de milieu&#39;s van de Proproductie en van het Staging kan slechts met bepaalde intervallen voorkomen, zodat, afhankelijk van uw huidig gebruik van de schijfruimte, de steun zou kunnen adviseren om schijftoewijzing met een minimum van 10 GB te verhogen. Als deze eenmaal zijn toegewezen, kan de opslagverhoging voor Pro-opslag en -productie niet worden teruggedraaid.

### Schijfruimte van toepassing

De `.magento.app.yaml` bestand bestuurt de [vaste schijfruimte](../application/properties.md#disk) beschikbaar voor de toepassing.

**De schijfruimte voor uw toepassing vergroten**:

1. Open in uw lokale ontwikkelomgeving de `.magento.app.yaml` configuratiebestand.

1. Een nieuwe waarde instellen voor de `disk` eigenschap (in MB).

   ```yaml
   disk: <value-mb>
   ```

1. Sla de wijzigingen op in het bestand.

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add .magento.app.yaml && git commit -m "Increase disk space for application" && git push origin <branch-name>
   ```

   De wijzigingen worden van kracht nadat u het bijgewerkte YAML-bestand naar de externe omgeving hebt geduwd.

### Schijfruimte van service

De `.magento/services.yaml` het dossier controleert de schijfruimte beschikbaar aan elke dienst, zoals MySQL en Redis.

**Om schijfruimte voor de dienst te verhogen**:

1. Open in uw lokale ontwikkelomgeving de `.magento/services.yaml` configuratiebestand.

1. Voeg een service toe of zoek een service in het bestand. Zie [meer over het vormen van de diensten](../services/services-yaml.md).

1. Stel een nieuwe waarde in voor de eigenschap disk (in MB).

   ```yaml
   <name>:
       type: <service-name>:<service-version>
       disk: <value-mb>
   ```

1. Sla de wijzigingen op in het bestand.

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add .magento/services.yaml && git commit -m "Increase disk space for service" && git push origin <branch-name>
   ```

   De wijzigingen worden van kracht nadat u het bijgewerkte YAML-bestand naar de externe omgeving hebt geduwd.

## Schijfruimte van monitor

In een Pro Production-omgeving kunt u de schijfruimte en andere prestatie-indicatoren controleren aan de hand van de Beheerde waarschuwingen voor het Adobe Commerce-waarschuwingsbeleid voor New Relic. Zie voor meer informatie [Prestaties bewaken met beheerde waarschuwingen](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts). Zie voor meer informatie [Aanbevolen procedures om prestatieproblemen met databases op te lossen](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html).

## Geen ruimte meer over

De buildcache kan na verloop van tijd groter worden. Als u een waarschuwing ontvangt dat de status `No space left on device`, probeer het bouwstijlgeheime voorgeheugen te ontruimen en opnieuw op te stellen:

```bash
magento-cloud project:clear-build-cache
```
