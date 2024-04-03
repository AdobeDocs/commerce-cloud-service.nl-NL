---
title: New Relic-bewaking
description: Leer hoe u toegang krijgt tot uw New Relic-dashboard en hoe u gegevens van uw Adobe Commerce analyseert over het infrastructuurproject in de cloud.
feature: Cloud, Observability
topic: Performance
exl-id: 8d1e2ad6-14d0-4754-9703-960d93e135a9
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---

# New Relic-bewaking

New Relic sluit uw infrastructuur aan en bewaakt deze [!DNL Commerce] toepassing met PHP-agents. Nadat een Cloud-omgeving verbinding heeft gemaakt met New Relic, kunt u zich aanmelden bij uw New Relic-account om de gegevens te bekijken die door de agent zijn verzameld.

Op de _APM&#39;s en services_ pagina, selecteert u de **Samenvatting** om transactiegegevens over uw toepassing weer te geven. Met deze weergave kunt u mogelijke fouten opsporen en de algemene status van uw toepassing en services controleren.

![New Relic-overzichtspagina van Cloud-project](../../assets/new-relic/dashboard.png)

Vanuit deze weergave kunt u transacties volgen die trage reacties of knelpunten, de doorvoer van toepassingen, webfouten en nog veel meer veroorzaken.

Bijgehouden gegevens controleren:

- **Meest tijdrovend**—Bepaal tijdverbruik door verzoeken parallel te volgen. U hebt bijvoorbeeld de hoogste transactietijd in product- en categorieweergaven doorgebracht. Als een pagina van de klantenrekening plotseling hoog in tijdconsumptie rangschikt, zou uw toepassing door een vraag of vraag-slepende prestaties kunnen worden beïnvloed.

- **Hoogste doorvoer**—Identificeer de pagina&#39;s het meest gebaseerd op de grootte en de frequentie van overgebrachte bytes.

Alle verzamelde gegevensdetails de tijd die aan acties wordt doorgebracht die gegevens, vragen, of _Redis_ gegevens. Als query&#39;s problemen veroorzaken, geeft New Relic informatie om deze problemen te volgen en erop te reageren.

>[!TIP]
>
>Zie voor meer informatie over het gebruik van deze gegevens om problemen met de toepassingsprestaties op te lossen [Prestaties oplossen met New Relic](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-performance-using-new-relic-on-magento-commerce.html) in de _Adobe Commerce Help Center_.

## Prestaties bewaken met beheerde waarschuwingen

Adobe biedt de _Beheerde waarschuwingen voor Adobe Commerce_ waarschuwingsbeleid om prestatiemetriek te volgen. Het beleid omvat een inzameling van alarm dat drempels plaatst en waarschuwing en kritieke berichten teweegbrengt wanneer de infrastructuur of de toepassingskwesties plaatsprestaties beïnvloeden. Het beleid volgt de volgende metriek op de milieu&#39;s van de Productie:

| Metrisch | Gegevensverzameling | Beschikbaarheid |
|:-------------------|:----------------|:----------------|
| [!DNL Apdex] score | APM | Pro en Starter |
| CPU-gebruik | NRI | Pro |
| Schijfruimte | NRI | Pro |
| Foutfrequentie | APM | Pro en Starter |
| Geheugengebruik | NRI | Pro |
| MariaDB-query laden | NRI | Pro |
| Herdis-geheugen | NRI | Pro |

Wanneer de infrastructuur of de toepassingsvoorwaarden van de plaats een waakzame drempel teweegbrengen, verzendt New Relic waakzame berichten zodat u de kwestie kunt proactief behandelen. Zie [Beheerde waarschuwingen voor Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce.html) in de _Adobe Commerce Help Center_ voor details over waakzame drempels en het oplossen van problemenstappen om de kwesties op te lossen die de waakzaamheid teweegbrachten.

>[!TIP]
>
>Voor Pro Staging- en integratieomgevingen en Starter-omgevingen kunt u [Gezondheidsmeldingen](../integrations/health-notifications.md) om de schijfruimte te controleren.

