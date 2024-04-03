---
title: Logboekhandlers
description: Leer hoe u loghandlers voor Adobe Commerce kunt configureren op cloudinfrastructuur.
feature: Cloud, Logs, Configuration
role: Developer
exl-id: d3be7b6d-5778-4c32-865b-31bdb2852a23
source-git-commit: f8e35ecff4bcafda874a87642348e2d2bff5247b
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Logboekhandlers

U kunt logboekmanagers vormen om berichten naar een verre registrerenserver te verzenden. Een logboekmanager duwt bouw en stelt logboeken aan andere systemen op, gelijkaardig aan de manier u logboeken aan Slack en e-mail duwt. U kunt een _syslog_ handler, die ideaal is voor logboekberichten met betrekking tot hardware, of een Grijslogbestand Extended Log Format (GELF)-handler, die ideaal is voor het registreren van berichten van softwaretoepassingen.

Het volgende voorbeeld vormt allebei van deze managers door de configuratie aan toe te voegen `.magento.env.yaml` bestand. Voor het minimale registratieniveau (`min_level`) waarden, zie [Logboekniveaus](#log-levels).

```yaml
log:
  syslog:
    ident: "<syslog-ident>"
    facility: 8 # https://php.net/manual/en/network.constants.php
    min_level: "info"
    logopts: <syslog-logopts>

  syslog_udp:
    host: "<syslog-host>"
    port: <syslog-port>
    facility: 8  # https://php.net/manual/en/network.constants.php
    ident: "<syslog-ident>"
    min_level: "info"

  gelf:
    min_level: "info"
    use_default_formatter: true
    additional: # Some additional information for each log message
      project: "<some-project-id>"
      app_id: "<some-app-id>"
    transport:
      http:
        host: "<http-host>"
        port: <http-port>
        path: "<http-path>"
        connection_timeout: 60
      tcp:
        host: "<tcp-host>"
        port: <tcp-port>
        connection_timeout: 60
      udp:
        host: "<udp-host>"
        port: <udp-port>
        chunk_size: 1024
```

## Logboekniveaus

De niveaus van het logboek bepalen het niveau van detail in berichtberichten. De volgende categorieën van het logboekniveau omvatten elk logboekniveau onder het. Bijvoorbeeld een `debug` omvat het kappen van elk niveau, terwijl een `alert` alleen waarschuwingen en noodsituaties worden weergegeven.

- **foutopsporing**—gedetailleerde foutopsporingsgegevens
- **info**—interessante gebeurtenissen, zoals een gebruikersaanmelding of SQL-logboek
- **bericht**—normale, maar significante gebeurtenissen
- **waarschuwing**—buitengewone gebeurtenissen die geen fouten zijn, zoals het gebruik van een vervangen API of slecht gebruik van een API
- **fout**—uitvoeringsfouten die geen onmiddellijke actie vereisen
- **kritisch**—kritieke omstandigheden, zoals een niet-beschikbare toepassingscomponent of een onverwachte uitzondering
- **alert**—onmiddellijke actie vereist—zoals een website is neer of het gegevensbestand niet beschikbaar-dat een alarm van SMS teweegbrengt
- **noodsituatie**—systeem onbruikbaar is
