---
source-git-commit: b08443d937dfc18120daa0d6a1277b9c7bca67aa
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---
# Cloud-fragmenten

## Waarschuwing Elasticsearch {#elasticsearch-support}

>[!WARNING]
>
>Elasticsearch 7.11 en hoger wordt niet ondersteund voor Adobe Commerce op cloudinfrastructuur. Adobe Commerce-versies 2.3.7-p3, 2.4.3-p2 en 2.4.4 en hoger ondersteunen de OpenSearch-service. De installaties ter plaatse blijven Elasticsearch steunen.

## Verbeterde integratie {#enhanced-integration-envs}

>[!NOTE]
>
>De projecten die vóór 5 juni 2020 werden verstrekt hadden veelvoudige, kleinere milieu&#39;s van de Integratie. Als u een grotere milieu van de Integratie voor het testen en de ontwikkeling nodig hebt, verzoek om een verbetering aan Verbeterde milieu&#39;s van de Integratie. Zie de [Aanvraag voor integratieomgeving](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/announcements/commerce-announcements/integration-environment-enhancement-request-pro-and-starter.html) artikel in het _Adobe Commerce Help Center_ voor meer informatie.

## Samenvoegopties {#merge-options}

Standaard overschrijft het implementatieproces alle instellingen in de `env.php` bestand, maar u kunt een of meer waarden voor een serviceconfiguratie samenvoegen zonder alle waarden te overschrijven.

Stel de `_merge` een van de volgende opties:

- `true`—**Samenvoegen** de gevormde de de dienstwaarden met de milieu veranderlijke waarden.
- `false`—**Overschrijven** de gevormde de de dienstwaarden met de milieu veranderlijke waarden.

## Persoonlijke opslagplaats {#private-repository}

>[!NOTE]
>
>Adobe raadt u ten zeerste aan een privéopslagplaats voor uw Adobe Commerce te gebruiken voor een cloudinfrastructuurproject om eigendomsgebonden informatie of ontwikkelingswerk, zoals extensies en kwetsbare configuraties, te beschermen.

## Pro-waarschuwing voor zelfbediening {#pro-self-service-warning}

>[!WARNING]
>
>Sommige **Pro-projecten** vereisen een steunkaartje om de routeconfiguratie in bij te werken `routes.yaml` bestand en de uitsnijdconfiguratie in het dialoogvenster `.magento.app.yaml` bestand. De Adobe adviseert het bijwerken van en het testen van de configuratiedossiers van YAML in een milieu van de Integratie, dan het opstellen van veranderingen in het het Opvoeren milieu. Als uw veranderingen niet op het Opvoeren plaatsen nadat u zich herstelt en er geen verwante foutenmeldingen in het logboek zijn, dan u **MOET** [Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) dat de poging tot configuratieveranderingen beschrijft. Neem de bijgewerkte YAML-configuratiebestanden op in het ticket.

## Pro-services-ondersteuning {#pro-update-service}

>[!TIP]
>Voor Pro-projecten moet u [een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) installeren of bijwerken [diensten](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/services-yaml.html) in `Staging` en `Production` alleen omgevingen.
>
>Geef aan welke servicewijzigingen nodig zijn en neem uw bijgewerkte `.magento.app.yaml` en `services.yaml` en geef de PHP-versie op in het ticket. Voor zelfbedieningswijzigingen in PHP-versie, extensies of omgevingen raadpleegt u [PHP-instellingen](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/app/php-settings.html) in _Toepassingsconfiguratie_.
>
>Voor wijzigingen in een _leven_ Productieomgeving (**Alleen Pro**), moet u een minimale opzegtermijn van 48 uur opgeven om het infrastructuurteam van de cloud voldoende tijd te geven om bronnen te zoeken en een beveiligde upgrade uit te voeren.

## Pro-back-ups {#pro-backups}

