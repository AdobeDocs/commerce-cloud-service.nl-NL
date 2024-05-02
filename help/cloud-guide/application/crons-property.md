---
title: Crons, eigenschap
description: Zie voorbeelden op hoe te om het bezit ` crons ` in te vormen [!DNL Commerce] toepassingsconfiguratiebestand.
feature: Cloud, Configuration
exl-id: 67d592c1-2933-4cdf-b4f6-d73cd44b9f59
source-git-commit: 1c0e05c3d8461bea473bcf6ec35162d65ef2774f
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 0%

---

# Crons, eigenschap

Adobe Commerce gebruikt de `crons` eigendom om herhalende activiteiten te plannen. Het is ideaal voor het plannen van een specifieke taak om op bepaalde tijden van de dag te lopen. Vanwege de aard van alleen-lezen omgevingen kan slechts één snijtaak tegelijk op de webinstantie voor Adobe Commerce worden uitgevoerd voor cloudinfrastructuurprojecten. Het is aan te raden om taken die al lang worden uitgevoerd, op te splitsen in kleinere taken in een wachtrij. U kunt ook een [arbeidersinstantie](workers-property.md).

Adobe raadt u aan `crons` als de [eigenaar van bestandssysteem](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html). Do _niet_ run `crons` als `root` of als gebruiker van de webserver.

Deze configuratie is anders dan plaatsingen in het gebouw van Adobe Commerce, die veelvoudige standaard kantelbanen hebben. Zie [Cron-taken configureren](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html) in de _Configuratiegids_.

## Uitsnijdtaken instellen

De `crons` het bezit beschrijft processen die op een programma worden teweeggebracht. Voor elke taak zijn een naam en de volgende opties vereist:

- `spec`—De expressie voor uitsnijden die wordt gebruikt voor planning.
- `cmd`—De opdracht die moet worden uitgevoerd `start` en `stop`.
- `shutdown_timeout`—(_Optioneel_) Als een uitsnijdtaak wordt geannuleerd, is dit het aantal seconden waarna een SIGKILL-signaal wordt verzonden om de taak of het proces te stoppen. De standaardwaarde is 10 seconden.
- `timeout`—(_Optioneel_) De maximale tijdsduur dat een uitsnijdtaak kan worden uitgevoerd vóór een time-out. De standaardwaarde is 86400 seconden (24 uur).

Standaard heeft elk Commerce-wolkenproject de volgende standaardinstelling `crons` in de `.magento.app.yaml` bestand:

```yaml
crons:
    cronrun:
        spec: "* * * * *"
        cmd: "php bin/magento cron:run"
```

