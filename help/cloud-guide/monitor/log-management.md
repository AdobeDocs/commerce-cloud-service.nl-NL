---
title: New Relic-logbeheer
description: Meer informatie over het gebruik van het New Relic-logboek
feature: Cloud, Logs, Observability
exl-id: d8afb5c0-9727-4123-8944-81cd6ad7cbb7
source-git-commit: ebe1746ee9fd08480da5ad07d7f1f8299ad9af7e
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# New Relic-logbeheer

Alle cloud-infrastructuurprojecten omvatten [New Relic-logbeheer](https://docs.newrelic.com/docs/logs/get-started/get-started-log-management/). De dienst wordt pre-gevormd om alle logboekgegevens van uw het Opvoeren en milieu&#39;s van de Productie samen te voegen en het in een gecentraliseerd logboekbeheersdashboard te tonen.

De geaggregeerde gegevens bevatten informatie uit de volgende logboeken:

- Alles `ece-tools` en toepassingslogbestanden van de `~/var/log` directory
- Logboeken voor cloudservices van de `var/log/platform/<project-ID>` directory
- Fastly CDN and WAF

Wanneer uw project is verbonden met New Relic, kunt u de service New Relic Logs gebruiken om taken als:

- New Relic-query&#39;s gebruiken om geaggregeerde loggegevens te zoeken
- Loggegevens visualiseren via de toepassing New Relic Logs
- Aangepaste grafieken, dashboards en waarschuwingen maken
- Problemen met prestaties oplossen via één dashboard

## Loggegevens weergeven en analyseren

Gebruik de toepassing New Relic Logs om de geaggregeerde loggegevens te doorzoeken en toepassings-, infrastructuur-, CDN- en WAF-fouten op te lossen. U kunt grafieken, dashboards, en alarm tot stand brengen gebruikend logboekgegevens die bij de diensten van New Relic APM en van de Infrastructuur worden verzameld.

**De toepassing New Relic Logs gebruiken**:

1. Aanmelden bij uw [New Relic-account](https://login.newrelic.com/login).

1. Selecteren **Logboeken** in het navigatiemenu Verkenner.

1. Controleer of uw account boven aan het dialoogvenster _Alle logbestanden_ weergeven.

1. Selecteer een tijdbereik voor de Logs-query.

1. Infrastructuurloggegevens voor cloudservices controleren (logbestanden van `~/var/log/`), voert u de queryreeks in `has: "filePath"` in de _Zoeken naar logbestanden_ veld. Klik vervolgens op **[!UICONTROL Query logs]**.

   De namen van de logbestanden worden opgeslagen in het dialoogvenster `filePath` met volledige paden naar het logbestand.

   ![New Relic-servicelogbestandgegevens van Cloud-project](../../assets/new-relic/var-log-query.png)

1. Voer de queryreeks in om gegevens in het logboek snel te controleren `has: "client_ip"` in de _Zoeken naar logbestanden_ veld. Klik vervolgens op **[!UICONTROL Query logs]**.

1. Als u de resultaten van het snellog wilt filteren op landcode, klikt u op **[!UICONTROL Add column]** selecteert u vervolgens **[!UICONTROL geo_country_code]**.

   ![Cloud-project, New Relic CDN-logkenmerkfilter](../../assets/new-relic/fastly-countrycode-filter.png)

>[!TIP]
>
>U kunt de queryweergave opslaan vanuit de _Opgeslagen weergaven_ vervolgkeuzelijst. Klikken **[!UICONTROL Create new]**, geef een naam op, selecteer opties en klik op **[!UICONTROL Save view]**.
>
>Zie [Aan de slag met logbeheer](https://docs.newrelic.com/docs/logs/get-started/get-started-log-management/) en [Inleiding tot de New Relic-querytaal](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/introduction-nrql-new-relics-query-language/) op de _New Relic Docs_ site.