>[!TIP]
>
>In Pro Staging- en Productieomgevingen moet u [een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om een specifieke steun terug te winnen noterend de datum, de tijd, en de tijdzone in het kaartje.
>
>Adobe doet **niet** herstel omgevingen vanuit een automatische back-up. Zie [Een DB-momentopname herstellen uit Staging of Productie](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/restore-a-db-snapshot-from-staging-or-production.html) voor hulp die een methode kiest om een Opname van het Staging of van de Productie te herstellen.

## Waarschuwing bij opnieuw implementeren {#redeploy-warning}

>[!WARNING]
>
>Het plaatsingsproces begint wanneer u een fusie, duw, of synchronisatie van uw milieu uitvoert, of wanneer u een handherplaatsing teweegbrengt, waarin [!DNL Commerce] de toepassing bevindt zich in de onderhoudsmodus. Voor een productieomgeving raadt de Adobe aan deze werkzaamheden tijdens de werkuren buiten de piekuren af te ronden om onderbreking van de service te voorkomen.

## Plaatsaanduiding voor route {#route-placeholder}

>[!NOTE]
>
>De volgende voorbeelden van de routeconfiguratie gebruiken routesjablonen met placeholders. De `{default}` placeholder vertegenwoordigt het standaarddomein dat voor uw plaats wordt gevormd. Als uw project meerdere domeinen heeft, gebruikt u de `{all}` placeholder om het verpletteren voor het standaarddomein en alle aliassen te vormen. Zie [Verbindingen vormen](/help/cloud-guide/routes/routes-yaml.md).

## SCD-timing {#scd-timing-warning}

>[!WARNING]
>
>Als er problemen optreden met statische inhoudsbestanden in uw toepassing na de implementatie, zoals ontbrekende aangepaste themabestanden, verhoogt u de maximale verwachte uitvoeringstijd tot 900 seconden of langer.

## Implementatie op basis van scenario&#39;s {#scenarios}

>[!NOTE]
>
>Met [!DNL ECE-Tools] 2002.1.0 en hoger kunt u de op scenario&#39;s gebaseerde implementatiefunctie gebruiken om de ontwikkelings-, implementatie- en postimplementatieprocessen voor uw Adobe Commerce aan te passen in het infrastructuurproject in de cloud. Zie [Implementatie op basis van scenario&#39;s](/help/cloud-guide/deploy/scenario-based.md).

## Serviceinstructie {#service-instruction}

Gebruik de volgende instructies voor de dienstopstelling op de milieu&#39;s van de Integratie Pro en van de Starter milieu&#39;s, met inbegrip van `master` vertakking.

>[!NOTE]
>
>[Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om de de dienstconfiguratie op ProProductie en het Opvoeren milieu&#39;s te veranderen.

## Servicewijziging {#service-change-tip}

>[!TIP]
>
>Nadat u de service hebt ingesteld, kunt u de softwareversie van een geïnstalleerde service wijzigen door het `services.yaml` en `.magento.app.yaml` configuratiebestanden. Zie [Serviceversie wijzigen](/help/cloud-guide/services/services-yaml.md#change-service-version) richtsnoeren voor de verbetering of inkrimping van een dienst.

## Tip voor implementatie stoppen {#stuck-deployment-tip}

>[!TIP]
>
>Voor hulp bij vastgelopen implementaties kunt u de [Adobe Commerce-probleemoplossing voor implementatie](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-deployment-troubleshooter.html) in de _Hulp-centrum voor handel_.

## Bijwerken naar ECE-gereedschappen {#ece-tools-package}

>[!NOTE]
>
>Als u een versie van Adobe Commerce gebruikt op een cloudinfrastructuur die de `ece-tools` pakket, dan moet u een [eenmalige upgrade](/help/cloud-guide/dev-tools/install-package.md) naar uw cloud-project om verouderde pakketten te verwijderen. Als u momenteel `ece-tools` en u moet het pakket bijwerken, zie [Het pakket ECE-gereedschappen bijwerken](/help/cloud-guide/dev-tools/update-package.md).

## Upgradetip {#upgrade-tip}

>[!TIP]
>
>Voordat u met een upgrade of een patchproces begint, maakt u een actieve vertakking vanuit de integratieomgeving en checkt u de nieuwe vertakking uit naar uw lokale werkstation. Als u een vertakking aan de upgrade of het patchproces toewijst, voorkomt u dat uw werk wordt gehinderd.

<!-- Fastly-related snippets begin -->

## Aanmelden bij beheerder {#admin-login-step}

1. [Aanmelden](/help/get-started/onboarding.md#access-your-admin-panel) aan de beheerder.

## Aangepaste implementatie van VCL-fragmenten automatiseren {#automate-vcl-snippet-deployment}

>[!NOTE]
>
>In plaats van handmatig aangepaste VCL-fragmenten te uploaden, kunt u fragmenten toevoegen aan de `$MAGENTO_CLOUD_APP_DIR/var/vcl_snippets_custom` in uw omgeving. Fragmenten in deze map worden automatisch geüpload wanneer u op _VCL snel uploaden naar_ in de Commerce Admin. Zie [Geautomatiseerde implementatie van aangepaste VCL-fragmenten](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/CUSTOM-VCL-SNIPPETS.md#automated-custom-vcl-snippets-deployment) in de Fastly CDN module voor Magento 2 documentatie.

<!-- Fastly-related snippets end -->
