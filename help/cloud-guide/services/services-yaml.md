---
title: Services configureren
description: Leer hoe u services die door Adobe Commerce worden gebruikt op cloudinfrastructuur configureert.
feature: Cloud, Configuration, Services
exl-id: 48091c10-c53f-4aad-afbe-b4516653bda1
source-git-commit: 4d790bff2ba5d02ef10de5c36a2f0d140e31a407
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Services configureren

De `services.yaml` In dit bestand worden de services gedefinieerd die door Adobe Commerce worden ondersteund en gebruikt op cloudinfrastructuur, zoals MySQL, Redis en Elasticsearch of OpenSearch. U hoeft zich niet in te schrijven op externe serviceproviders. Dit bestand staat in het dialoogvenster `.magento` directory van uw project.

Het plaatsingsmanuscript gebruikt de configuratiedossiers in `.magento` directory to provision the environment with the configured services. Een service wordt beschikbaar voor uw toepassing als deze is opgenomen in het dialoogvenster [`relationships`](../application/properties.md#relationships) eigendom van de `.magento.app.yaml` bestand. De `services.yaml` bevat het bestand _type_ en _schijf_ waarden. Het type van de dienst bepaalt de dienst _name_ en _versie_.

Het veranderen van een de dienstconfiguratie veroorzaakt een plaatsing aan voorziening het milieu met de bijgewerkte diensten, die de volgende milieu&#39;s beïnvloedt:

- Alle startomgevingen inclusief productie `master`
- Pro-integratieomgevingen

{{pro-update-service}}

## Standaard en ondersteunde services

De cloudinfrastructuur ondersteunt en implementeert de volgende services:

- [MySQL](mysql.md)
- [Redis](redis.md)
- [RabbitMQ](rabbitmq.md)
- [Elasticsearch](elasticsearch.md)
- [OpenSearch](opensearch.md)

U kunt standaardversies en schijfwaarden weergeven in de huidige versie, [default `services.yaml` file](https://github.com/magento/magento-cloud/blob/master/.magento/services.yaml). In het volgende voorbeeld wordt het `mysql`, `redis`, `opensearch` of `elasticsearch`, en `rabbitmq` in de `services.yaml` configuratiebestand:

```yaml
mysql:
    type: mysql:10.4
    disk: 5120

redis:
    type: redis:6.2

opensearch:
    type: opensearch:2  # minor version not required; uses latest
    disk: 1024

rabbitmq:
    type: rabbitmq:3.9
    disk: 1024
```

## Servicewaarden

U moet de dienst identiteitskaart en de configuratie van het de diensttype verstrekken `type: <name>:<version>`. Als de service blijvende opslag gebruikt, moet u een schijfwaarde opgeven.

Gebruik de volgende indeling:

```yaml
<service-id>:
    type: <name>:<version>
    disk: <value-MB>
```

### `service-id`

De `service-id` de waarde identificeert de dienst in het project. U kunt alleen alfanumerieke tekens in kleine letters gebruiken: `a` tot `z` en `0` tot `9`, zoals `redis`.

Dit _service-id_ waarde wordt gebruikt in het dialoogvenster [`relationships`](../application/properties.md#relationships) eigendom van de `.magento.app.yaml` configuratiebestand:

```yaml
relationships:
    redis: "<name>:redis"
```

U kunt meerdere instanties van elk servicetype een naam geven. U kunt bijvoorbeeld meerdere Redis-exemplaren gebruiken, een voor een sessie en een voor een cache.

```yaml
redis:
    type: redis:<version>

redis2:
    type: redis:<version>
```

De naam van een service wijzigen in het dialoogvenster `services.yaml` file **permanent verwijderen** het volgende:

- De bestaande service voordat u een service met de nieuwe naam maakt die u opgeeft.
- Alle bestaande gegevens voor de service worden verwijderd. Adobe raadt u ten zeerste aan [back-up maken van uw Starter-omgeving](../storage/snapshots.md) voordat u de naam van een bestaande service wijzigt.

### `type`

De `type` value geeft de servicenaam en -versie aan. Bijvoorbeeld:

```yaml
mysql:
    type: mysql:10.4
```

### `disk`

De `disk` value geeft de grootte aan van de permanente schijfopslag (in MB) die aan de service moet worden toegewezen. De diensten die blijvende opslag, zoals MySQL gebruiken, moeten een schijfwaarde verstrekken. Voor services die geheugen gebruiken in plaats van permanente opslag, zoals Redis, is geen schijfwaarde vereist.

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
```

Het huidige standaard opslagbedrag per project is 5 GB of 512 0MB. U kunt dit bedrag tussen uw toepassing en elk van zijn diensten verdelen.

## Servicerelaties

In Adobe Commerce voor cloud-infrastructuurprojecten, service [relaties](../application/properties.md#relationships) geconfigureerd in het dialoogvenster `.magento.app.yaml` bepalen welke services beschikbaar zijn voor uw toepassing.

U kunt de configuratiegegevens voor alle de dienstverhoudingen van terugwinnen [`$MAGENTO_CLOUD_RELATIONSHIPS`](../environment/variables-cloud.md) omgevingsvariabele. De configuratiegegevens omvatten de de dienstnaam, type, en versie samen met om het even welke vereiste verbindingsdetails zoals havenaantal en login geloofsbrieven.

**Relaties in lokale omgeving verifiëren**:

1. Geef in uw lokale omgeving de relaties voor de actieve omgeving weer.

   ```bash
   magento-cloud relationships
   ```

1. Bevestig de `service` en `type` uit het antwoord. De reactie verstrekt verbindingsinformatie, zoals het IP adres en havenaantal.

   >Afkorting van monsterrespons

   ```terminal
   redis:
       -
   ...
           type: 'redis:7.0'
           port: 6379
   elasticsearch:
       -
   ...
           type: 'opensearch:2'
           port: 9200
   database:
       -
   ...
           type: 'mysql:10.6'
           port: 3306
   ```

**Relaties in externe omgevingen verifiëren**:

1. Gebruik SSH om u aan te melden bij de externe omgeving.

1. Maak een lijst van de gegevens van de relatieconfiguratie voor alle diensten die in het milieu worden gevormd.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   of, gebruik het volgende `ece-tools` opdracht om relaties weer te geven:

   ```bash
   php ./vendor/bin/ece-tools env:config:show services
   ```

1. Bevestig de `service` en `type` uit het antwoord. De reactie verstrekt verbindingsinformatie, zoals het IP adres en havenaantal en om het even welke vereiste gebruikersbenaming en wachtwoordgeloofsbrieven.

## Serviceversies

Serviceversie en compatibiliteitsondersteuning voor Adobe Commerce op cloudinfrastructuur worden bepaald door versies die worden geïmplementeerd en getest op de cloudinfrastructuur en verschillen soms van versies die worden ondersteund door Adobe Commerce-implementaties op locatie. Zie [Systeemvereisten](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) in de _Installatie_ gids voor een lijst van derdesoftwaregebiedsdelen die de Adobe met specifieke versies van Adobe Commerce en van de Magento Open Source heeft getest.

### Software EOL-controles

Tijdens het implementatieproces `ece-tools` worden de geïnstalleerde de dienstversies vergeleken met de einddatum (EOL) voor elke dienst.

- Als een de dienstversie binnen drie maanden na de datum EOL is, toont een bericht in het opstellen logboek.
- Als de datum EOL in het verleden is, toont een waarschuwingsbericht.

Om de veiligheid van de opslag te handhaven, werk geïnstalleerde softwareversies bij alvorens zij EOL bereiken. U kunt de EOL-datums bekijken in het dialoogvenster [Gereedschappen `eol.yaml` file](https://github.com/magento/ece-tools/blob/develop/config/eol.yaml).

### Migreren naar OpenSearch

{{elasticsearch-support}}

Voor Adobe Commerce versie 2.4.4 en hoger raadpleegt u [OpenSearch-service instellen](opensearch.md).

## Serviceversie wijzigen

U kunt de versie van de geïnstalleerde service upgraden voor compatibiliteit met de Adobe Commerce-versie die in uw cloud-omgeving is geïmplementeerd.

U kunt de de dienstversie voor een geïnstalleerde dienst niet direct degraderen. U kunt echter wel een service met de vereiste versie maken. Zie [De dienstversie van de downgrade](#downgrade-version).

### Installatieversie van de service upgraden

U kunt de geïnstalleerde de dienstversie bevorderen door de de dienstconfiguratie in bij te werken `services.yaml` bestand.

1. Wijzig de [`type`](#type) waarde voor de dienst in `.magento/services.yaml` bestand:

   > Oorspronkelijke servicedefinitie

   ```yaml
   mysql:
       type: mysql:10.3
       disk: 2048
   ```

   > Bijgewerkte servicedefinitie

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   ```

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add .magento/services.yaml
   ```

   ```bash
   git commit -m "Upgrade MySQL from MariaDB 10.3 to 10.4."
   ```

   ```bash
   git push origin <branch-name>
   ```

### Downgrade

U kunt een geïnstalleerde service niet rechtstreeks downgraden. U hebt twee opties:

1. Wijzig de naam van een bestaande service met de nieuwe versie, waardoor de bestaande service en gegevens worden verwijderd en er een nieuwe wordt toegevoegd.

1. Creeer de dienst en sla de gegevens van de bestaande dienst op.

Wanneer u de de dienstversie verandert, moet u de de dienstconfiguratie in bijwerken `services.yaml` en de relaties in het dialoogvenster `.magento.app.yaml` bestand.

**Om een de dienstversie te degraderen door een bestaande dienst anders te noemen**:

1. Wijzig de naam van de bestaande service in het dialoogvenster `.magento/services.yaml` en wijzigt u de versie.

   >[!WARNING]
   >
   >Als u de naam van een bestaande service wijzigt, wordt deze vervangen en worden alle gegevens verwijderd. Als u de gegevens wilt behouden, maakt u een service in plaats van de naam van de bestaande service te wijzigen.

   Als u bijvoorbeeld de MariaDB-versie wilt verlagen voor de _mysql_ van versie 10.4 naar 10.3 _service-id_ en _type_ configuratie.

   > Origineel `services.yaml` definitie

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   ```

   > Nieuw `services.yaml` definitie

   ```yaml
   mysql2:
        type: mysql:10.3
        disk: 5120
   ```

1. De relaties in het dialoogvenster bijwerken `.magento.app.yaml` bestand.

   > Origineel `.magento.app.yaml` configuratie

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

   > Bijgewerkt `.magento.app.yaml` configuratie

   ```yaml
   relationships:
       database: "mysql2:mysql"
   ```

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

**Om de dienst te degraderen door de dienst te creëren**:

1. Voeg een de dienstdefinitie aan toe `services.yaml` bestand voor uw project met de gedowngradeerde versiespecificatie. Zie _mysql2_ in het volgende voorbeeld:

   > services.yaml

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   mysql2:
       type: mysql:10.3
       disk: 5120
   ```

1. Wijzig de relatieconfiguratie in het dialoogvenster `.magento.app.yaml` bestand om de nieuwe service te gebruiken.

   > Origineel `.magento.app.yaml` configuratie

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

   > Nieuw `.magento.app.yaml` configuratie

   ```yaml
   relationships:
       database: "mysql2:mysql"
   ```

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.