>[!PREREQUISITES]
>
>- **New Relic-referenties**—Credentials voor aanmelding bij de New Relic-account voor uw Cloud-project
>- **Active New Relic-integratie**—Controleren of uw cloud-omgeving is verbonden met New Relic
>- **Workflowmelding**—minstens één configureren [werkstroom](#set-up-a-workflow-for-notifications) om de waarschuwingsberichten te ontvangen

**De beheerde waarschuwingen voor het Adobe Commerce-beleid controleren**:

1. Aanmelden bij uw [New Relic-account](https://login.newrelic.com/login).

1. Zoek de _Beheerde waarschuwingen voor Adobe Commerce_ beleid:

   - Klik in het navigatiemenu Verkenner op **[!UICONTROL Alerts & AI]**.

   - Onder _Detecteren_, klikt u op **[!UICONTROL Alert Conditions & Policies]**.

   - Controleer of uw account boven aan het dialoogvenster _Waarschuwingsvoorwaarden en -beleid_ weergeven.

   - In de _Beleid_ list, selecteer **Beheerde waarschuwingen voor Adobe Commerce** beleid.

     ![Gegenereerd waarschuwingsbeleid](../../assets/new-relic/managed-alerts-policy.png)

     >[!NOTE]
     >
     >Als de _Beheerde waarschuwingen voor Adobe Commerce_ beleid is niet beschikbaar, zie [Beheerde waarschuwingen voor Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce.html) in de _Adobe Commerce Help Center_.

1. Klik op de knop **[!UICONTROL Alert conditions]** om de in het beleid gedefinieerde waarschuwingsvoorwaarden te controleren.

## Waarschuwingsbeleid maken

Wijzig geen waarschuwingen die zijn opgenomen in het beleid Beheerde waarschuwingen voor Adobe Commerce. De Adobe werkt en verbetert de waakzame voorwaarden in dit beleid in tijd bij, dat om het even welke aanpassingen beschrijft u aan het beleid toevoegt.

In plaats van een bestaande waarschuwing te wijzigen, kunt u een waarschuwingsbeleid maken. Kopieer vervolgens de waarschuwingsvoorwaarden naar het nieuwe beleid. Zie [Beleid of voorwaarden bijwerken](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/alert-policies/update-or-disable-policies-conditions/) in de _New Relic_ documentatie.

>[!TIP]
>
>Zie [Inleiding tot signaleringen](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/learn-alerts/alerts-concepts-workflow/) in de _New Relic_ documentatie voor meer gedetailleerde informatie over Alarm, waakzaam beleid, en werkschema&#39;s.

## Een workflow voor meldingen instellen

U kunt nu een _werkstroom_, voorheen een meldingskanaal genoemd, om meldingen over de prestaties van uw site te ontvangen op basis van gefilterde gegevens, zoals een waarschuwingsbeleid. Meldingen over prestatieproblemen gaan naar alle workflows die aan een waarschuwingsbeleid zijn gekoppeld wanneer de voorwaarden van de toepassing of infrastructuur een waarschuwing activeren. U ontvangt ook meldingen wanneer een probleem wordt bevestigd en gesloten.

New Relic biedt sjablonen voor het configureren van verschillende typen workflowmeldingen, zoals e-mail, Slack, PagerDuty, webhooks en meer.

**Een workflow configureren**:

1. Aanmelden bij uw [New Relic-account](https://login.newrelic.com/login).

1. Maak een workflow.

   - Klik in het navigatiemenu Verkenner op **[!UICONTROL Alerts & AI]**.

   - In de linkernavigatie onder _Verrijken en waarschuwen_, klikt u op **[!UICONTROL Workflows]**.

   - Klikken **[!UICONTROL Add a workflow]** aan de rechterkant.

     ![New Relic voegt een workflow toe](../../assets/new-relic/add-a-workflow.png)

   - Op de _Uw workflow configureren_ voert u een naam in voor de workflow.

   - In de _Gegevens filteren_ sectie, selecteert u **[!UICONTROL Managed Alerts for Adobe Commerce]** van de **[!UICONTROL Policy]** vervolgkeuzelijst.

   - In de _Waarschuwen_ selecteert u een kanaal en volgt u de instructies.

   - Klikken **[!UICONTROL Test workflow]** om uw configuratie te verifiëren.

1. Klik op **[!UICONTROL Activate workflow]**.

Raadpleeg de documentatie bij New Relic over [Workflows](https://docs.newrelic.com/docs/alerts-applied-intelligence/applied-intelligence/incident-workflows/incident-workflows/).

>[!WARNING]
>
>De waarschuwingen in het beleid Beheerde waarschuwingen voor Adobe Commerce hebben standaardworkflows die zijn geconfigureerd om Adobe-teams die Adobe Commerce ondersteunen op klanten van cloudinfrastructuren op de hoogte te brengen. Wijzig niet de configuratie voor deze standaardkanalen, en verwijder geen waakzaam beleid dat aan hen wordt toegewezen.
