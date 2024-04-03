---
title: MySQL-service instellen
description: Leer hoe u de MySQL-service beheert voor permanente gegevensopslag met Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Services, Storage
exl-id: 70820d00-8b82-4b60-87e4-ea98fd7ffcb2
source-git-commit: 9be8d1e062ab3dba86bc4d9c9ee8b8ece33d5b75
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# MySQL-service instellen

De `mysql` service biedt permanente gegevensopslag op basis van [MariaDB](https://mariadb.com/) versies 10.2 tot en met 10.4, ter ondersteuning van de [XtraDB](https://docs.percona.com/percona-xtradb-cluster/8.0/index.html) -opslagengine en opnieuw geïmplementeerde functies uit MySQL 5.6 en 5.7.

Het opnieuw indexeren op MariaDB 10.4 neemt meer tijd in vergelijking met andere versies MariaDB of MySQL. Zie [Indexers](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/configuration.html#indexers) in de _Aanbevolen werkwijzen voor prestaties_ hulplijn.

>[!WARNING]
>
>Wees voorzichtig wanneer u een upgrade uitvoert van MariaDB van versie 10.1 naar 10.2. MariaDB 10.1 is de laatste versie die ondersteuning biedt voor _XtraDB_ als de opslagengine. Het gebruik van MariaDB 10.2 _InnoDB_ voor de opslagengine. Nadat u van 10.1 aan 10.2 bevordert, kunt u niet de verandering terugdraaien. Adobe Commerce ondersteunt beide opslagengines. U moet echter wel de extensies en andere systemen controleren die door uw project worden gebruikt om te controleren of deze compatibel zijn met MariaDB 10.2. Zie [Niet-compatibele wijzigingen tussen 10.1 en 10.2](https://mariadb.com/kb/en/upgrading-from-mariadb-101-to-mariadb-102/#incompatible-changes-between-101-and-102).

{{service-instruction}}

**MySQL inschakelen**:

1. Voeg de vereiste naam, het type en de schijfwaarde (in MB) toe aan de `.magento/services.yaml` bestand.

   ```yaml
   mysql:
       type: mysql:<version>
       disk: 5120
   ```

   >[!TIP]
   >
   >MySQL-fouten, zoals `PDO Exception: MySQL server has gone away`kan optreden als er onvoldoende schijfruimte is. Controleer of u voldoende schijfruimte hebt toegewezen aan de service in het dialoogvenster [`.magento/services.yaml`](services-yaml.md#disk) bestand.

1. Configureer de relaties in de `.magento.app.yaml` bestand.

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable mysql service" && git push origin <branch-name>
   ```

1. [Verifieer de de dienstverhoudingen](services-yaml.md#service-relationships).

{{service-change-tip}}

## MySQL-database configureren

U hebt de volgende opties wanneer het vormen van het gegevensbestand MySQL:

- **`schemas`**—Een schema definieert een database. Het standaardschema is het `main` database.
- **`endpoints`**—Elk eindpunt vertegenwoordigt een referentie met specifieke voorrechten. Het standaardeindpunt is `mysql`, die `admin` toegang tot de `main` database.
- **`properties`**—De eigenschappen worden gebruikt om extra gegevensbestandconfiguraties te bepalen.

Het volgende is een basisvoorbeeldconfiguratie in `.magento/services.yaml` bestand:

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
    configuration:
        properties:
            optimizer_switch: "rowid_filter=off"
            optimizer_use_condition_selectivity: 1
```

De `properties` in het bovenstaande voorbeeld wijzigt u de standaardwaarde `optimizer` instellingen als [geadviseerd in de gids van Beste praktijken van Prestaties](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/configuration.html#indexers).

**MariaDB-configuratieopties**:

| Opties | Beschrijving | Standaardwaarde |
| -------------------- | --------------------------------------------------- | ------------------ |
| `default_charset` | De standaardtekenset. | utf8mb4 |
| `default_collation` | De standaardsortering. | utf8mb4_unicode_ci |
| `max_allowed_packet` | Maximale grootte voor pakketten, in MB. Bereik `1` tot `100`. | 16 |
| `optimizer_switch` | Stel waarden in voor de functie voor query-optimalisatie. Zie [MariaDB-documentatie](https://mariadb.com/kb/en/server-system-variables/#optimizer_switch). | |
| `optimizer_use_condition_selectivity` | Selecteer de statistieken die door optimizer worden gebruikt. Bereik `1` tot `5`. Zie [MariaDB-documentatie](https://mariadb.com/kb/en/server-system-variables/#optimizer_use_condition_selectivity). | 4 voor 10.4 en hoger |

### Meerdere databasegebruikers instellen

U kunt desgewenst meerdere gebruikers instellen met verschillende machtigingen voor toegang tot de `main` database.

Door gebrek, is er één genoemd eindpunt `mysql` die beheerderstoegang tot het gegevensbestand heeft. Als u meerdere databasegebruikers wilt instellen, moet u meerdere eindpunten definiëren in het dialoogvenster `services.yaml` de relaties in de `.magento.app.yaml` bestand. Voor Pro Staging- en Productieomgevingen [Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om de extra gebruiker aan te vragen.

Gebruik een geneste array om de eindpunten voor specifieke gebruikerstoegang te definiëren. Elk eindpunt kan toegang tot één of meerdere schema&#39;s (gegevensbestanden) en verschillende niveaus van toestemming op elk aanwijzen.

De geldige machtigingsniveaus zijn:

- `ro`: Alleen SELECT-query&#39;s zijn toegestaan.
- `rw`: U kunt query&#39;s SELECT en query&#39;s INSERT, UPDATE en DELETE gebruiken.
- `admin`: Alle vragen zijn toegestaan, met inbegrip van vragen DDL (CREATE LIJST, DROP LIJST, en meer).

Bijvoorbeeld:

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
    configuration:
        schemas:
            - main
        endpoints:
            admin:
                default_schema: main
                privileges:
                    main: admin
            reporter:
                privileges:
                    main: ro
            importer:
                privileges:
                    main: rw
        properties:
            optimizer_switch: "rowid_filter=off"
            optimizer_use_condition_selectivity: 1
```

In het voorgaande voorbeeld wordt `admin` eindpunt verleent admin-vlakke toegang tot `main` de `reporter` eindpunt verleent read-only toegang, en `importer` het eindpunt verleent read-write toegang, wat betekent:

- De `admin` de gebruiker heeft volledige controle over de database.
- De `reporter` gebruiker heeft alleen SELECT-rechten.
- De `importer` gebruiker heeft de rechten SELECT, INSERT, UPDATE en DELETE.

Voeg de in het bovenstaande voorbeeld gedefinieerde eindpunten toe aan de `relationships` eigendom van de `.magento.app.yaml` bestand. Bijvoorbeeld:

```yaml
relationships:
    database: "mysql:admin"
    databasereporter: "mysql:reporter"
    databaseimporter: "mysql:importer"
```

>[!NOTE]
>
>Als u één gebruiker MySQL vormt, kunt u niet gebruiken [`DEFINER`](https://dev.mysql.com/doc/refman/8.0/en/show-grants.html) toegangsbeheersmechanisme voor opgeslagen procedures en meningen.

## Verbinding maken met de database

Als u rechtstreeks toegang wilt krijgen tot de MariaDB-database, moet u een SSH gebruiken om u aan te melden bij de externe Cloud-omgeving en verbinding te maken met de database.

1. Gebruik SSH om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Haal de MySQL aanmeldingsgegevens op van het `database` en `type` eigenschappen in de [$MAGENTO_CLOUD_RELATIONSHIPS](../application/properties.md#relationships) variabele.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   of

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   In de reactie, vind de informatie MySQL. Bijvoorbeeld:

   ```json
   "database" : [
      {
         "password" : "",
         "rel" : "mysql",
         "hostname" : "nnnnnnnn.mysql.service._.magentosite.cloud",
         "service" : "mysql",
         "host" : "database.internal",
         "ip" : "###.###.###.###",
         "port" : 3306,
         "path" : "main",
         "cluster" : "projectid-integration-id",
         "query" : {
            "is_master" : true
         },
         "type" : "mysql:10.3",
         "username" : "user",
         "scheme" : "mysql"
      }
   ],
   ```

1. Maak verbinding met de database.

   - Gebruik voor Starter de volgende opdracht:

     ```bash
     mysql -h database.internal -u <username>
     ```

   - Voor Pro, gebruik het volgende bevel met hostname, havenaantal, gebruikersbenaming, en wachtwoord die van wordt teruggewonnen `$MAGENTO_CLOUD_RELATIONSHIPS` variabele.

     ```bash
     mysql -h <hostname> -P <number> -u <username> -p'<password>'
     ```

>[!TIP]
>
>U kunt de `magento-cloud db:sql` gebruiken om verbinding te maken met de externe database en SQL-opdrachten uit te voeren.

## Verbinding maken met secundaire database

>[!IMPORTANT]
>
>Deze functie is alleen beschikbaar voor Pro Production- en Staging-clusters.

Soms, moet u met het secundaire gegevensbestand verbinden om gegevensbestandprestaties te verbeteren of gegevensbestand het sluiten kwesties op te lossen. Als deze configuratie wordt vereist, gebruik `"port" : 3304` om de verbinding tot stand te brengen. Zie de [Beste praktijken om de MySQL slave verbinding te vormen](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration.html) in het _Aanbevolen werkwijzen voor implementatie_ hulplijn.

## Problemen oplossen

Raadpleeg de volgende Adobe Commerce Support-artikelen voor hulp bij het oplossen van MySQL-problemen:

- [Het controleren van langzame vragen en verwerkt MySQL](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/database/checking-slow-queries-and-processes-mysql.html)
- [Database-dump maken op Cloud](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/create-database-dump-on-cloud.html)
- [Problemen met het hulpprogramma voor gegevensmigratie oplossen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-migration-tool-troubleshooting.html)
- [Adobe Commerce-upgrade: compact naar dynamische tabellen 2.2.x, 2.3.x naar 2.4.x](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/commerce-235-upgrade-prerequisites-mariadb.html)
