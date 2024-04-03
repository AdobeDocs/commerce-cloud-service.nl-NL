---
title: Logbestanden weergeven en beheren
description: Begrijp de typen logbestanden die beschikbaar zijn in de cloudinfrastructuur en waar u ze kunt vinden.
last-substantial-update: 2023-05-23T00:00:00Z
exl-id: d7f63dab-23bf-4b95-b58c-3ef9b46979d4
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---

# Logbestanden weergeven en beheren

Logbestanden voor Adobe Commerce voor infrastructuurprojecten in de cloud zijn handig voor het oplossen van problemen met betrekking tot [haken maken en implementeren](../application/hooks-property.md), cloudservices en de Adobe Commerce-toepassing.

U kunt de logboeken weergeven vanuit het bestandssysteem, de [!DNL Cloud Console]en de `magento-cloud` CLI.

- **Bestandssysteem**—De `/var/log` systeemdirectory bevat logboeken voor alle omgevingen. De `var/log/` Deze map bevat toepassingsspecifieke logs die uniek zijn voor een bepaalde omgeving. Deze mappen worden niet gedeeld tussen knooppunten in een cluster. In Pro Productie en het Staging milieu&#39;s, moet u de logboeken op elke knoop controleren.

- **[!DNL Cloud Console]**—U kunt bouw zien, opstellen, en post-opstellen logboekinformatie in het milieu _berichten_ lijst.

- **Cloud CLI**—U kunt logboeken van lokale milieu bekijken gebruikend `magento-cloud log` de opdracht of externe omgevingslogboeken gebruiken `magento-cloud ssh` gebruiken.

## Loglocaties

Systeemlogboeken worden opgeslagen op de volgende locaties:

- Integratie: `/var/log/<log-name>.log`
- Pro Staging: `/var/log/platform/<project-ID>_stg/<log-name>.log`
- Pro-productie: `/var/log/platform/<project-ID>/<log-name>.log`

De waarde van `<project-ID>` afhankelijk is van het project en of het milieu aan het staging of aan de productie is. Met bijvoorbeeld een project-id van `yw1unoukjcawe`, de Staging-omgevingsgebruiker is `yw1unoukjcawe_stg` en de productieomgeving `yw1unoukjcawe`.

Gebruikend dat voorbeeld, stelt logboek op is: `/var/log/platform/yw1unoukjcawe_stg/deploy.log`

### Logboeken voor externe omgevingen weergeven

De meeste logboeken omvatten gebeurtenissen die in het verre milieu voorkomen. Voor Pro, zijn er veelvoudige knopen en elke knoop heeft unieke logboeken. Gebruik het volgende om een lijst van alle gastheren te zien:

```bash
magento-cloud ssh -p <project-ID> -e <environment-ID> --all
```

Monsterrespons:

```terminal
1.ent-project-environment-id@ssh.region.magento.cloud
2.ent-project-environment-id@ssh.region.magento.cloud
3.ent-project-environment-id@ssh.region.magento.cloud
```

**Een lijst met externe omgevingslogboeken weergeven**:

```bash
magento-cloud ssh -e <environment-ID> "ls var/log"
```

Voorbeeld voor Pro:

```bash
ssh 1.ent-project-environment-id@ssh.region.magento.cloud "ls var/log | grep error"
```

**Een extern logboek weergeven**:

```bash
magento-cloud ssh -e <environment-ID> "cat var/log/cron.log"
```

Voorbeeld voor Pro:

```bash
ssh 1.ent-project-environment-id@ssh.region.magento.cloud "cat var/log/cron.log"
```

>[!TIP]
>
>In Pro-omgevingen zijn automatische rotatie, compressie en verwijdering van logbestanden ingeschakeld voor logbestanden met een vaste bestandsnaam. Elk logboekbestandstype heeft een roterend patroon en een levensduur. Starteromgevingen hebben geen logrotatie. U vindt volledige informatie over de logrotatie en de levensduur van gecomprimeerde logbestanden in de omgeving in: `/etc/logrotate.conf` en `/etc/logrotate.d/<various>`

