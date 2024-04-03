---
title: "Vertakkingen beheren met de [!DNL Cloud Console]"
description: Leer hoe u de omgevingstakken voor Adobe Commerce op cloudinfrastructuur beheert met de [!DNL Cloud Console].
role: Developer
feature: Cloud, Install
exl-id: 2c4ef149-fdb9-473f-91fd-5e6421ac5a43
source-git-commit: a5af3cc6e174a731a8f2ff198acd794384ef4585
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 0%

---

# Vertakkingen beheren met de [!DNL Cloud Console]

U kunt uw omgevingen beheren met de [!DNL Cloud Console] of de `magento-cloud` CLI. Uw projectbestanden worden opgeslagen in een Git-opslagplaats. U kunt Git-opdrachten gebruiken om uw code te beheren, maar de opdrachten `magento-cloud` CLI wordt ontworpen om met platformeigenschappen in wisselwerking te staan terwijl de bevelen van het Git niet. Zie [Opdrachten Git](../dev-tools/cloud-cli-overview.md#git-commands) in het Cloud CLI-onderwerp.

In dit onderwerp wordt besproken hoe u het dialoogvenster [!DNL Cloud Console] tot:

- Een omgeving toevoegen of verwijderen
- Sync (`git pull`) van de bovenliggende omgeving
- Samenvoegen (`git push`) aan de bovenliggende omgeving

>[!TIP]
>
>U kunt geen vertakkingen maken vanuit Pro Staging- en Productieomgevingen. U kunt vertakken vanuit de `master` vertakking.

## Een omgeving maken

De vertakkingsstrategie gebruikt een algemene Git-workflow waar u code ontwikkelt en extensies toevoegt in een ontwikkelingsvertakking. Zie [Starter](../architecture/starter-architecture.md) en [Pro](../architecture/starter-develop-deploy-workflow.md) architectuur-overzichten.

- Voor Starter maakt u een `staging` vertakking van `master` vertakking, dan vertakking van `staging` voor ontwikkeling.
- Voor Pro maakt u een ontwikkelingsvertakking vanuit de `Integration` milieu.

Uw account ondersteunt een beperkt aantal ![actieve vertakking](../../assets/icon-active.png){width="32"} (active) and an unlimited number of ![inactive branch](../../assets/icon-inactive.png){width="32"} (inactieve) ontwikkelingssectoren. Actieve en inactieve vertakkingen beheren door een vertakking toe te voegen of te verwijderen met alleen de [!DNL Cloud Console] of de Cloud CLI. Voordat u een vertakking kunt verwijderen, deactiveert u de vertakking, die in de _Omgevingen_ lijst als _inactief_. U kunt de vertakking later opnieuw activeren of [vertakking verwijderen](../dev-tools/cloud-cli-overview.md#) in omgevingen of met de Cloud CLI.

Als u aanvullende actieve omgevingen nodig hebt voor ontwikkeling, dient u een [Ondersteuningsticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket).

**Een vertakking toevoegen**:

1. Aanmelden bij de [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Selecteer een project in het menu _Alle projecten_ lijst.

1. Selecteer een omgeving.

   >[!TIP]
   >
   >Uw nieuwe vertakking is gekloond uit deze omgeving. Kies een bovenliggende omgeving die vergelijkbaar is met de omgeving die u gaat maken.

1. Klik op **[!UICONTROL Branch]**.

   ![Een vertakking maken](../../assets/button-branch.png){width="150"}

1. In de _Vertakking vanaf ..._ Voer een naam voor een vertakking in.

   Het milieu _name_ verschilt van het milieu _ID_ alleen als u spaties of hoofdletters in de omgevingsnaam gebruikt. Een milieu-id bestaat uit alle kleine letters, getallen en toegestane symbolen. Hoofdletters in een omgevingsnaam worden omgezet in kleine letters in de id. Spaties in een omgevingsnaam worden omgezet in streepjes.

   Een omgevingsnaam **kan** include-tekens die zijn gereserveerd voor uw Linux-shell of voor reguliere expressies. Verboden tekens bevatten accolades (`{ }`), ronde haakjes, asterisk (`*`), punthaken (`>`), ampersand (`&`), percentage (<code>%</code>) en andere tekens.

1. Selecteer een **[!UICONTROL Environment type]**.

1. Klik op **[!UICONTROL Create Branch]**.

1. Wacht terwijl het milieu opstelt.

   Tijdens de implementatie is de status van de omgeving  **In proces**. Na een geslaagde implementatie verandert de status in een groen vinkje voor **succes**.

## Inactieve vertakking maken

U kunt geen inactieve tak van de console van Adobe Commerce Cloud of CLI tot stand brengen. Als u een inactieve vertakking wilt maken, maakt u deze in de Git-opslagplaats en drukt u op de knop `environment.Parent` op de opdracht.

```bash
git push -o "environment.Parent=<parent branch>" <origin> <branch>
```

## Een omgeving verwijderen

Voordat u een omgeving kunt verwijderen, moet u deze deactiveren. Als een omgeving inactief is, kunt u deze verwijderen.

**Een omgeving deactiveren**:

1. Aanmelden bij de [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Selecteer een project in het menu _Alle projecten_ lijst.

1. Selecteer de omgeving op de navigatiebalk _Omgeving_ lijst.

1. Klik op het configuratiepictogram aan de rechterkant van de bovenste navigatiebalk om de omgevingsinstellingen te openen.

1. Op de _[!UICONTROL General]_tab, omlaag schuiven naar de_[!UICONTROL Deactivate environment]_ sectie en klik op **[!UICONTROL Deactivate environment and delete data]** en volgt u de instructies.

## Een omgeving synchroniseren

Een omgeving (of vertakking) synchroniseren is hetzelfde als `git pull origin <parent>`. U kunt bijgewerkte code synchroniseren vanuit een bovenliggende omgeving. U kunt deze functie gebruiken via de [!DNL Cloud Console] voor alle Starter- en Pro-omgevingen.

Voor een Pro-abonnement kunt u synchroniseren van Staging en Productie naar uw `master` vertakking. Deze synchronisatie trekt en duwt slechts code, niet gegevens. Om gegevens te synchroniseren, stort de gegevensbestandgegevens en duw het aan het gegevensbestand van een andere milieu. Zie [Statische bestanden en gegevens migreren en implementeren](/help/cloud-guide/deploy/staging-production.md#migrate-static-files).

**Een omgeving synchroniseren**:

1. Aanmelden bij de [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Selecteer een project in het menu _Alle projecten_ lijst.

1. Klik in de lijst met omgevingen op de naam van de vertakking die u wilt synchroniseren.

1. Klik (synchroniseren).

   ![Een omgeving synchroniseren](../../assets/button-sync.png){width="150"}

1. Selecteer de te synchroniseren items.

   - Vervang de gegevens—(gegevens en bestanden) synchroniseert wijzigingen in de database en inhoudsbestanden van de bovenliggende vertakking.
   - Met Samenvoegen—(code) wordt de bijgewerkte code van de bovenliggende vertakking gesynchroniseerd.

   Dit bouwt ook een bevel CLI voor u om te kopiëren en te gebruiken.

1. Klikken **Sync**.

## Samenvoegen met bovenliggende omgeving

Een omgeving (of vertakking) samenvoegen is hetzelfde als `git push origin`. U voegt samen om bijgewerkte code van een milieu aan zijn oudermilieu te duwen. U kunt deze code samenvoegen tot `master`. U kunt in Staging en Productie implementeren met de `merge` gebruiken.

**Samenvoegen met de bovenliggende omgeving**:

1. Aanmelden bij de [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Selecteer een project in het menu _Alle projecten_ lijst.

1. Klik in de lijst met omgevingen op de naam van de vertakking die u wilt samenvoegen.

1. Klik op Samenvoegen.

   ![Een omgeving samenvoegen](../../assets/button-merge.png){width="150"}

1. Klikken **Samenvoegen** en bevestig de actie.

## Logboeken weergeven

Via de [!DNL Cloud Console], kunt u diverse logboeken voor milieu&#39;s met inbegrip van bouwstijl, implementatie, en plaatsingsgeschiedenis herzien.

Voor **Starter**, kunt u bouwt en opstelt logboeken en de plaatsingsgeschiedenis herzien. Deze omgevingen omvatten `master` (Productie) filiaal en alle filialen die daarvan zijn gemaakt.

Voor **Pro** kunt u de volgende logbestanden in elke omgeving bekijken:

- Integratie-bouwt en opstelt en plaatsingsgeschiedenis
- Staging—Bouw logbestanden en implementatiegeschiedenis samen. Gebruik SSH om u aan te melden bij de server om logboeken voor implementatie weer te geven.
- Productie-bouw logboeken en plaatsingsgeschiedenis. Gebruik SSH om u aan te melden bij de server om logboeken voor implementatie weer te geven.

**Als u aanmeldingen wilt weergeven in het dialoogvenster[!DNL Cloud Console]**:

1. Aanmelden bij de [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Selecteer een project in het menu _Alle projecten_ lijst.

1. Selecteer een omgeving.

   De omgevingsweergave biedt een [Activiteitenlijst](activity-stream.md) dat toont _recent_ gebeurtenissen, één ingang per actie probeerde met inbegrip van syncs, fusies, takken, steunen, en meer. Klikken **Alles** voor de volledige plaatsingsgeschiedenis.

1. Om het bouwstijllogboek te bekijken, selecteer het Succes of de Verbinding van de Mislukking per plaatsingsverslag op de rekening.

>[!TIP]
>
>Klik op de knop **Filteren op** voor een vervolgkeuzelijst en selecteer het type berichten dat u wilt weergeven.

## Code ophalen uit een persoonlijke Git-opslagplaats

Uw Adobe Commerce on cloud-infrastructuurproject kan code van een privéopslagplaats voor Git bevatten. U hebt bijvoorbeeld code voor een aangepaste module of een aangepast thema in een privérepo. Hiervoor moet u de openbare SSH-sleutel van uw project toevoegen aan uw persoonlijke Git-opslagplaats en uw project bijwerken `composer.json` bestand.

Om een plaatsingssleutel aan uw privé bewaarplaats toe te voegen GitHub, moet u de beheerder van die bewaarplaats zijn. GitHub staat u toe om sleutel voor één bewaarplaats slechts te gebruiken opstellen.

Als u liever hebt dat uw project toegang krijgt tot meerdere opslagruimten, kunt u een SSH-sleutel aan een geautomatiseerde gebruikersaccount koppelen. Omdat dit account niet door een mens wordt gebruikt, wordt het een [computergebruiker](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys). Voeg de computeraccount toe als medewerker of voeg de gebruiker van de computer toe aan een team dat toegang heeft tot de opslagruimten.

>[!INFO]
>
>Adobe raadt u aan deze code toe te voegen en samen te voegen aan uw Git-opslagruimten voor projecten. Als u de verbinding niet vormt, kunt u bouwstijlkwesties ervaren.

**Om uw SSH openbare sleutel te vinden**:

1. Aanmelden bij de [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Selecteer een project in het menu _Alle projecten_ lijst.

1. Klik op het configuratiepictogram rechts van de bovenste navigatiebalk.

1. In _Projectinstellingen_, klikt u op **[!UICONTROL Deploy Key]**.

1. Kopieer de implementatiesleutel naar het klembord voor gebruik in een van de volgende op Git gebaseerde methoden:

>[!BEGINTABS]

>[!TAB GitHub]

### Ga uw sleutel van GitHub opstellen in

Op GitHub, stel sleutels in read-only door gebrek op.

**Om uw project openbare sleutel in te gaan aangezien GitHub sleutel opstelt**:

1. Meld u als beheerder aan bij uw GitHub-opslagplaats.
1. Klik op de opslagplaats **[!UICONTROL Settings]** tab.

   >[!NOTE]
   >
   >Als deze optie niet wordt weergegeven, wordt u niet aangemeld als beheerder van de gegevensopslagruimte en kunt u deze taak niet uitvoeren. Vraag uw beheerder van de bewaarplaats GitHub om dit te doen.

1. Op de _Instellingen_ in de linkernavigatie klikt u op **[!UICONTROL Deploy Keys]**.
1. Klik op **[!UICONTROL Add deploy key]**.
1. Volg de aanwijzingen.

In `composer.json`, gebruikt u de `<user>@<host>:<.git</code>` of `ssh://<user>@<host>:<port>/<path>.git` als u een niet-standaardpoort gebruikt.

>[!TAB Bitmap]

### Voer de implementatietoets voor bitmaps in

**Om uw project openbare sleutel in te gaan als Bitbucket opstellen sleutel**:

1. Meld u als beheerder aan bij de opslagplaats voor bitmaps.
1. Klik in de linkernavigatie op **[!UICONTROL Settings]**.
1. Klik op Algemeen > **[!UICONTROL Deployment Keys]**.
1. Klik op **[!UICONTROL Add Key]**.
1. Volg de aanwijzingen.

>[!TAB GitLab]

### Voer uw GitLab-implementatietoets in

**Om de openbare sleutel van SSH voor uw project toe te voegen zoals GitLab opstellen sleutel**:

1. Meld u als eigenaar aan bij de GitLab-opslagplaats.
1. Controleer of de _Pijpleidingen_ Deze optie is ingeschakeld voor uw project:

   1. Vouw in de projectinstellingen de **[!UICONTROL Visibility, project, features, permissions]** sectie.
   1. Klik indien nodig op **[!UICONTROL Pipelines]** om de optie in te schakelen.

1. Voeg uw openbare sleutel van SSH aan de montages CI/CD toe.

   1. Klik in de linkernavigatie op Instellingen > **[!UICONTROL CI / CD]**.
   1. Klik op Toepassingssleutels **Uitbreiden** om de sleutel te vormen.
   1. In de _Sleutel implementeren_ formulier, voeg een implementatiesleutel toe aan de **[!UICONTROL Title]** veld en plak de openbare SSH-toets in het dialoogvenster **[!UICONTROL Key]** veld.
   1. Klikken **[!UICONTROL Add Key]** om de configuratie op te slaan.

>[!ENDTABS]

## Beveiligde omgevingen en vertakkingen

U kunt uw project en milieu&#39;s van om het even welke plaats door Webbrowser toegang hebben gebruikend [!DNL Cloud Console]. U kunt veiligheid hebben die voor uw milieu, opslag, en plaatsen van de Productie wordt geplaatst. Deze sectie helpt u uw milieu&#39;s van de Integratie en van het Staging voor strikt uw ontwikkelaars, DBAs, en meer beveiligen.

>[!WARNING]
>
>**NIET** de volgende methoden gebruiken voor het beveiligen van Pro Staging- en Production-omgevingen. Dit verbreekt snel caching. Gebruik de [Blokkeren](../cdn/fastly-vcl-blocking.md) beschikbaar in de snelste CDN voor Adobe Commerce.

**Om omgevingen te beveiligen**:

1. Aanmelden bij de [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Selecteer een project in het menu _Alle projecten_ lijst.

1. Selecteer een omgeving en klik op het configuratiepictogram op de navigatiebalk.

1. Omgevingsinstellingen _Algemeen_ tabblad, klikt u op **ON** for **[!UICONTROL HTTP access control enabled]** om veilige toegang mogelijk te maken. U kunt tussen geloofsbrieven of IP adressen kiezen om voor toegang te filtreren.

1. Als u wilt filteren op referenties, klikt u op **[!UICONTROL Add Login]**, voert u een gebruikersnaam en wachtwoord in en klikt u op **[!UICONTROL Add Login]** toe te voegen.

1. Om door IP adres te filtreren, ga de IP adressen in een lijst met in `deny` of `allow`. Bijvoorbeeld:

   ```text
   123.456.789.111/29 allow
   123.456.789.112/29 allow
   234.123.567.111/29 allow
   0.0.0.0/0 deny
   ```

1. Klik op **[!UICONTROL Save]**. Hierdoor wordt de omgeving opnieuw geïmplementeerd om de beveiliging en instellingen bij te werken. Adobe raadt aan de omgeving te testen nadat de beveiligingsinstellingen zijn voltooid.
