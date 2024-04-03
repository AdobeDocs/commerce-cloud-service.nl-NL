---
title: Schaalbare architectuur
description: Lees meer over de gesplitste architectuur en hoe deze geschaald kan worden uitgebreid om aan de vraag te voldoen.
feature: Cloud, Auto Scaling, Iaas, Logs
exl-id: c54d8772-b6cc-41cc-b1ab-bef7d6f13bf2
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---

# Schaalbare architectuur

De Cloud-infrastructuur wordt geschaald op basis van uw vereisten voor bronnen voor een hogere efficiëntie. De Adobe Commerce op cloudinfrastructuur bewaakt uw toepassingen en kan de capaciteit aanpassen om stabiele, voorspelbare prestaties te behouden. Het omzetten in deze architectuur helpt om problemen, zoals latentie of grote pieken in verkeer te verlichten.

>[!NOTE]
>
>De geschaalde architectuur is beschikbaar voor Adobe Commerce op cloudinfrastructuuraccounts met de Pro 48-cluster of hoger.

## Architectuur op gesplitste niveaus

De Pro-architectuur bestond uit drie knooppunten, die elk een volledige technologiestapel bevatten. Nu, is er een scalable infrastructuur die een gelaagde architectuur met een minimum van zes knopen verstrekt: drie knopen voor het kerngegevensbestand en de diensten en drie knopen voor de Webserver. Deze gesplitste architectuur biedt de mogelijkheid om lagen onafhankelijk te schalen om een optimale balans van prestaties te bereiken.

### Serviceniveau

Er zijn drie de dienstknopen voor gegevensopslag, geheim voorgeheugen, en de diensten: **OpenSearch** of **Elasticsearch**, **MariaDB**, **Redis** en meer. Wanneer de servicelaag de capaciteit nadert, kunt u alleen schalen door de grootte van de server te vergroten, bijvoorbeeld door de CPU-stroom en het geheugen op te voeren. De capaciteit is beperkt tot de grootte van de knoop die beschikbaar is. Omdat de gegevensbestandcluster voor hoge beschikbaarheid wordt ontworpen, kunt u niet horizontaal met de gebruikte technologieën schrapen.

![Schalen op serviceniveau](../../assets/scaling-service.png)

Overweeg een voorbeeld dat het de instantietype van de de dienstknoop is _m5.2xlarge_ met 32 GB RAM. Een service, zoals de database, gebruikt een aanzienlijke hoeveelheid geheugen (30 Gb). Schalen naar de volgende beschikbare instantiegrootte _m5.4xlarge_ biedt 64 GB RAM, waardoor het geheugen wordt verdubbeld en aan de groeiende behoeften van de database wordt voldaan.

U kunt de prestaties van de de dienstrij verder optimaliseren door verkeer te verpletteren dat op het knooptype wordt gebaseerd. Door gebrek, wordt de gegevensbestandknoop geïsoleerd van het Webverkeer. Als voorbeeld kunt u ervoor kiezen om het webverkeer op het databaseknooppunt te bedienen.

### Weblaag

Er zijn drie webknooppunten voor het verwerken van aanvragen en voor webverkeer: **php-fpm** en **NGINX**. Naast verticale schaling door meer stroom en geheugen te gebruiken, kan de weblaag ook horizontaal worden geschaald door webservers toe te voegen aan een bestaande cluster wanneer deze beperkt zijn op PHP-niveau. Zie [Automatisch schalen](autoscaling.md) voor meer informatie over hoe de webknooppunten automatisch worden geschaald.

![Schalen op webniveau](../../assets/scaling-web.png)

Dit vult de verticale schaling aan die door de de dienstrij wordt verstrekt. Aangezien de de dienstrij in grootte en macht schrapt om een groeiend gegevensbestand en de dienstgebruik aan te passen, de Webrijschaal in grootte, macht, en instanties om een toename van procesverzoeken en hogere verkeersvereisten aan te passen.

