---
title: Implementaties bijhouden
description: Leer hoe u New Relic configureert om implementaties in uw Adobe Commerce bij te houden voor het infrastructuurproject in de cloud en wijzigingen in prestaties te analyseren.
feature: Cloud, Deploy, Observability
topic: Performance
last-substantial-update: 2023-10-12T00:00:00Z
exl-id: 3d477a4b-ae5a-4c82-b71b-33ff24827b93
source-git-commit: cd9b541bd5b2fa342b76c992ab85a5115368313b
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Implementaties bijhouden

U kunt de New Relic inschakelen _Wijzigingen bijhouden_ om implementatiegebeurtenissen op uw Handel in het project van de wolkeninfrastructuur te controleren.

De de gegevensinzameling van Plaatsingen helpt de invloed van plaatsingsveranderingen in algemene prestaties, zoals cpu, geheugen, reactietijd, en meer analyseren. Zie [Wijzigingen bijhouden met NerdGraph](https://docs.newrelic.com/docs/change-tracking/change-tracking-graphql/) in de _New Relic-documentatie_.

>[!PREREQUISITES]
>
>- `NR_API_URL`: New Relic API-eindpunt, in dit geval NerdGraph API-URL `https://api.newrelic.com/graphql`
>- `NR_API_KEY`: Een gebruikerssleutel maken, zie [New Relic API-toetsen](https://docs.newrelic.com/docs/apis/intro-apis/new-relic-api-keys) in de _New Relic_ documentatie.
>- `NR_APP_GUID`: Een entiteit die gegevens aan New Relic rapporteert heeft een unieke identiteitskaart (GUID). Als voorbeeld, om op een milieu van het Staging toe te laten, pas de het Staging milieu aan `NR_APP_GUID` wolkenvariabele met _staging-entiteit GUID_ uit New Relic. Zie de [Meer informatie over New Relic-entiteiten](https://docs.newrelic.com/docs/new-relic-solutions/new-relic-one/core-concepts/what-entity-new-relic/) en [NerdGraph-zelfstudie: entiteitsgegevens weergeven](https://docs.newrelic.com/docs/apis/nerdgraph/examples/nerdgraph-entities-api-tutorial/) in de _New Relic_ documentatie.

## Trackimplementaties inschakelen

Volg uw Commerce-projectimplementatiegebeurtenissen in New Relic door een _script_ integratie.

**Om spoorplaatsingen toe te laten**:

1. Wijzig op uw lokale werkstation de projectmap.
1. Een `action-integration.js` bestand. Kopieer de volgende code en plak deze in de `action-integration.js` bestand en opslaan:

   ```javascript
   function trackDeployments() {
     const envName = activity.payload.environment.name;
     let variables;
     activity.payload.deployment.variables.forEach(function(variable) {
       if (variable.name === "env:NR_CONFIG") {
         variables = variable.value;
       }
     });
     const config = JSON.parse(variables.replace(/'/g, '"'));
     const commitSha = activity.payload.commits ? activity.payload.commits[0].sha : activity.payload.environment.head_commit;
     const deploymentType = activity.type;
   
     if (!(envName in config)) {
       throw new Error('There is no configuration for ' + envName);
     }
   
     const configEnv = config[envName];
   
     if (!configEnv.NR_APP_GUID || !configEnv.NR_API_KEY || !configEnv.NR_API_URL) {
       throw new Error('You must define the next configuation in the env variable NR_CONFIG: NR_APP_GUID, NR_API_KEY and NR_API_URL');
     }
   
     const query = `mutation {
       changeTrackingCreateDeployment(
       deployment: {
           version: "${commitSha}",
           entityGuid: "${configEnv.NR_APP_GUID}",
           commit: "${commitSha}",
           changelog: "${deploymentType}"
       }
       ) {
         deploymentId
         entityGuid
       }
     }`;
   
     var resp = fetch(configEnv.NR_API_URL, {
       method: 'POST',
       headers: {
           'Content-Type': 'application/json',
           'API-Key': configEnv.NR_API_KEY
       },
       body: JSON.stringify({
           query
       })
     });
   
     if (!resp.ok) {
       console.log('Sending new relic change tracking failed: ' + resp.text());
     } else {
       console.log(resp.text());
     }
   }
   
   trackDeployments();
   ```

1. Een _script_ integratie met behulp van `magento-cloud` CLI-opdracht en verwijzing naar de `action-integration.js` bestand.

   ```bash
   magento-cloud integration:add --type script --events='environment.restore, environment.push, environment.branch, environment.activate, environment.synchronize, environment.initialize, environment.merge, environment.redeploy, environment.variable.create, environment.variable.delete, environment.variable.update' --file ./action-integration.js --project=<YOUR_PROJECT_ID> --environments=<YOUR_ENVIRONMENT_ID>
   ```

   Monsterrespons:

   ```terminal
   Created integration 767u4hathojjw (type: script)
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | Property              | Value                                                                                                                                   |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | id                    | 767u4hathojjw                                                                                                                           |
   | type                  | script                                                                                                                                  |
   | role                  |                                                                                                                                         |
   | events                | - environment.restore                                                                                                                   |
   |                       | - environment.push                                                                                                                      |
   |                       | - environment.branch                                                                                                                    |
   |                       | - environment.activate                                                                                                                  |
   |                       | - environment.synchronize                                                                                                               |
   |                       | - environment.initialize                                                                                                                |
   |                       | - environment.merge                                                                                                                     |
   |                       | - environment.redeploy                                                                                                                  |
   |                       | - environment.variable.create                                                                                                           |
   |                       | - environment.variable.delete                                                                                                           |
   |                       | - environment.variable.update                                                                                                           |
   | environments          | - staging                                                                                                                               |
   |                       | - production                                                                                                                            |
   | excluded_environments | {  }                                                                                                                                    |
   | states                | - complete                                                                                                                              |
   | result                | *                                                                                                                                       |
   | script                | function variables() {                                                                                                                  |
   |                       |     var vars = {};                                                                                                                      |
   |                       |     activity.payload.deployment.variables.forEach(function(variable) {                                                                  |
   |                       |         vars[variable.name] = variable.value;                                                                                           |
   |                       |     });                                                                                                                                 |
   |                       |     return vars;                                                                                                                        |
   |                       | }                                                                                                                                       |
   |                       |                                                                                                                                         |
   |                       | function trackDeployments() {                                                                                                           |
   |                       |     const envName = activity.payload.environment.name;                                                                                  |
   |                       |                                                                                                                                         |
   |                       |     const config = JSON.parse(variables()['env:NR_CONFIG'].replace(/'/g, '"'));                                                         |
   |                       |     const commitSha = activity.payload.commits ? activity.payload.commits[0].sha : activity.payload.environment.head_commit;            |
   |                       |     const deploymentType = activity.type;                                                                                               |
   |                       |                                                                                                                                         |
   |                       |     if (!(envName in config)) {                                                                                                         |
   |                       |         throw new Error('There is no configuration for ' + envName);                                                                    |
   |                       |     }                                                                                                                                   |
   |                       |                                                                                                                                         |
   |                       |     const configEnv = config[envName];                                                                                                  |
   |                       |                                                                                                                                         |
   |                       |     if (!configEnv.NR_APP_GUID || !configEnv.NR_API_KEY || !configEnv.NR_API_URL) {                                                     |
   |                       |         throw new Error('You must define the next configuation in the env variable NR_CONFIG: NR_APP_GUID, NR_API_KEY and NR_API_URL'); |
   |                       |     }                                                                                                                                   |
   |                       |                                                                                                                                         |
   |                       |     const query = `mutation {                                                                                                           |
   |                       |         changeTrackingCreateDeployment(                                                                                                 |
   |                       |           deployment: {                                                                                                                 |
   |                       |             version: "${commitSha}",                                                                                                    |
   |                       |             entityGuid: "${configEnv.NR_APP_GUID}",                                                                                     |
   |                       |             commit: "${commitSha}",                                                                                                     |
   |                       |             changelog: "${deploymentType}"                                                                                              |
   |                       |           }                                                                                                                             |
   |                       |         ) {                                                                                                                             |
   |                       |           deploymentId                                                                                                                  |
   |                       |           entityGuid                                                                                                                    |
   |                       |         }                                                                                                                               |
   |                       |     }`;                                                                                                                                 |
   |                       |                                                                                                                                         |
   |                       |     var resp = fetch(configEnv.NR_API_URL, {                                                                                            |
   |                       |         method: 'POST',                                                                                                                 |
   |                       |         headers: {                                                                                                                      |
   |                       |             'Content-Type': 'application/json',                                                                                         |
   |                       |             'API-Key': configEnv.NR_API_KEY                                                                                             |
   |                       |         },                                                                                                                              |
   |                       |         body: JSON.stringify({                                                                                                          |
   |                       |             query                                                                                                                       |
   |                       |         })                                                                                                                              |
   |                       |     });                                                                                                                                 |
   |                       |                                                                                                                                         |
   |                       |     if (!resp.ok) {                                                                                                                     |
   |                       |         console.log('Sending new relic change tracking failed: ' + resp.text());                                                        |
   |                       |     } else {                                                                                                                            |
   |                       |         console.log(resp.text());                                                                                                       |
   |                       |     }                                                                                                                                   |
   |                       | }                                                                                                                                       |
   |                       |                                                                                                                                         |
   |                       | trackDeployments();                                                                                                                     |
   |                       |                                                                                                                                         |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   ```

1. Noteer de integratie-id voor later gebruik. In dit voorbeeld is de id:

   ```terminal
   Created integration 767u4hathojjw (type: script)
   ```

   U kunt desgewenst de integratie verifiëren en de integratie-id noteren met: `magento-cloud integration:list`

1. Maak de omgevingsvariabele met behulp van de voorwaarden.

   ```bash
   magento-cloud variable:create --level project --name=env:NR_CONFIG --value='{"<YOUR_ENVIRONMENT_ID>":{"NR_API_KEY": "<YOUR_API_KEY>", "NR_API_URL": "https://api.newrelic.com/graphql", "NR_APP_GUID":"<YOUR_APP_GUID>"}}'  -p <YOUR_PROJECT_ID>
   ```

1. Controleer het laatste activiteitenlogboek.

   ```bash
   magento-cloud integration:activity:log <INTEGRATION_ID> -p <YOUR_PROJECT_ID> -e <YOUR_ENVIRONMENT_ID>
   ```

   Reactie:

   ```terminal
   Integration ID: 767u4hathojjw
   Activity ID: poxqidsfajkmg
   Type: integration.script
   Description: Running activity script
   Created: 2023-08-28T20:32:02+00:00
   State: complete
   Log:
   HTTP request
   HTTP response
   {"data":{"changeTrackingCreateDeployment":{"deploymentId":"some-deployment-id","entityGuid":"SomeGUIDhere"}}}
   ```

1. Aanmelden bij uw [New Relic-account](https://login.newrelic.com/login).

1. Klik in het navigatiemenu Verkenner op **[!UICONTROL APM & Services]**. Selecteer uw omgeving [!UICONTROL Name] en [!UICONTROL Account].

1. Onder _Gebeurtenissen_, klikt u op **[!UICONTROL Change tracking]**.

   ![Inzet](../../assets/new-relic/deployments.png)
