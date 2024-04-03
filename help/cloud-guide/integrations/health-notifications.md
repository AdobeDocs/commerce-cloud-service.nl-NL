---
title: Gezondheidsmeldingen
description: Leer hoe u Slack-, e-mail- en PagerDuty-meldingen voor schijfruimtegebruik op uw Adobe Commerce configureert voor een cloudinfratuuropbouwproject.
feature: Cloud, Observability, Integration
exl-id: d3173098-78ed-42a8-aeb3-9ccbaccc4d32
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Gezondheidsmeldingen

Adobe Commerce on cloud Infrastructure bewaakt het gebruik van schijfruimte voor alle toepassingen en services in uw Starter-omgeving of uw Pro-integratieomgeving. Een databaseschijf die onvoldoende ruimte heeft, kan gegevensbeschadiging veroorzaken. De statuscontrole vindt elke 5 minuten plaats en kan u via e-mail of een andere externe service op de hoogte stellen. Er zijn drie waarschuwingen op een lage schijf voor gezondheidsmeldingen:

- **Waarschuwing**—beschikbare schijfruimte minder dan 20%
- **Kritiek**—beschikbare schijfruimte minder dan 10%
- **Alles-duidelijk**—beschikbare schijfruimte retourneert meer dan 20%, na een low-disk-gebeurtenis

>[!NOTE]
>
>In een Pro Production-omgeving kunt u de Beheerde waarschuwingen voor het Adobe Commerce-waarschuwingsbeleid voor New Relic gebruiken om schijfruimte te controleren. Zie [Prestaties bewaken met beheerde waarschuwingen](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts).

## E-mailmeldingen

Voor de integratie van e-mailberichten over de gezondheid is een adres van oorsprong en ten minste één adres van de ontvanger vereist. U kunt hetzelfde e-mailadres gebruiken voor het `from-address` en de `recipients` adres. In het volgende voorbeeld wordt een integratie van een e-mail met de status geregistreerd met twee ontvangers:

```bash
magento-cloud integration:add --type health.email --from-address you@example.com --recipients them@example.com --recipients others@example.com
```

## Slack-kanaalmeldingen

Slack is een externe service die interactieve apps, bots genaamd, gebruikt om berichten in een chatroom te posten. Voordat u gezondheidsmeldingen in de Slack kunt ontvangen, moet u een aangepaste [bot-gebruiker](https://api.slack.com/bot-users) voor uw groep Slacks. Nadat u de beide gebruikers voor uw kanaal, of kanalen vormt, sparen [beide, token](https://api.slack.com/docs/token-types#bot) verstrekt door Slack om uw integratie te registreren. In het volgende voorbeeld worden gezondheidsmeldingen geregistreerd in een Slack-kanaal:

```bash
magento-cloud integration:add --type health.slack --token SLACK_BOT_TOKEN --channel '#slack-channel-name'
```

## PagerDuty-meldingen

PagerDuty is een externe dienst die teamleden op vraag van belangrijke kwesties kan op de hoogte brengen. Voordat u meldingen over de gezondheid in PagerDuty kunt ontvangen, moet u een [PagerDuty-integratie](https://developer.pagerduty.com/v2/docs/integrating) die versie 2 van de API voor gebeurtenissen gebruikt. de integratietoets gebruiken, of _routeringssleutel_, om uw integratie te registreren. Het volgende voorbeeld registreert berichten voor PagerDuty gebruikend een verpletterende sleutel:

```bash
magento-cloud integration:add --type health.pagerduty --routing-key PAGERDUTY_ROUTING_KEY
```