## Logboeken samenstellen en implementeren

Na het duwen van veranderingen in uw milieu, kunt u het registreren van elke haak in herzien `var/log/cloud.log` bestand. Het logboek bevat begin en eindeberichten voor elke haak. In het volgende voorbeeld zijn de berichten &quot;`Starting post-deploy.`&quot; en &quot;`Post-deploy is complete.`&quot;

Controleer de tijdstempels op logboekingangen, verifieer, en bepaal de plaats van de logboeken voor een specifieke plaatsing. Hieronder ziet u een beknopt voorbeeld van loguitvoer die u kunt gebruiken voor het oplossen van problemen:

```terminal
Re-deploying environment project-integration-ID
  Executing post deploy hook for service `mymagento`
    [2019-01-03 19:44:11] NOTICE: Starting post-deploy.
    [2019-01-03 19:44:11] INFO: Validating configuration
    [2019-01-03 19:44:11] INFO: End of validation
    [2019-01-03 19:44:11] INFO: Enable cron
    [2019-01-03 19:44:11] INFO: Create backup of important files.
    [2019-01-03 19:44:11] INFO: Backup /app/app/etc/env.php.bak for /app/app/etc/env.php was created.
    [2019-01-03 19:44:11] INFO: Backup /app/app/etc/config.php.bak for /app/app/etc/config.php was created.
    [2019-01-03 19:44:11] INFO: php ./bin/magento cache:flush --ansi --no-interaction
    [2019-01-03 19:44:32] INFO: Warming up failed: http://integration-id-project.us.magentosite.cloud/
    [2019-01-03 19:44:32] NOTICE: Post-deploy is complete.
```

>[!TIP]
>
>Wanneer u uw Cloud-omgeving configureert, kunt u [op logbestanden gebaseerde Slack- en e-mailmeldingen](../environment/set-up-notifications.md) voor bouw en stel acties op.

De volgende logboeken hebben een gemeenschappelijke plaats voor alle projecten van de Wolk:

- **Implementatielogboek**: `var/log/cloud.log`
- **Logbestand met laatste implementatiefout**: `var/log/cloud.error.log`
- **Foutopsporingslogbestand**: `var/log/debug.log`
- **Uitzonderingslogboek**: `var/log/exception.log`
- **Systeemlogboek**: `var/log/system.log`
- **Ondersteuningslogboek**: `var/log/support_report.log`
- **Rapporten**: `var/report/`

Hoewel de `cloud.log` Het dossier bevat terugkoppelt van elk stadium van het plaatsingsproces, logboeken die door de opstellen haak worden gecreeerd zijn uniek aan elke milieu. Het milieu-specifieke opstellen logboek is in de volgende folders:

- **Starter en Pro-integratie**: `/var/log/deploy.log`
- **Pro Staging**: `/var/log/platform/<project-ID>_stg/deploy.log`
- **Pro Production**: `/var/log/platform/<project-ID>/deploy.log`

### Logbestand implementeren

Het logboek voor elke plaatsing schakelt aan specifiek samen `deploy.log` bestand. Het volgende voorbeeld drukt het opstellen logboek van het huidige milieu in de terminal af:

```bash
magento-cloud log -e <environment-ID> deploy
```

Monsterrespons:

```terminal
Reading log file projectID-branchname-ID--mymagento@ssh.zone.magento.cloud:/var/log/'deploy.log'

[2023-04-24 18:58:03.080678] Launching command 'b'php ./vendor/bin/ece-tools run scenario/deploy.xml\n''.

[2023-04-24T18:58:04.129888+00:00] INFO: Starting scenario(s): scenario/deploy.xml (magento/ece-tools version: 2002.1.14, magento/magento2-base version: 2.4.6)
[2023-04-24T18:58:04.364714+00:00] NOTICE: Starting pre-deploy.
...
```

