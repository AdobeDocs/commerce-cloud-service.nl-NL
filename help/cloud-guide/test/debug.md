---
title: Configureren [!DNL Xdebug]
description: Leer hoe u de Xdebug-extensie configureert voor foutopsporing in uw Adobe Commerce op het gebied van projecten voor cloudinfrastructuur.
exl-id: bf2d32d8-fab7-439e-8df3-b039e53009d4
source-git-commit: 751456f50e7b017b47c2ff43e008c2d04a558d96
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 0%

---

# Xdebug configureren

[!DNL Xdebug] is een extensie voor foutopsporing in uw PHP. Hoewel u winde van uw keus kunt gebruiken, verklaart het volgende hoe te te vormen [!DNL Xdebug] en [!DNL PhpStorm] om fouten op te sporen in uw lokale omgeving.

>[!NOTE]
>
>U kunt [!DNL Xdebug] om in de Cloud Docker-omgeving voor lokale foutopsporing uit te voeren zonder de projectconfiguratie van uw Adobe Commerce op de cloud-infrastructuur te wijzigen. Zie [Xdebug configureren voor Docker](https://developer.adobe.com/commerce/cloud-tools/docker/test/configure-xdebug/).

Inschakelen [!DNL Xdebug], moet u een dossier in uw bewaarplaats van de Git vormen, uw winde vormen, en de haven van opstelling door:sturen. U kunt bepaalde instellingen configureren in het dialoogvenster `magento.app.yaml` bestand. Na het bewerken voert u de Git-wijzigingen door in alle Starter-omgevingen en Pro-integratieomgevingen om [!DNL Xdebug]. [!DNL Xdebug] is al beschikbaar in Pro Staging &amp; Production-omgevingen.

Zodra gevormd, kunt u bevelen CLI, Webverzoeken, en code zuiveren. Houd er rekening mee dat alle omgevingen met cloudinfrastructuren alleen-lezen zijn. Kloont de code aan uw lokale ontwikkelomgeving om het zuiveren uit te voeren. Voor Pro Staging- en Productomgevingen raadpleegt u [aanvullende instructies](#debug-for-pro-staging-and-production) for [!DNL Xdebug].

## Vereisten

Uitvoeren en gebruiken [!DNL Xdebug], hebt u de SSH-URL voor de omgeving nodig. U kunt de informatie vinden via de [[!DNL Cloud Console]](../project/overview.md) of uw [!DNL Cloud Onboarding UI].

## Xdebug configureren

Om te vormen [!DNL Xdebug]Voer de volgende stappen uit:

- [In een vertakking werken om updates van bestanden door te voeren](#get-started-with-a-branch)
- [Inschakelen [!DNL Xdebug] voor omgevingen](#enable-xdebug-in-your-environment)
- [Vorm uw winde](#configure-phpstorm)
- [Poorten doorsturen instellen](#set-up-port-forwarding)

### Aan de slag met een vertakking

Toevoegen [!DNL Xdebug], raadt de Adobe aan [een ontwikkelingsafdeling](../dev-tools/cloud-cli-overview.md#create-an-environment-branch).

### Xdebug inschakelen in uw omgeving

U kunt [!DNL Xdebug] rechtstreeks naar alle Starter-omgevingen en Pro-integratieomgevingen. Deze configuratiestap is niet vereist voor Pro Production &amp; Staging-omgevingen. Zie [Foutopsporing voor Pro Staging en Production](#debug-for-pro-staging-and-production).

Inschakelen [!DNL Xdebug] voor uw project toevoegen `xdebug` aan de `runtime:extensions` van de `.magento.app.yaml` bestand.

**Xdebug inschakelen**:

1. In uw lokale terminal, open `.magento.app.yaml` in een teksteditor.

1. In de `runtime` sectie, onder `extensions`, toevoegen `xdebug`. Bijvoorbeeld:

   ```yaml
   runtime:
       extensions:
           - redis
           - xsl
           - newrelic
           - sodium
           - xdebug
   ```

1. Sla uw wijzigingen op in het dialoogvenster `.magento.app.yaml` en sluit de teksteditor af.

1. Voeg de wijzigingen toe, begaan en duw deze om de omgeving opnieuw te implementeren.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Add xdebug"
   ```

   ```bash
   git push origin <environment-ID>
   ```

Bij implementatie in Starter-omgevingen en Pro-integratieomgevingen, [!DNL Xdebug] is nu beschikbaar. Ga door met het configureren van uw IDE. Voor PHPStorm raadpleegt u [PhpStorm configureren](#configure-phpstorm).

### PhpStorm configureren

De [PhpStorm](https://www.jetbrains.com/phpstorm/) IDE moet worden gevormd om behoorlijk met te werken [!DNL Xdebug].

**PHPStorm configureren voor gebruik met Xdebug**:

1. Open in uw PhpStorm-project de **Instellingen** deelvenster.

   - _macOS_—Selecteren **PhpStorm** > **Voorkeuren**.
   - _Windows/Linux_—Selecteren **Bestand** > **Instellingen**.

1. In de _Instellingen_ het deelvenster, vouwt u de **Talen en kaders** > **PHP** > **Servers** sectie.

1. Klik op de knop **+** een serverconfiguratie toevoegen. De projectnaam is grijs bovenaan.

1. [Optioneel] Configureer de volgende instellingen voor de nieuwe serverconfiguratie. Zie [Geen foutopsporingsserver geconfigureerd](https://www.jetbrains.com/help/phpstorm/troubleshooting-php-debugging.html#no-debug-server-is-configured) in de _PHPStorm_ documentatie.

   - **Naam**—Ga het zelfde als hostname in. Deze waarde moet overeenkomen met de waarde voor de `PHP_IDE_CONFIG` variabele in [Foutopsporing CLI-opdrachten](#debug-cli-commands) om CLI voor het zuiveren te gebruiken.
   - **Host**—Voer de hostnaam in.
   - **Poort**—Enter `443`.
   - **Foutopsporing**—Selecteren `Xdebug`.

1. Selecteren **Padtoewijzingen gebruiken**. In de _Bestand/map_ deelvenster, de hoofdmap van het project voor het deelvenster `serverName` worden weergegeven.

1. In de **Absoluut pad op de server** kolom, klikt u op de **Bewerken** en voegt een instelling toe op basis van de omgeving.

   - Voor alle Starter-omgevingen en Pro-integratieomgevingen is het externe pad `/app`.
   - Voor Pro Staging- en Productieomgevingen:

      - Productie: `/app/<project_code>/`
      - Staging:  `/app/<project_code>_stg/`

1. Wijzig de [!DNL Xdebug] haven aan 9000 in **Talen en kaders** > **PHP** > **Foutopsporing** > **Xdebug** > **Foutopsporingspoort** deelvenster.

1. Klikken **Toepassen**.

### Poorten doorsturen instellen

Wijs de `XDEBUG` verbinding van de server met uw lokale systeem. Voor elk type foutopsporing moet u poort 9000 van uw Adobe Commerce op de server van de cloudinfrastructuur doorsturen naar uw lokale computer. Zie een van de volgende secties:

- [Poorten doorsturen in Mac of UNIX](#port-forwarding-on-mac-or-unix)
- [Poorten doorsturen in Windows](#port-forwarding-on-windows)

#### Poorten doorsturen op Mac of UNIX®

**Aan opstellings haven die op een Mac of in een milieu UNIX® door:sturen**:

1. Open een terminal.

1. Gebruik SSH om de verbinding te maken.

   ```bash
   ssh -R 9000:localhost:9000 <ssh url>
   ```

   Gebruik de `-v` (verbose) optie zodat wanneer een contactdoos met de haven wordt verbonden die door:sturen het in de terminal toont.

   Als een &quot;onbekwaam om&quot;te verbinden of &quot;niet aan haven op verre&quot;fout kon luisteren wordt getoond, kon er een andere actieve zitting van SSH die op de server voortduurt die haven 9000 bezet. Als die verbinding niet wordt gebruikt, kunt u het eindigen.

**Verbinding problemen oplossen**:

1. Gebruik SSH om u aan te melden bij de externe integratie, staging of productieomgeving.

1. Een lijst met SSH-sessies weergeven: `who`

1. Bestaande SSH-sessies op gebruiker weergeven. Wees voorzichtig dat u geen andere gebruiker aangaat dan uzelf!

   - integratie: gebruikersnamen zijn vergelijkbaar met `dd2q5ct7mhgus`
   - Staging: gebruikersnamen zijn vergelijkbaar met `dd2q5ct7mhgus_stg`
   - Productie: gebruikersnamen lijken op `dd2q5ct7mhgus`

1. Voor een gebruikerszitting die ouder is dan van u, vind de pseudo-terminal (PTS) waarde, zoals `pts/0`.

1. Vernietig de proces-id (PID) die overeenkomt met de PTS-waarde.

   ```bash
   ps aux | grep ssh
   kill <PID>
   ```

   Monsterrespons:

   ```terminal
   dd2q5ct7mhgus        5504  0.0  0.0  82612  3664 ?      S    18:45   0:00 sshd: dd2q5ct7mhgus@pts/0
   ```

   Om de verbinding te eindigen, ga een doodbevel met procesidentiteitskaart (PID) in.

   ```bash
   kill 3664
   ```

#### Poorten doorsturen in Windows

Aan opstellingshaven door:sturen (het een tunnel graven van SSH) op Vensters, moet u uw eindtoepassing van Vensters vormen. Dit voorbeeld stappen door het creëren van een tunnel van SSH gebruikend [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html). U kunt andere toepassingen gebruiken, zoals Cygwin. Raadpleeg de documentatie van de leverancier bij deze toepassingen voor meer informatie over andere toepassingen.

**Om een tunnel van SSH op Vensters te vestigen die Putty gebruikt**:

1. Als u dit nog niet hebt gedaan, downloadt u [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).

1. Start Putty.

1. Klik in het deelvenster Categorie op **Sessie**.

1. Voer de volgende gegevens in:

   - **Hostnaam (of IP-adres)** veld: voer de [SSH-URL](../development/secure-connections.md#connect-to-a-remote-environment) voor uw Cloud-server
   - **Poort** veld: Enter `22`

   ![Putty instellen](../../assets/xdebug/putty-session.png)

1. In de _Categorie_ deelvenster, klikt u op **Verbinding** > **SSH** > **Tunnels**.

1. Voer de volgende gegevens in:

   - **Bronpoort** veld: Enter `9000`
   - **Doel** veld: Enter `127.0.0.1:9000`
   - Klikken **Extern**

1. Klikken **Toevoegen**.

   ![Een SSH-tunnel maken in Putty](../../assets/xdebug/putty-tunnels.png)

1. In de _Categorie_ deelvenster, klikt u op **Sessie**.

1. In de **Opgeslagen sessies** gebied, ga een naam voor deze tunnel van SSH in.

1. Klikken **Opslaan**.

   ![Uw SSH-tunnel opslaan](../../assets/xdebug/putty-session-save.png)

1. Om de tunnel van SSH te testen, klik **Laden** en klik vervolgens op **Openen**.

   Als de fout &quot;Kan geen verbinding maken&quot; wordt weergegeven, controleert u het volgende:

   - Alle instellingen voor Putty zijn correct
   - U gebruikt Putty op de computer waarop uw privé Adobe Commerce op de sleutels van de de infrastructuurSSH van de wolkeninfrastructuur wordt gevestigd

## SSH-toegang tot Xdebug-omgevingen

Voor het in werking stellen van het zuiveren, het uitvoeren van opstelling, en meer, hebt u de bevelen van SSH voor de toegang tot van de milieu&#39;s nodig. U kunt deze informatie via de [[!DNL Cloud Console]](../development/secure-connections.md#use-an-ssh-command) en uw projectspreadsheet.

Voor Starter-omgevingen en Pro-integratieomgevingen kunt u het volgende gebruiken `magento-cloud` CLI bevel aan SSH in die milieu&#39;s:

```bash
magento-cloud environment:ssh --pipe -e <environment-ID>
```

Te gebruiken [!DNL Xdebug], SSH voor het milieu als volgt:

```bash
ssh -R <xdebug listen port>:<host>:<xdebug listen port> <SSH-URL>
```

Bijvoorbeeld:

```bash
ssh -R 9000:localhost:9000 pwga8A0bhuk7o-mybranch@ssh.us.magentosite.cloud
```

## Foutopsporing voor Pro Staging en Production

>[!NOTE]
>
>In Pro Staging &amp; Production-omgevingen, [!DNL Xdebug] is altijd beschikbaar omdat deze omgevingen een speciale installatie hebben voor [!DNL Xdebug]. Alle normale webaanvragen worden gerouteerd naar een speciaal PHP-proces dat niet [!DNL Xdebug]. Daarom worden deze verzoeken op normale wijze verwerkt en zijn zij niet onderworpen aan de verslechtering van de prestaties wanneer [!DNL Xdebug] is geladen. Wanneer een webaanvraag wordt verzonden die de [!DNL Xdebug] key, het wordt gerouteerd naar een afzonderlijk PHP proces dat [!DNL Xdebug] geladen.

Te gebruiken [!DNL Xdebug] specifiek op Pro plan het Staging en van de Productie milieu, creeert u een afzonderlijke tunnel van SSH en Webzitting slechts u toegang tot hebt. Dit gebruik verschilt van typische toegang, die slechts toegang tot u en niet aan alle gebruikers verleent.

U hebt het volgende nodig:

- SSH-opdrachten voor toegang tot de omgevingen. U kunt deze informatie via de [[!DNL Cloud Console]](../project/overview.md) of uw [!DNL Cloud Onboarding UI].
- De `xdebug_key` ingestelde waarde bij het configureren van de Staging- en Pro-omgevingen.

  De `xdebug_key` kan worden gevonden door SSH te gebruiken aan login aan de primaire knoop en het uitvoeren:

  ```bash
  cat /etc/platform/*/nginx.conf | grep xdebug.sock | head -n1
  ```

**Om een tunnel van SSH aan een het Staging of milieu van de Productie te vestigen**:

1. Open een terminal.

1. Maak alle SSH-sessies op voor elk webknooppunt van de cluster.

   ```bash
   ssh USERNAME@CLUSTER.ent.magento.cloud 'rm /run/platform/USERNAME/xdebug.sock'
   ```

1. Opstelling de tunnel van SSH voor Xdebug voor elke Webknoop van de cluster.

   ```bash
   ssh -R /run/platform/USERNAME/xdebug.sock:localhost:9000 -N USERNAME@CLUSTER.ent.magento.cloud
   ```

**Foutopsporing starten met de URL van de omgeving**:

1. Foutopsporing op afstand inschakelen; de site in de browser bezoeken en het volgende aan de URL toevoegen waar `KEY` is waarde voor `xdebug_key`.

   ```http
   ?XDEBUG_SESSION_START=KEY
   ```

   Met deze stap wordt het cookie ingesteld dat de browserverzoeken verzendt om te activeren [!DNL Xdebug].

1. Voltooi de foutopsporing met [!DNL Xdebug].

1. Wanneer u klaar bent om de zitting te beëindigen, gebruik het volgende bevel om het koekje te verwijderen en het zuiveren door browser te beëindigen waar `KEY` is waarde voor `xdebug_key`.

   ```http
   ?XDEBUG_SESSION_STOP=KEY
   ```

   >[!NOTE]
   >
   >De `XDEBUG_SESSION_START` doorgegeven door `POST` aanvragen worden niet ondersteund.

## Foutopsporing CLI-opdrachten

Deze sectie loopt door het zuiveren bevelen CLI.

Om CLI bevelen te zuiveren:

1. SSH in de server u wilt zuiveren gebruikend bevelen CLI.

1. Maak de volgende omgevingsvariabelen:

   ```bash
   export XDEBUG_CONFIG='PHPSTORM'
   ```

   ```bash
   export PHP_IDE_CONFIG="serverName=<name of the server that is configured in PHPSTORM>"
   ```

   Deze variabelen worden verwijderd wanneer de SSH-sessie wordt beëindigd.

1. Foutopsporing starten

   Bij Starter-omgevingen en Pro-integratieomgevingen voert u de CLI-opdracht uit om fouten op te sporen.
U kunt bijvoorbeeld runtime-opties toevoegen:

   ```bash
   php -d xdebug.profiler_enable=On -d xdebug.max_nesting_level=9999 bin/magento cache:clean
   ```

   In een Pro-testomgeving moet u het pad naar de [!DNL Xdebug] PHP-configuratiebestand bij foutopsporing in CLI-opdrachten, bijvoorbeeld:

   ```bash
   php -c /etc/platform/USERNAME/php.xdebug.ini bin/magento cache:clean
   ```

## Fouten opsporen in webverzoeken

De volgende stappen helpen u Webverzoeken zuiveren.

1. Op de _Extensie_ menu, klikt u op **Foutopsporing** om in te schakelen.

1. Klik met de rechtermuisknop, selecteer het optiemenu en stel de IDE-toets in op **PHPSTORM**.

1. Installeer de [!DNL Xdebug] op de browser. Vorm en laat het toe.

### Voorbeeld: Chrome instellen

In deze sectie wordt besproken hoe u het programma kunt gebruiken [!DNL Xdebug] in Chrome met de [!DNL Xdebug] Helperextensie. Voor informatie over [!DNL Xdebug] raadpleeg de documentatie van de browser voor andere browsers.

**Xdebug Helper gebruiken met Chrome**:

1. Een [SSH-tunnel](#ssh-access-to-xdebug-environments) naar de Cloud-server.

1. Installeer de [Xdebug Helper-extensie](https://chromewebstore.google.com/detail/eadndfjplgieldjbigjakmdgkmoaaaoc) in de Chrome-winkel.

1. Laat de uitbreiding in Chrome toe zoals aangetoond in het volgende cijfer.

   ![Xdebug-extensie inschakelen in Chrome](../../assets/xdebug/enable-chrome-ext.png)

1. Klik in Chrome met de rechtermuisknop op het groene hulppictogram op de werkbalk Chrome.

1. Klik in het pop-upmenu op **Opties**.

1. Van de _IDE-sleutel_ lijst, klik **PhpStorm**.

1. Klikken **Opslaan**.

   ![Xdebug Helper-opties](../../assets/xdebug/helper-options.png)

1. Open uw PhpStorm-project.

1. Klik in de bovenste navigatiebalk op de knop **Beginnen met luisteren** pictogram.

   Als de navigatiebalk niet wordt weergegeven, klikt u **Weergave** > **Navigatiebalk**.

1. Dubbelklik in het navigatievenster PHP op het PHP-bestand dat u wilt testen.

## Lokale code debuggen

Wegens de read-only milieu&#39;s, moet u code aan het lokale werkstation van een milieu of specifieke tak van de it trekken om het zuiveren uit te voeren.

De methode die u kiest, is aan u. U hebt de volgende opties:

- Code uitchecken vanuit Git en uitvoeren `composer install`

  Deze methode werkt tenzij `composer.json` verwijst naar pakketten in privéopslagruimten waartoe u geen toegang hebt. Met deze methode krijgt u de volledige Adobe Commerce-codebase.

- De `vendor`, `app`, `pub`, `lib`, en `setup` mappen

  Deze methode leidt ertoe dat u alle code hebt die u mogelijk kunt testen. Afhankelijk van het aantal statische elementen waarover u beschikt, kan dit resulteren in een lange overdracht met een groot volume bestanden.

- De `vendor` alleen directory

  Omdat het grootste deel van de code zich in de `vendor` Deze methode zal waarschijnlijk resulteren in goede tests, hoewel de volledige codebase niet wordt getest.

**Bestanden comprimeren en naar de lokale computer kopiëren**:

1. Gebruik SSH om u aan te melden bij de externe omgeving.

1. Comprimeer de bestanden.

   ```bash
   tar -czf /tmp/<file-name>.tgz <directory list>
   ```

   Als u bijvoorbeeld het dialoogvenster `vendor` alleen directory:

   ```bash
   tar -czf /tmp/vendor.tgz vendor
   ```

1. Gebruik PHPStorm in uw lokale omgeving om de bestanden te comprimeren.

   ```bash
   cd <phpstorm project root dir>
   ```

   ```bash
   rsync <SSH-URL>:/tmp/<file-name>.tgz .
   ```

   ```bash
   tar xzf <file-name>.tgz
   ```