Als voor uw project aangepaste uitsnijdtaken zijn vereist, kunt u deze aan de standaardtaken toevoegen `crons` configuratie. Zie [Een uitsnijdtaak maken](#build-a-cron-job).

### `crontab`

Adobe Commerce heeft alleen een auto-crons-configuratieoptie toegevoegd aan Pro-projecten ter ondersteuning van de zelfbediening `crons` configuratie in de Staging- en Productomgevingen. Als deze optie is ingeschakeld, kunt u `crontab` om de uitsnijdconfiguratie te bekijken. Dit is _niet_ beschikbaar bij Starter-projecten.

Hoewel u `crontab` Adobe Commerce gebruikt deze methode niet om de configuratie van Pro-projecten te controleren `crontab` voor het uitvoeren van cron-taken voor sites die worden geïmplementeerd op de cloudinfrastructuur.

**Snijconfiguratie controleren in Pro-omgevingen**:

1. Gebruiken [SSH](../development/secure-connections.md#use-an-ssh-command) aan login aan het verre milieu.

1. Vermeld de geplande uitsnijdprocessen.

   ```shell
   crontab -l
   ```

   >[!NOTE]
   >
   >Als de `crontab -l` command retourneert een `Command not found` fout (alleen in Pro Staging- en Production-omgevingen): [Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om de auto-crons zelfbedienings configuratieoptie op uw project toe te laten.

In het volgende voorbeeld wordt het `crontab` uitvoer voor een omgeving die alleen de standaardinstelling heeft `crons` configuratie:

```terminal
username@hostname:~$ crontab -l
# Crontab is managed by the system, attempts to edit it directly will fail.
SHELL=/etc/platform/6fck2obu3244c/cron-run
MAILTO=""

# m h  dom mon dow  job_name

* * * * *           cronrun
```

## Een uitsnijdtaak maken

Een uitsnijdtaak bevat de planning- en tijdspecificatie en de opdracht die op de geplande tijd moet worden uitgevoerd. Voor Starter-omgevingen en Pro `integration` in omgevingen is het minimale interval eenmaal per vijf minuten. Voor Pro het Staging en van de Productie milieu&#39;s, is het minimuminterval eens per minuut. In Adobe Commerce op cloudinfrastructuur voegt u aangepaste uitsnijdtaken toe aan de `.magento.app.yaml` in het `crons` sectie. De algemene notatie is `spec` voor planning en `cmd` om de opdracht of het aangepaste script op te geven dat moet worden uitgevoerd.

### Specificatie

Adobe Commerce gebruikt een expressie van vijf waarden voor een `crons` specificatie (specificatie): `* * * * *`

1. Minuut (0 tot en met 59) Voor alle Starter- en Pro-omgevingen is de minimale frequentie die wordt ondersteund voor taken voor cron vijf minuten. Mogelijk moet u instellingen configureren in uw beheerder.
2. Uur (0 tot en met 23)
3. Dag van de maand (1 tot en met 31)
4. Maand (1 tot en met 12)
5. Dag van de week (0 tot en met 6) (zondag tot en met zaterdag; 7 is ook zondag op sommige systemen)

Enkele voorbeelden:

- `00 */3 * * *` om de drie uur op de eerste minuut (12:00, 3:00, 6:00 uur)
- `20 */8 * * *` om de 8 uur om de 20 uur (12:20, 8:20, 4:20)
- `00 00 * * *` eenmaal daags om middernacht
- `00 * * * 1` loopt eenmaal per week op maandag om middernacht.

>[!NOTE]
>
>De `crons` in de `.magento.app.yaml` Het bestand is gebaseerd op de tijdzone van de server, niet op de tijdzone die is opgegeven in de configuratiewaarden van de opslagruimte in de database.

Wanneer het bepalen van het plannen, overweeg de tijd het neemt om de taak te voltooien. Als u bijvoorbeeld om de drie uur een taak uitvoert en de taak 40 minuten duurt, kunt u overwegen de geplande tijd te wijzigen.

### Opdracht

De `cmd` geeft de opdracht of het aangepaste script op dat moet worden uitgevoerd. Het formaat van het bevelmanuscript kan het volgende omvatten:

```text
<path-to-php-binary> <project-dir>/<script-command>
```

Bijvoorbeeld:

```yaml
crons:
    spec: "00 */8 * * *"
    cmd: "/usr/bin/php /app/abc123edf890/bin/magento export:start catalog_category_product"
```

In dit voorbeeld: `<path-to-php-binary>` is `/usr/bin/php`. De installatiemap, die de project-id bevat, is `/app/abc123edf890/bin/magento`en de scripthandeling is `export:start catalog_category_product`.

### Aangepaste uitsnijdtaken toevoegen aan uw project

Op het Adobe Commerce-platform voor cloudinfrastructuur kunt u aanpassingen toevoegen aan de `crons` van de [`.magento.app.yaml`](../application/configure-app-yaml.md) bestand.

>[!NOTE]
>
>Voor Starter-omgevingen en Pro `integration` in omgevingen is het minimale interval eenmaal per vijf minuten. Voor Pro het Staging en van de Productie milieu&#39;s, is het minimuminterval eens per minuut. U kunt geen frequentere intervallen dan de standaardminimumintervallen vormen.

Voor Adobe Commerce Pro-projecten [automatisch aanmaken, functie](#set-up-cron-jobs) moet op uw project worden toegelaten alvorens u de banen van de douanescron aan het Opvoeren en van de Productie milieu&#39;s kunt toevoegen gebruikend `.magento.app.yaml` bestand. Als deze functie niet is ingeschakeld, [Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om automatische crons in te schakelen.

**Aangepaste uitsnijdtaken toevoegen**:

1. Bewerk in uw lokale ontwikkelomgeving de `.magento.app.yaml` bestand in de Adobe Commerce `/app` directory.

1. In de `crons` voegt u uw aanpassing toe in de volgende indeling:

   ```yaml
   crons:
       <cron_name_1>:
           spec: "<schedule_time>"
           cmd: "<schedule_command>"
       <cron_name_2>:
           spec: "<schedule_time>"
           cmd: "<schedule_command>"
   ```

   In het volgende voorbeeld wordt `productcatalog` de productcatalogus wordt elke acht uur, 20 minuten na het uur, geëxporteerd.

   ```yaml
   crons:
       magento:
           spec: '* * * * *'
           cmd: 'php bin/magento cron:run'
       productcatalog:
           spec: '20 */8 * * *'
           cmd: 'bin/magento export:start catalog_product_category'
   ```

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add .magento.app.yaml && git commit -m "cron config updates" && git push origin <branch-name>
   ```

### Snijtaken bijwerken

Als u een aangepaste taak wilt toevoegen, verwijderen of bijwerken, wijzigt u de configuratie in het dialoogvenster `crons` van de `.magento.app.yaml` bestand. Vervolgens test u de updates op de externe server `integration` milieu alvorens de veranderingen in het Staging en de milieu&#39;s van de Productie te duwen.

## Snijtaken uitschakelen

U kunt snijtaken handmatig uitschakelen voordat u onderhoudstaken uitvoert, zoals opnieuw indexeren of het cachegeheugen schoonmaken om prestatieproblemen te voorkomen. U kunt de `ece-tools` CLI, opdracht `cron:disable` om alle snijtaken uit te schakelen en actieve snijprocessen te stoppen.

**Snijtaken uitschakelen**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Gebruik SSH om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Hiermee schakelt u uitsnijdtaken uit en stopt u actieve uitsnijdprocessen.

   ```shell
   ./vendor/bin/ece-tools cron:disable
   ```

1. Nadat u alle vereiste onderhoudstaken hebt uitgevoerd, dient u de uitsnijdtaken opnieuw in te schakelen.

   ```shell
   ./vendor/bin/ece-tools cron:enable
   ```

## Problemen met uitsnijdtaken oplossen

Adobe heeft het Adobe Commerce-pakket voor cloudinfrastructuur bijgewerkt om de verwerking van cron op het Adobe Commerce-platform voor cloudinfrastructuur te optimaliseren en om problemen met betrekking tot cloudinfrastructuur op te lossen. Als u problemen ondervindt met de verwerking van het programma, controleert u of uw project de meest actuele versie van het dialoogvenster `ece-tools` pakket. Zie [ECE-gereedschappen bijwerken](../dev-tools/update-package.md).

U kunt de gegevens van de cron-verwerking bekijken in de logbestanden op toepassingsniveau voor elke omgeving. Zie [Toepassingslogboeken](../test/log-locations.md#application-logs).

Raadpleeg de volgende Adobe Commerce Support-artikelen voor hulp bij het oplossen van problemen met betrekking tot andere toepassingen:

- [Taken uitsnijden vergrendelen taken uit andere groepen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-tasks-lock-tasks-from-other-groups.html)

- [Vastgezette snijtaken handmatig opnieuw instellen in de cloud](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/reset-stuck-magento-cron-jobs-manually-on-cloud.html)
