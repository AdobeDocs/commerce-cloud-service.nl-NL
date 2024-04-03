---
title: Redis-service instellen
description: Leer hoe u Redis kunt instellen en optimaliseren als back-end cacheoplossing voor Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Cache, Services
exl-id: d6971875-d302-495a-ad10-a81c507c2bc9
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# Redis-service instellen

[Redis](https://redis.io) is een facultatieve, achterste geheim voorgeheugenoplossing die Zend Framework Zend_Cache_Backend_File vervangt, die Adobe Commerce door gebrek gebruikt.

Zie [Redis configureren](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/redis/config-redis.html) in de _Configuratiegids_.

{{service-instruction}}

**Redis inschakelen**:

1. Voeg de vereiste naam en type toe aan de `.magento/services.yaml` bestand.

   ```yaml
   myredis:
       type: redis:<version>
   ```

   Om uw eigen configuratie te verstrekken Redis, voeg toe `core_config` in uw `.magento/services.yaml` bestand:

   ```yaml
   cache:
       type: redis:<version>
   ```

1. Configureer de relaties in de `.magento.app.yaml` bestand.

   ```yaml
   runtime:
       extensions:
           - redis
   
   relationships:
       redis: "redis:redis"
   ```

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable redis service" && git push origin <branch-name>
   ```

1. [Verifieer de de dienstverhoudingen](services-yaml.md#service-relationships).

{{service-change-tip}}

## Het gebruik van Redis CLI

Ervan uitgaande dat uw relatie met Redis een naam heeft `redis`, kunt u het gebruiken van `redis-cli` gebruiken.

1. Gebruik SSH om verbinding te maken met de integratieomgeving met Redis geïnstalleerd en geconfigureerd.

1. Open een tunnel SSH aan een gastheer.

   ```bash
   redis-cli -h redis.internal
   ```

## De geïnstalleerde versie van Redis ophalen

Gebruik de volgende opdracht om de Redis-versie op een integratieomgeving te installeren:

```bash
redis-cli -h redis.internal info | grep version
```

Monsterrespons:

```terminal
redis_version:7.0.5
gcc_version:8.3.0
```

### Redis op Pro-ophaling en -productie

Als u de versie Redis wilt installeren in een omgeving voor Staging of Productie, gebruikt u de opdracht `redis-server` opdracht:

```bash
redis-server -v
```

```terminal
Redis server v=7.0.5 ...
```

Gebruik het volgende bevel om de configuratie te krijgen Redis die op een Pro het Staging of milieu van de Productie wordt geïnstalleerd:

```bash
echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
```

Monsterrespons:

```terminal
"redis" : [
    {
        "cluster" : "project-master-123abc4",
        "fragment" : null,
        "host" : "redis.internal",
        "host_mapped" : false,
        "hostname" : "oblahblahblahblahe.redis.service._.magentosite.cloud",
        "ip" : "169.254.10.10",
        "password" : null,
        "path" : null,
        "port" : 6379,
        "public" : false,
        "query" : {},
        "rel" : "redis",
        "scheme" : "redis",
        "service" : "redis",
        "type" : "redis:7.0.5",
        "username" : null
    }
]
```

## Problemen met Redis oplossen

Raadpleeg de volgende Adobe Commerce Support-artikelen voor hulp bij het oplossen van problemen met Redis:

- [Uitstel opnieuw verzenden Aanmelding beheerder of Afhandeling](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/redis-issue-delay-magento-admin-login-or-checkout.html)
- [Uitgebreide Redis cache-implementatie Adobe Commerce 2.3.5+](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/redis-service-configuration.html)
- [MDVA-30102: Redis cache wordt vol](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/patches/v1-0-6/mdva-30102-magento-patch-redis-cache-getting-full.html)
- [Beheerde waarschuwingen voor Adobe Commerce: waarschuwing voor opnieuw verzonden geheugen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-redis-memory-warning-alert.html)
- [Beheerde waarschuwingen voor Adobe Commerce: Redis-waarschuwing voor geheugenkritiek](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-redis-memory-critical-alert.html)
- [Redis troubleshooter](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/redis-troubleshooter.html)
