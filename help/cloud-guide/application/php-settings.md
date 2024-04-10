---
title: PHP-instellingen
description: Leer over de optimale PHP montages voor de toepassingsconfiguratie van de Handel in de wolkeninfrastructuur.
feature: Cloud, Configuration, Extensions
exl-id: b4180265-f7a1-48e4-8c23-27835253e171
source-git-commit: 94c1e16a07567471d446478e3bd2a33977247ef3
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# PHP-instellingen

U kunt kiezen welke [versie van PHP](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) om in uw `.magento.app.yaml` bestand:

```yaml
name: mymagento
type: php:<version>
```

>[!TIP]
>
>Als u een upgrade uitvoert naar PHP 8.1 en hoger, verwijdert u JSON uit de [`runtime: extensions:` eigenschap](properties.md#runtime) in de `.magento.app.yaml` bestand en opnieuw implementeren. De JSON-extensie wordt sinds PHP 8.0 geïnstalleerd in de Cloud-omgeving.

## PHP configureren

U kunt de PHP-instellingen aanpassen voor uw omgeving met behulp van een `php.ini` bestand dat wordt toegevoegd aan de configuratie die door Adobe Commerce wordt onderhouden.

Voeg in de gegevensopslagruimte de `php.ini` naar de hoofdmap van de toepassing (de opslagplaats).

>[!TIP]
>
>Als PHP-instellingen onjuist worden geconfigureerd, kunnen er problemen optreden. Daarom moeten alleen gevorderde beheerders deze opties instellen.

### Limiet voor PHP-geheugen verhogen

Als u de limiet voor het PHP-geheugen wilt verhogen, voegt u de volgende instelling toe aan de `php.ini` bestand:

```ini
memory_limit = 1G
```

Voor het zuiveren, verhoog de waarde tot 2G.

### Configuratie realpath_cache optimaliseren

Het volgende instellen `realpath_cache` instellingen om de prestaties van de toepassing te verbeteren.

```conf
;
; Increase realpath cache size
;
realpath_cache_size = 10M

;
; Increase realpath cache ttl
;
realpath_cache_ttl = 7200
```

Met deze instellingen kunnen PHP-processen paden naar bestanden in cache plaatsen in plaats van ze voor elke pagina te bekijken die wordt geladen. Zie [Prestaties afstemmen](https://www.php.net/manual/en/ini.core.php) in de PHP documentatie.

>[!NOTE]
>
>Voor een lijst met aanbevolen PHP configuratie-instellingen raadpleegt u [Vereiste PHP-instellingen](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html) in de _Installatiehandleiding_.

### Aangepaste PHP-instellingen controleren

Nadat u de `php.ini` in uw Cloud-omgeving kunt u controleren of de aangepaste PHP-configuratie aan uw omgeving is toegevoegd. Gebruik bijvoorbeeld SSH om u aan te melden bij de externe omgeving en het bestand weer te geven met iets dat lijkt op het volgende:

```bash
cat /etc/php/<php-version>/fpm/php.ini
```

>[!WARNING]
>
>Als u Cloud Docker voor Handel voor lokale ontwikkeling gebruikt, raadpleegt u [Docker-servicecontainers](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#fpm-container) voor informatie over het gebruik van een aangepaste `php.ini` bestand in een Docker-omgeving.

## Extensies inschakelen

U kunt PHP-extensies in- of uitschakelen in het dialoogvenster `runtime:extension` sectie. Bovendien worden de opgegeven extensies beschikbaar in de Docker PHP containers.

>[!IMPORTANT]
>
>Voordat extensies kunnen worden ingeschakeld, is het belangrijk te begrijpen dat de PHP-versie compatibel moet zijn met het besturingssysteem dat het project host. Voor uw projectomgeving is mogelijk een upgrade van het besturingssysteem door het infrastructuurteam vereist voordat u kunt doorgaan.

Voorbeeld in `.magento.app.yaml` bestand:

```yaml
runtime:
    extensions:
        - sockets
        - sodium
        - ssh2
    disabled_extensions:
        - bcmath
        - bz2
        - calendar
        - exif
```

Gebruik SSH om u aan te melden bij een omgeving en geef een overzicht van de PHP-extensies.

```bash
php -m
```

Zie voor meer informatie over een specifieke PHP extensie de klasse [PHP-extensielijst](https://www.php.net/manual/en/extensions.alphabetical.php).

In de volgende tabel worden de ondersteunde PHP-extensies weergegeven wanneer Adobe Commerce wordt geïmplementeerd op het Cloud-platform.

{{$include /help/_includes/templated/php-extensions-cloud.md}}

PHP module requirements is linked to the Adobe Commerce version. Zie [PHP-vereisten](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html).

### Ondersteuning voor extensies

Voor Pro-projecten is aanvullende ondersteuning vereist voor de volgende extensies:

- `sourceguardian`

Als u bijvoorbeeld PHP zo wilt instellen dat alleen door SourceGuardian beveiligde scripts in alle omgevingen worden uitgevoerd, moet de volgende optie zijn ingesteld in het dialoogvenster `php.ini` bestand:

```ini
[SourceGuardian]
sourceguardian.restrict_unencoded = "1"
```

Zie [sectie 3.5 van de documentatie SourceGuardian](https://sourceguardian.com/demofiles/files/SourceGuardian%20for%20Linux%20User%20Manual.pdf). _Dit is een koppeling naar een PDF_.

[Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) voor hulp bij het installeren van deze PHP-extensies in alle productieomgevingen en Pro Staging-omgevingen. Uw bijgewerkte versie opnemen `.magento/services.yaml` bestand, `.magento.app.yaml` bestand met de bijgewerkte PHP versie en eventuele extra PHP extensies. Voor wijzigingen in een live productieomgeving moet u een minimale opzegtermijn van 48 uur opgeven. Het kan tot 48 uur duren voordat het infrastructuurteam van de cloud uw project kan bijwerken.

>[!WARNING]
>
>PHP gecompileerd met debug wordt niet ondersteund en de Probe kan conflicteren met [!DNL XDebug] of [!DNL XHProf]. Schakel die extensies uit wanneer u de sonde inschakelt. De sonde veroorzaakt een conflict met sommige PHP-extensies, zoals [!DNL Pinba] of IonCube.