Bekijk een voorbeeld van het instantietype van het webknooppunt _C5.2Exlarge met acht CPU&#39;s en 16 Gb RAM_. Het aantal verzoeken aan de plaats nam sterk toe. U kunt een C5.2xlarge knoop toevoegen om de toename van php-fpm processen te behandelen of u kunt elk instantietype veranderen in _C5.4x uitgebreid met 16 CPU en 32 GB RAM_. Als u een knooppunt toevoegt, neemt het risico van onvoldoende piekcapaciteit af.

## Projectstructuur

Minimaal, hebben de Pro projecten met de Schaalde architectuur zes beschikbare knopen.

- 3 webknooppunten c5.2xlarge (8 CPU, 16 Gb RAM)

- 3 serviceknooppunten m5.2xlarge (8 CPU, 32 Gb RAM)

Elk project is echter uniek en vereist prestatiebewaking om het beheer van bronnen correct te analyseren. Elke account bevat de [New Relic-service](../monitor/new-relic-service.md), die automatisch verbinding maakt met de toepassingsgegevens en prestatie-analyses voor dynamische servercontrole. Specifiek, kunt u de dienst van New Relic gebruiken om het gebruik van cpu en van RAM te controleren om te bepalen welke knopen extra middelen vereisen. Wanneer een bron capaciteit bereikt of wanneer de prestaties achteruitgaan op basis van de analyse, kunt u een verzoek maken om uw infrastructuur te schalen om aan de vraag te voldoen.

### SSH-toegang

Bepaalde bestanden en logbestanden, zoals de `/app/<project-id>/var/log` niet worden gedeeld tussen knooppunten. Elk knooppunt heeft een unieke SSH-toegang. U kunt de `magento-cloud` CLI aan login aan de dienst of Webknopen, maar u kunt de knoopadressen in de lijst van de Toegang van SSH in uw vinden [!DNL Cloud Console].

```bash
ssh <node>.<project-ID>-<environment>-<user-ID>@ssh.<region>.magento.com
```

- `node` 1 door 3-Adressen om tot de de dienstknopen toegang te hebben

- `node` 4 door _n_—Adressen voor toegang tot de webknooppunten

>[!TIP]
>
>Nadat u zich hebt aangemeld, kunt u de server-id en de rol: de serviceknoppen gebruiken de _verenigd_ en webknooppunten gebruiken de _web_ rol.

Voorbeeld van een reactie als u zich aanmeldt bij een **serviceknooppunt** bevat de _verenigd_ rol:

```terminal
 __  __                   _          ___ _             _
|  \/  |__ _ __ _ ___ _ _| |_ ___   / __| |___ _  _ __| |
| |\/| / _` / _` / -_) ' \  _/ _ \ | (__| / _ \ || / _` |
|_|  |_\__,_\__, \___|_||_\__\___/  \___|_\___/\_,_\__,_|
            |___/

 Welcome to Magento Cloud.

 This is server unique-server-id, role project-id:unified.

project-id@server-id:~$
```

Voorbeeld van een reactie als u zich aanmeldt bij een **webknooppunt** bevat de _web_ rol:

```terminal
 __  __                   _          ___ _             _
|  \/  |__ _ __ _ ___ _ _| |_ ___   / __| |___ _  _ __| |
| |\/| / _` / _` / -_) ' \  _/ _ \ | (__| / _ \ || / _` |
|_|  |_\__,_\__, \___|_||_\__\___/  \___|_\___/\_,_\__,_|
            |___/

 Welcome to Magento Cloud.

 This is server unique-server-id, role project-id:web.

project-id@server-id:~$
```

### Loglocaties

De logboekplaatsen variëren lichtjes afhankelijk van de knoop. Een databaselogbestand, zoals de **MySQL foutenlogboek**, is beschikbaar op een serviceknooppunt (`/var/log/mysql/mysql-error.log`), maar niet beschikbaar op een webknooppunt.

Elke Pro-account bevat de [New Relic Logs-service](../monitor/new-relic-service.md), die automatisch verbinding maakt met loggegevens van de toepassing voor dynamisch logbeheer. Samengevoegde loggegevens van alle knooppunten worden weergegeven in de toepassing New Relic Logs, zodat u problemen met de prestaties van specifieke knooppunten op één dashboard kunt oplossen.
