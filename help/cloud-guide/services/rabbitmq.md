---
title: RabbitMQ-service instellen
description: Leer hoe u de RabbitMQ-service in staat stelt om berichtwachtrijen voor Adobe Commerce te beheren op cloudinfrastructuur.
feature: Cloud, Services
exl-id: 85794b8f-2260-4a6e-b5a6-a1b4c356594e
source-git-commit: adcfbb7217c70122a4003a66d1bec1a623fbf11a
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# Instellen [!DNL RabbitMQ] service

De [Het Kader van de Rij van het bericht (MQF)](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/message-queue-framework.html) is een systeem in Adobe Commerce dat een [module](https://glossary.magento.com/module) om berichten aan rijen te publiceren. Het bepaalt ook de consumenten die de berichten asynchroon ontvangen.

Het MQF-gebruik [RabbitMQ](https://www.rabbitmq.com/) als overseinenmakelaar, die een scalable platform voor het verzenden van en het ontvangen van berichten verstrekt. Het omvat ook een mechanisme voor het opslaan van niet-geleverde berichten. [!DNL RabbitMQ] is gebaseerd op de Geavanceerde specificatie 0.9.1 van het Protocol van de Een rij vormen van het Bericht (AMQP).

>[!WARNING]
>
>Als u liever een bestaande AMQP-service gebruikt, zoals [!DNL RabbitMQ]in plaats van op Adobe Commerce te vertrouwen op cloudinfrastructuur om deze voor u te maken, kunt u de [`QUEUE_CONFIGURATION`](../environment/variables-deploy.md#queue_configuration) omgevingsvariabele om deze aan te sluiten op uw site.

{{service-instruction}}

**RabbitMQ inschakelen**:

1. Voeg de vereiste naam, het type en de schijfwaarde (in MB) toe aan de `.magento/services.yaml` samen met de geïnstalleerde versie van RabbitMQ.

   ```yaml
   rabbitmq:
       type: rabbitmq:<version>
       disk: 1024
   ```

1. Configureer de relaties in de `.magento.app.yaml` bestand.

   ```yaml
   relationships:
       rabbitmq: "rabbitmq:rabbitmq"
   ```

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add .magento/services.yaml .magento.app.yaml
   ```

   ```bash
   git commit -m "Enable RabbitMQ service"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. [Verifieer de de dienstverhoudingen](services-yaml.md#service-relationships).

{{service-change-tip}}

## Verbinding maken met RabbitMQ voor foutopsporing

Voor het zuiveren doeleinden, is het nuttig om met een de dienstinstantie op één van de volgende manieren direct te verbinden:

- Verbinding maken met uw lokale ontwikkelomgeving
- Verbinding maken vanuit de toepassing
- Verbinding maken met uw PHP-toepassing

### Verbinding maken met uw lokale ontwikkelomgeving

1. Aanmelden bij de `magento-cloud` CLI en project:

   ```bash
   magento-cloud login
   ```

1. Ontdek de omgeving met RabbitMQ geïnstalleerd en geconfigureerd.

   ```bash
   magento-cloud environment:checkout <environment-id>
   ```

1. SSH gebruiken om verbinding te maken met de cloud-omgeving:

   ```bash
   magento-cloud ssh
   ```

1. Haal de gegevens van de RabbitMQ-verbinding en aanmeldingsgegevens op via [$MAGENTO_CLOUD_RELATIONSHIPS](../application/properties.md#relationships) variabele:

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   of

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   In het antwoord vindt u bijvoorbeeld de RabbitMQ-informatie:

   ```json
   {
      "rabbitmq" : [
         {
            "password" : "guest",
            "ip" : "246.0.129.2",
            "scheme" : "amqp",
            "port" : 5672,
            "host" : "rabbitmq.internal",
            "username" : "guest"
         }
      ]
   }
   ```

1. Laat lokale haven toe door:sturen aan RabbitMQ (als uw project op een verschillend gebied zoals V.S.-3, EU-5, of AP-3 gebied wordt gevestigd, substitueer ``us-3``/``eu-5``/``ap-3`` for ``us``)

   ```bash
   ssh -L <port-number>:rabbitmq.internal:<port-number> <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

   Een voorbeeld voor toegang tot de RabbitMQ Management Web Interface op `http://localhost:15672` is:

   ```bash
   ssh -L 15672:rabbitmq.internal:15672 <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

1. Terwijl de sessie geopend is, kunt u een RabbitMQ-client naar keuze starten vanaf uw lokale werkstation, geconfigureerd om verbinding te maken met de `localhost:<portnumber>` het gebruiken van het havenaantal, gebruikersbenaming, en wachtwoordinformatie van de MAGENTO_CLOUD_RELATIONSHIPS variabele.

### Verbinding maken vanuit de toepassing

Als u verbinding wilt maken met RabbitMQ die wordt uitgevoerd in een toepassing, installeert u een client, zoals [amqp-utils](https://github.com/dougbarth/amqp-utils), als projectafhankelijkheid in uw `.magento.app.yaml` bestand.

Bijvoorbeeld:

```yaml
dependencies:
    ruby:
        amqp-utils: "0.5.1"
```

Wanneer u zich aanmeldt bij uw PHP-container, voert u een `amqp-` beschikbaar om uw rijen te beheren.

### Verbinding maken met uw PHP-toepassing

Als u verbinding wilt maken met RabbitMQ via uw PHP-toepassing, voegt u een PHP toe [bibliotheek](https://glossary.magento.com/library) naar de bronstructuur.
