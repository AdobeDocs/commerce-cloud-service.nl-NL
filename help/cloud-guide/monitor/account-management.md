---
title: New Relic-accountbeheer
description: Leer hoe u toegang krijgt tot uw New Relic-account en toegang, integratie en het gebruik van tools voor uw Adobe Commerce kunt beheren voor een cloud-infrastructuurproject.
feature: Cloud, Observability
role: Admin
exl-id: ee639e2e-4074-4384-8f68-152bc3bac93b
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# New Relic-accountbeheer

Wanneer de Adobe uw project van de wolkeninfrastructuur voorziet, ontvangt de Eigenaar van de Vergunning een e-mail van New Relic met geloofsbrieven en instructies voor de toegang tot van de rekening van New Relic. Als u het e-mailbericht niet hebt ontvangen, gebruikt u het e-mailadres van de eigenaar van de licentie om het New Relic-wachtwoord opnieuw in te stellen.

## Gebruikerstoegang beheren

Op een New Relic-account kan slechts één persoon worden toegewezen aan de rol Eigenaar. Als u de eigenaar van de account moet wijzigen, wijst u de beheerdersrol toe aan de huidige eigenaar en wijst u de rol Eigenaar toe aan een andere gebruiker. Zie [De rekeninghouder bijwerken](https://docs.newrelic.com/docs/accounts/original-accounts-billing/original-users-roles/users-roles-original-user-model/) in de _New Relic-documentatie_ voor instructies.

Richtlijnen voor het beheer van New Relic-toegang:

- Eigenaars van projecten en gebruikers van beheerders kunnen gebruikers toevoegen aan en verwijderen uit de New Relic-account.
- Maak niet meer dan vijf volledige toegangsrechten **Gebruikers**.
- Biedt alleen volledige toegang tot gebruikers die strikt toegang tot de volledige functieset vereisen.
- Er zijn geen specifieke richtsnoeren voor gratis **Beperkt** gebruikers.

>[!TIP]
>
>Voordat u de rol Eigenaar toewijst aan een gebruiker, moet u controleren of de gebruiker aanwezig is op de New Relic-account voor Adobe Commerce in de cloud-infrastructuur. Als u de gebruiker aan dat account moet toevoegen en een bestaande accounteigenaar of beheerder niet kan helpen, heeft iedere gebruiker toegang tot de [Eigenaarsaccount Adobe-partnerschap](https://account.newrelic.com/accounts/1311131/users) voor New Relic kan namens de klant gebruikers toevoegen.

Minstens één toevoegen **Beheerder** gebruiker aan uw New Relic-account die alle toegang, integratie en gereedschapsgebruik kan beheren.

**Toegang tot gebruikersbeheer in New Relic**:

1. Aanmelden bij uw [New Relic-account](https://login.newrelic.com/login).

1. Selecteer uw gebruikersnaam in de navigatie linksonder.

1. Klikken **[!UICONTROL Administration]** en selecteer een van de volgende opties in de lijst:

   - **[!UICONTROL User management]** om een gebruiker toe te voegen en actieve gebruikers en uitnodigingen in behandeling te beheren.

   - **[!UICONTROL Access management]** om gebruikersgroepen, rollen, en rekeningen te beheren.

Zie [Gebruikersbeheer](https://docs.newrelic.com/docs/accounts/accounts-billing/new-relic-one-user-management/user-management-ui-and-tasks/) in de _New Relic_ documentatie.

## New Relic for Starter-omgeving configureren

>[!NOTE]
>
>**Pro-omgevingen** zijn vooraf geconfigureerd voor het gebruik van New Relic-services en kunnen instructies voor inschakelen en verbinden overslaan. Als New Relic APM niet is geïnstalleerd in de Staging and Production-omgeving of als de New Relic-infrastructuur niet beschikbaar is in de productieomgeving, [een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om installatie aan te vragen.

Voor Starter-omgevingen moet u de `.magento.app.yaml` bestand om te controleren of de `runtime` bevat de New Relic-extensie. Als de extensie niet is geconfigureerd, voegt u het volgende toe:

> `.magento.app.yaml`

```yaml
runtime:
    extensions:
        - newrelic
```

### Licentiecode toepassen

Als u een Cloud-omgeving wilt verbinden met New Relic, voegt u de New Relic-licentiecode toe aan de omgeving.

- Voor **Pro-projecten**, voegt Adobe de licentiecode toe aan uw productie- en staging-omgevingen tijdens het inrichtingsproces. U kunt zich aanmelden bij uw [New Relic-account](https://login.newrelic.com/login) om de connectiviteit tussen uw Adobe Commerce op de cloudinframesite en New Relic te controleren.

- Voor **Startersprojecten**, hebt u een New Relic-licentiecode die ondersteuning biedt voor maximaal _drie_ omgevingen. U moet de sleutel aan uw omgevingsconfiguraties manueel toevoegen. Starteromgevingen zijn niet vooraf ingericht voor gebruik van de New Relic-service.

Voor Starter-omgevingen schakelt u de New Relic-integratie in door de New Relic-licentiecode toe te voegen aan de omgevingsconfiguratie. Voeg de sleutel toe aan de het Staging en milieu&#39;s van de Productie en één andere milieu van uw keus. Alleen de New Relic-licentiecode is vereist voor de configuratie. U vindt informatie over aanvullende configuratieopties in het dialoogvenster [New Relic Reporting](https://experienceleague.adobe.com/docs/commerce-admin/config/general/new-relic-reporting.html) in het _Adobe Commerce-gebruikershandleiding_.

{{redeploy-warning}}

>[!PREREQUISITES]
>
>- Aanmeldingsgegevens voor de Adobe Commerce-accountpagina of voor de New Relic-licentie voor uw project
>- [Toegang op beheerniveau](../project/user-access.md) naar de Starter-omgevingen om
>- Bevoegdheden om toegang te krijgen tot de [Beheerder](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions.html) milieu

**New Relic for Starter-omgevingen configureren**:

1. Zoek uw New Relic-licentiecode via [!DNL Cloud Console] of de Cloud CLI.

   **[!DNL Cloud Console]methode**:

   - Uw cloud-project openen [accountpagina](https://accounts.magento.cloud/user).

   - Op de _Projecten_ , zoekt u uw project.

   - Klikken **Details weergeven** voor informatie over de projectinfrastructuur.

   - Breid uit **New Relic Service** om de licentiecode weer te geven.

   - Kopieer de licentiecode.

   **Cloud CLI, methode**:

   ```bash
   magento-cloud subscription:info services.newrelic
   ```

1. Voeg de New Relic-licentiecode toe aan een omgeving met behulp van de `magento-cloud` CLI.

   - Verandering in het milieu dat de vergunningssleutel vereist.
   - Werk de waarde van de variabele als volgt bij `magento-cloud` CLI-opdracht:

     ```bash
     magento-cloud variable:update php:newrelic.license --value <newrelic-license-key>
     ```

   U kunt het desgewenst toevoegen vanuit het dialoogvenster [Commerce Admin](https://experienceleague.adobe.com/docs/commerce-admin/start/reporting/new-relic-reporting.html#step-3%3A-configure-your-store).

1. Aanmelden bij uw [New Relic-account](https://login.newrelic.com/login) om te controleren of u gegevens uit de Adobe Commerce-omgeving kunt bekijken. Zie [Prestaties onderzoeken](investigate-performance.md).

### Licentiecode verwijderen

U kunt uw New Relic-licentiecode alleen in drie actieve omgevingen gebruiken. Als de sleutel in gebruik in drie milieu&#39;s is, moet u de sleutel uit één van de milieu&#39;s verwijderen alvorens u het aan een verschillende milieu kunt toevoegen.

**Een licentiecode verwijderen uit een omgeving**:

1. Omgevingsvariabelen weergeven.

   ```bash
   magento-cloud variable:list
   ```

   Monsterrespons:

   ```terminal
    +----------------------+-------------+----------------------+---------+
    | Name                 | Level       | Value                | Enabled |
    +----------------------+-------------+----------------------+---------+
    | php:newrelic.license | environment | newrelic-license-key | true    |
    +----------------------+-------------+----------------------+---------+
   ```

   >[!WARNING]
   >
   >Als u de licentiecode als een _project_ variabele, moet u die project-vlakke variabele verwijderen. Een projectvariabele voegt de licentie toe aan _elke_ omgevingsvertakking gemaakt, die de licentielimiet kan verbruiken of overschrijden. Projectvariabelen weergeven: `magento-cloud variable:list --level project`

1. Verwijder de licentievariabele.

   ```bash
   magento-cloud variable:delete php:newrelic.license
   ```