{{scd-timing-warning}}

### Foutlogboek

De fout en de waarschuwingsberichten die tijdens het plaatsingsproces worden geproduceerd worden geschreven aan zowel `var/log/cloud.log` en de `var/log/cloud.error.log` bestanden. Het logbestand met fouten in de cloud bevat alleen fouten en waarschuwingen van de meest recente implementatie. Een leeg bestand geeft aan dat de implementatie zonder fouten is gelukt.

U kunt het logbestand weergeven met de opdracht [Cloud CLI SSH](#view-remote-environment-logs)U kunt ook ECE-Tools gebruiken om de fouten weer te geven met suggesties:

```bash
magento-cloud ssh -e <environment-ID> "./vendor/bin/ece-tools error:show"
```

Monsterrespons:

```terminal
errorCode: 1001
stage: build
step: validate-config
suggestion: Please run the following commands:
1. bin/magento module:enable --all
2. git add -f app/etc/config.php
3. git commit -m 'Adding config.php'
4. git push
title: File app/etc/config.php does not exist
type: warning
---------------

errorCode: 1006
stage: build
step: validate-config
suggestion: Your application does not have the "post_deploy" hook enabled.
  In order to minimize downtime, add the following to ".magento.app.yaml":
  hooks:
      post_deploy: |
          php ./vendor/bin/ece-tools run scenario/post-deploy.xml
title: The configured state is not ideal
type: warning
```

De meeste foutberichten bevatten een beschrijving en voorgestelde actie. Gebruik de [Referentie van foutbericht voor ECE-Tools](../dev-tools/error-reference.md) om de foutcode voor verdere instructies te raadplegen. Voor verdere richtsnoeren gebruikt u de [Adobe Commerce-probleemoplossing voor implementatie](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-deployment-troubleshooter.html).

## Toepassingslogboeken

Toepassingslogboeken zijn net als logboeken voor implementatie uniek voor elke omgeving:

| Logbestand | Starter en Pro-integratie | Beschrijving |
| ------------------- | --------------------------- | ------------------------------------------------- |
| **Logbestand implementeren** | `/var/log/deploy.log` | Activiteit van de [inzetten, haak](../application/hooks-property.md). |
| **Logboek na implementatie** | `/var/log/post_deploy.log` | Activiteit van de [naimplementatiehaak](../application/hooks-property.md). |
| **Uitsnijdlog** | `/var/log/cron.log` | Uitvoer van snijtaken. |
| **Logboek voor Nginx-toegang** | `/var/log/access.log` | Bij Nginx-start worden HTTP-fouten gegenereerd voor ontbrekende mappen en uitgesloten bestandstypen. |
| **Logbestand met fouten in Nginx** | `/var/log/error.log` | Opstartberichten die nuttig zijn voor foutopsporing in configuratiefouten die aan Nginx zijn gekoppeld. |
| **PHP-toegangslogboek** | `/var/log/php.access.log` | Verzoeken aan de PHP service. |
| **PHP FPM log** | `/var/log/app.log` | |

Voor Pro Staging- en productieomgevingen zijn de logbestanden Implementeren, Post-implementeren en Uitsnijden alleen beschikbaar op het eerste knooppunt in de cluster:

| Logbestand | Pro Staging | Pro Production |
| ------------------- | --------------------------------------------------- | ----------------------------------------------- |
| **Logbestand implementeren** | Alleen eerste knooppunt:<br>`/var/log/platform/<project-ID>_stg/deploy.log` | Alleen eerste knooppunt:<br>`/var/log/platform/<project-ID>/deploy.log` |
| **Logboek na implementatie** | Alleen eerste knooppunt:<br>`/var/log/platform/<project-ID>_stg/post_deploy.log` | Alleen eerste knooppunt:<br>`/var/log/platform/<project-ID>/post_deploy.log` |
| **Uitsnijdlog** | Alleen eerste knooppunt:<br>`/var/log/platform/<project-ID>_stg/cron.log` | Alleen eerste knooppunt:<br>`/var/log/platform/<project-ID>/cron.log` |
| **Logboek voor Nginx-toegang** | `/var/log/platform/<project-ID>_stg/access.log` | `/var/log/platform/<project-ID>/access.log` |
| **Logbestand met fouten in Nginx** | `/var/log/platform/<project-ID>_stg/error.log` | `/var/log/platform/<project-ID>/error.log` |
| **PHP-toegangslogboek** | `/var/log/platform/<project-ID>_stg/php.access.log` | `/var/log/platform/<project-ID>/php.access.log` |
| **PHP FPM log** | `/var/log/platform/<project-ID>_stg/php5-fpm.log` | `/var/log/platform/<project-ID>/php5-fpm.log` |

### Gearchiveerde logbestanden

De toepassingslogboeken worden eenmaal per dag gecomprimeerd en gearchiveerd en één jaar bewaard. De gecomprimeerde logbestanden krijgen een naam met een unieke id die overeenkomt met de naam `Number of Days Ago + 1`. In Pro-productieomgevingen wordt bijvoorbeeld een PHP-toegangslogboek voor 21 dagen in het verleden opgeslagen en als volgt benoemd:

```terminal
/var/log/platform/<project-ID>/php.access.log.22.gz
```

De gearchiveerde logboekdossiers worden altijd opgeslagen in de folder waar het originele dossier vóór compressie werd gevestigd.

>[!NOTE]
>
>**Implementeren** en **Na implementatie** logbestanden worden niet geroteerd en gearchiveerd. De volledige plaatsingsgeschiedenis wordt geschreven binnen die logboekdossiers.

## Servicelogboeken

Omdat elke dienst in een afzonderlijke container loopt, zijn de de dienstlogboeken niet beschikbaar in het integratiemilieu. Adobe Commerce on cloud Infrastructure biedt alleen toegang tot de webservercontainer in de integratieomgeving. De volgende locaties van het servicelogboek zijn bestemd voor de Pro Production- en Staging-omgevingen:

- **Redis log**: `/var/log/platform/<project-ID>_stg/redis-server-<project-ID>_stg.log`
- **Logboek Elasticsearch**: `/var/log/elasticsearch/elasticsearch.log`
- **Java garbage collection log**: `/var/log/elasticsearch/gc.log`
- **E-maillogboek**: `/var/log/mail.log`
- **MySQL foutenlogboek**: `/var/log/mysql/mysql-error.log`
- **MySQL slowaakse logboeken**: `/var/log/mysql/mysql-slow.log`
- **RabbitMQ-logboek**: `/var/log/rabbitmq/rabbit@host1.log`

De logboeken van de dienst worden gearchiveerd en voor verschillende periodes, afhankelijk van het logboektype bewaard. In MySQL-logboeken is bijvoorbeeld de kortste levensduur verwijderd na zeven dagen.

>[!TIP]
>
>De bestandslocaties van logbestanden in de geschaalde architectuur zijn afhankelijk van het type knooppunt. Zie [Loglocaties in de geschaalde architectuur](../architecture/scaled-architecture.md#log-locations) onderwerp.

## Loggegevens voor Pro Production en Staging

In Pro-productie- en staging-omgevingen kunt u [New Relic-logbeheer](../monitor/log-management.md) geïntegreerd met uw project voor het beheer van geaggregeerde loggegevens van alle logbestanden die bij uw Adobe Commerce horen voor het infrastructuurproject in de cloud.

De New Relic Logs-toepassing biedt een gecentraliseerd logbeheerdashboard om Adobe Commerce problemen op te lossen en te controleren in productieomgevingen en testomgevingen voor cloudinfrastructuur. Het dashboard verleent ook toegang tot logboekgegevens voor de Snelle diensten van CDN, de Optimalisering van het Beeld, en van de de toepassingsfirewall van het Web (WAF). Zie [New Relic-services](../monitor/new-relic-service.md).
