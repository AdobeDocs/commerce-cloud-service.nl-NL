---
title: Automatisch schalen
description: Leer hoe Adobe Commerce op cloudinfrastructuur kan schalen om aan de behoeften aan bronnen te voldoen.
feature: Cloud, Auto Scaling
topic: Architecture
exl-id: 2ba49c55-d821-4934-965f-f35bd18ac95f
source-git-commit: c61d711b1041ecf76ec6468cd225a34fd77c24b1
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# Automatisch schalen

Automatisch schalen voegt automatisch bronnen toe aan of verwijdert bronnen uit de cloudinfrastructuur om optimale prestaties en redelijke kosten te behouden. Deze functie is momenteel alleen beschikbaar voor projecten die zijn geconfigureerd met een [Schaalbare architectuur](scaled-architecture.md).

## Webserverknooppunten

De [weblaag](scaled-architecture.md#web-tier) schalen om een verhoging van procesverzoeken en hogere verkeersvereisten aan te passen. Momenteel wordt de functie voor automatisch schalen alleen horizontaal geschaald door knooppunten van de webserver toe te voegen of te verwijderen.

Een auto-schrapende gebeurtenis komt voor wanneer het gebruik van cpu en het verkeer een vooraf bepaalde drempel bereiken:

- **Toegevoegde knooppunten**—CPU&#39;s/cores in alle actieve webknooppunten hebben een capaciteit van 75% gedurende 1 minuut en het verkeer neemt gedurende 5 opeenvolgende minuten met 20% toe.
- **Verwijderde knooppunten**—CPU&#39;s/cores voor alle actieve webknooppunten worden gedurende 20 minuten bij 60% geladen. Knooppunten worden verwijderd in de volgorde waarin ze zijn toegevoegd.

De minimum- en maximumdrempels worden bepaald en vastgesteld op basis van de contractueel vastgelegde middellimieten van elke handelaar; dit vermindert het risico van oneindige schaling.

## Drempelwaarden bewaken met New Relic

U kunt de [New Relic-service](../monitor/new-relic-service.md) om bepaalde drempels, zoals gastheeraantal en het gebruik van cpu te controleren. De volgende New Relic-query&#39;s gebruiken een variabele notatie voor `cluster-id` alleen voor doeleinden.

>[!TIP]
>
>Voor een verwijzing bij het bouwen van vragen, zie [NRQL-syntaxis, -clausules en -functies](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/nrql-syntax-clauses-functions/) in de _New Relic_ documentatie.
>Gebruik uw vragen om een [New Relic-dashboard](https://docs.newrelic.com/docs/query-your-data/explore-query-data/dashboards/introduction-dashboards/).

### Aantal gastheren

In het volgende voorbeeld van een New Relic-query wordt het aantal hosts in de omgeving getoond:

```sql
SELECT uniqueCount(SystemSample.entityId) AS 'Infrastructure hosts', uniqueCount(Transaction.host) AS 'APM hosts seen' FROM SystemSample, Transaction where (Transaction.appName = 'cluster-id_stg' AND Transaction.transactionType = 'Web') OR SystemSample.apmApplicationNames LIKE '%|cluster-id_stg|%' TIMESERIES SINCE 3 HOURS AGO
```

In de volgende schermafbeelding: **APM-hosts gezien** verwijst naar het aantal gastheren met transacties die tijdens de geselecteerde periode worden geregistreerd.

![Aantal New Relic-hosts](../../assets/new-relic/host-count.png)

### CPU-gebruik

In het volgende voorbeeld van een New Relic-query wordt het CPU-gebruik voor webknooppunten getoond:

```sql
SELECT average(cpuPercent) FROM SystemSample FACET hostname, apmApplicationNames WHERE instanceType LIKE 'c%' TIMESERIES SINCE 3 HOURS AGO
```

![CPU-gebruik voor New Relic-webknooppunten](../../assets/new-relic/web-node-cpu-usage.png)

## Automatisch schalen inschakelen

Automatisch schalen voor uw Adobe Commerce in- of uitschakelen voor een infrastructuurproject in de cloud [Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). Kies de volgende redenen in het ticket:

- **Contactreden**: Verzoek tot wijziging van infrastructuur
- **Reden voor contact met Adobe Commerce-infrastructuur**: Andere aanvraag tot wijziging van de infrastructuur

>[!IMPORTANT]
>
>Met de functie voor automatisch schalen worden onverwachte gebeurtenissen vastgelegd. Zelfs als automatische schaling is ingeschakeld, raadt de Adobe u aan door te gaan [Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) als u een aanstaande gebeurtenis verwacht.

### Laden testen

Adobe maakt automatische schaling op uw Cloud-project mogelijk _fasering_ cluster eerst. Nadat u het laden in uw omgeving hebt getest en voltooid, schakelt Adobe vervolgens automatische schaling in uw productiecluster in. Voor richtsnoeren voor het testen van de belasting, zie [Prestatietests](../launch/checklist.md#performance-testing).

### IP LIJST VAN GEWENSTE PERSONEN

Na het toelaten van auto het schrapen, komt het uitgaande verkeer van de Webknoop uit de IP adressen van de de dienstknopen voort. Als u een lijst van gewenste personen met een derdedienst gebruikt die niet met uw Adobe Commerce op het project van de wolkeninfrastructuur wordt gebundeld, dan verifieer de IP adressen in de lijst van gewenste personen van de derdendienst.

Bijvoorbeeld:

- Als de lijst van gewenste personen de IP adressen voor uw de dienstknopen (1, 2, en 3) bevat, dan is er geen vereiste actie.
- Als de lijst van gewenste personen de IP adressen voor uw de dienstknopen (1, 2, en 3) en Webknopen (4, 5, en 6)-in dit geval alle zes knopen-toen bevat is er geen vereiste actie.
- Als de lijst van gewenste personen de IP adressen bevat _alleen_ voor uw Webknopen (4, 5, en 6), dan moet u de lijst van gewenste personen bijwerken om de IP adressen voor de de dienstknopen te omvatten.
