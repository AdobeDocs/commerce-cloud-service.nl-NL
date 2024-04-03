---
title: Herstellen van componentfout
description: Leer hoe u kunt herstellen als een component niet correct wordt geïmplementeerd in Adobe Commerce op de cloudinfrastructuur.
feature: Cloud, Deploy
exl-id: 4855be0c-6883-4ab1-a364-316d10e97250
source-git-commit: b44d97f82ef09288807c648010202422c9ac04eb
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Herstellen van componentfout

Dit onderwerp bespreekt hoe te terug te krijgen als een component er niet in slaagt behoorlijk op te stellen. De typische voorbeelden omvatten componenten die gebiedsdelen hebben die niet door uw verre milieu, zoals incompatibele PHP versies worden voldaan.

U kunt op de volgende manieren herstellen van een mislukte implementatie:

- [Een back-up herstellen](../storage/snapshots.md#restore-a-snapshot)
- Project en code van vorige wijzigingen opschonen en opnieuw implementeren

## Reinigen, verwijderen en opnieuw implementeren

Om van de vorige plaatsing schoon te maken, identificeer de component die werd toegevoegd of bijgewerkt en verwijder dan het. Meld u eerst aan bij de externe omgeving en wis handmatig de inhoud van de `var` directory. Verwijder vervolgens de component uit de `composer.json` en de omgeving opnieuw te implementeren.

**Als u de `var` mappen**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Gebruik SSH om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Wis de `var` mappen.

   ```shell
   rm -rf var/*
   ```

1. Afmelden.

**De component verwijderen**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Wis de cache.

   ```bash
   composer clear-cache
   ```

1. De component verwijderen uit de `composer.json` bestand.

   ```bash
   composer remove <component-name>:<version>
   ```

   Als het volgende bericht wordt weergegeven, hoeft u niets meer te doen:

   ```terminal
   Package "<name>:<version>" listed for update is not installed. Ignoring.
   ```

1. Wacht terwijl de gebiedsdelen worden bijgewerkt.

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "<message>"
   ```

   ```bash
   git push origin <environment-ID>
   ```

{{redeploy-warning}}

Zie meer over het herstellen van een omgeving zonder back-up in [Omgeving herstellen](../development/restore-environment.md).

{{stuck-deployment-tip}}
