---
title: Slimme wizards
description: Leer hoe u slimme wizards gebruikt om te beoordelen of uw Adobe Commerce on cloud Infrastructure-project de best practices voor implementatie volgt.
feature: Cloud, Build, Deploy, SCD
exl-id: eb79431c-8835-4ae4-b453-9c4932c5d5ac
source-git-commit: 225fba1acfd8b3ce4d7ce989c7851e7b0b218680
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Slimme wizards

De slimme wizards kunnen u helpen bepalen of uw configuratie van de Wolk beste praktijken volgt. De beschikbare tovenaars helpen bij de volgende configuraties:

- Ideale status voor minimale uitvaltijd van implementatie
- Configuratie voor taakverdeling voor database en Redis
- De statische Plaatsing van de Inhoud (SCD) voor op bestelling, bouwt stadium, of stelt stadium op

Elk van de slimme tovenaarsbevelen verstrekt een controlerespons en, indien van toepassing, een aanbeveling voor de juiste configuratie.

| Opdracht | Beschrijving |
| ------- | ------------|
| `wizard:ideal-state` | Controleer of de SCD zich op de _build_ de `SKIP_HTML_MINIFICATION` variable is `true`en de functie post_implementatiehaak geconfigureerd in de cloud-omgeving. Niet voor gebruik in de lokale ontwikkelomgeving. |
| `wizard:master-slave` | Controleer of de `REDIS_USE_SLAVE_CONNECTION` en de `MYSQL_USE_SLAVE_CONNECTION` variable is `true`. |
| `wizard:scd-on-demand` | Controleer of de `SCD_ON_DEMAND` globale omgevingsvariabele is `true`. |
| `wizard:scd-on-build` | Controleer of de `SCD_ON_DEMAND` globale omgevingsvariabele is `false` en de `SKIP_SCD` omgevingsvariabele is `false` voor de _build_ in het werkgebied. Hiermee wordt gecontroleerd of de `config.php` Het bestand bevat informatie voor winkels, winkelgroepen en websites. |
| `wizard:scd-on-deploy` | Controleer of de `SCD_ON_DEMAND` globale omgevingsvariabele is `false` en de `SKIP_SCD` omgevingsvariabele is `false` voor de _inzetten_ in het werkgebied. Hiermee wordt gecontroleerd of de `config.php` bestand doet dit _NOT_ bevat de lijst met winkels, winkelgroepen en websites met verwante informatie. |

Als voorbeeld, kunt u verifiëren dat uw configuratie behoorlijk SCD op bestelling eigenschap toelaat:

```bash
./vendor/bin/ece-tools wizard:scd-on-demand
```

Een geslaagde configuratie retourneert:

```terminal
SCD on-demand is enabled
```

Een mislukte configuratie retourneert:

```terminal
SCD on-demand is disabled
```

## Een ideale configuratie controleren

De _ideaal_ De configuratie voor uw Cloud-project helpt implementatiedowntime te minimaliseren door de cache op te warmen en statische inhoud te genereren wanneer de gebruiker daarom vraagt. Deze tovenaar loopt automatisch tijdens het plaatsingsproces. Als uw cloud hiervoor niet is geconfigureerd _ideale status_ Vervolgens ontvangt u een bericht dat lijkt op het volgende:

```terminal
- SCD on build is not configured
- Post-deploy hook is not configured
- Skip HTML minification is disabled

Ideal state is not configured
```

Gebaseerd op de output, moet u de volgende correcties in uw configuratie aanbrengen:

1. Schakel de minificatievariabele HTML overslaan in.

   > .magento.env.yaml

   ```yaml
   stage:
     global:
       SKIP_HTML_MINIFICATION: true
   ```

1. Vorm de post-opstellen haak.

   > .magento.app.yaml

   ```yaml
       post_deploy: |
           php ./vendor/bin/ece-tools post-deploy
   ```

1. Duw uw code verandert en stel de test opnieuw in werking. Wanneer uw configuratie _ideaal_, ontvangt u het volgende bericht.

   ```terminal
   Ideal state is configured
   ```
