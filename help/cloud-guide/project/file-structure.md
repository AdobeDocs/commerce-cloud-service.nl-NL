---
title: Projectstructuur
description: Meer informatie over de bestandsstructuur en projectsjablonen voor Adobe Commerce op cloudinfrastructuur.
exl-id: 6dc559bd-116b-4745-a85b-731508e113ff
source-git-commit: 47ef728ea46b137eeaabbdbada940143d8773ef0
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# Projectstructuur

Een Adobe Commerce on cloud-infrastructuurproject bevat essentiële bestanden voor referenties en toepassingsconfiguratie. Deze bestanden zijn beschikbaar in de vorm van een sjabloon volgens de Adobe Commerce-versie. Zie de cloudsjablonen op basis van de Adobe Commerce-versie in het dialoogvenster [`magento/magento-cloud` GitHub-opslagplaats](https://github.com/magento/magento-cloud).

In de volgende tabel worden de bestanden beschreven die zijn opgenomen in een wolkenproject:

| Bestand | Beschrijving |
| ------------------------- | ------------ |
| `/.magento/routes.yaml` | Configuratiebestand dat wordt omgeleid `www` op het apex-domein en `php` om HTTP te bedienen. Zie [Verbindingen vormen](../routes/routes-yaml.md). |
| `/.magento/services.yaml` | Een configuratiedossier dat een instantie MySQL (MariaDB), Redis, en OpenSearch of Elasticsearch bepaalt. Zie [Services configureren](../services/services-yaml.md). |
| `/app` | De `code` wordt gebruikt voor aangepaste modules. De `design` map wordt gebruikt voor [aangepaste thema&#39;s](../store/custom-theme.md). De `etc` Deze map bevat configuratiebestanden voor de toepassing. |
| `/m2-hotfixes` | Wordt gebruikt voor aangepaste patches. |
| `/update` | Een de dienstomslag die door de steunmodule wordt gebruikt. |
| `.gitignore` | Geef op welke bestanden en mappen u wilt negeren. Zie [`.gitignore` referentie](#ignoring-files). |
| `.magento.app.yaml` | Een configuratiebestand dat de eigenschappen definieert om de toepassing samen te stellen. Zie [Toepassing configureren](../application/configure-app-yaml.md). |
| `.magento.env.yaml` | Het dossier van de configuratie voor de bouw, opstellen, en post-opstellen fasen. De `ece-tools` bevat een voorbeeld van dit bestand. Zie [Omgevingen configureren](../environment/configure-env-yaml.md). |
| `composer.json` | Zoekt Adobe Commerce en de configuratiescripts om uw toepassing voor te bereiden. Zie [Vereiste pakketten](../development/overview.md#required-packages). |
| `composer.lock` | Slaat versiegebiedsdelen voor elk pakket op. Zie [Vereiste pakketten](../development/overview.md#required-packages). |
| `magento-vars.php` | Wordt gebruikt om te definiëren [meerdere winkels](../store/multiple-sites.md) en sites die variabelen gebruiken. |

{style="table-layout:auto"}

>[!NOTE]
>
>Wanneer u uw lokale veranderingen in de verre server duwt, stelt manuscript in gebruik de waarden die door configuratiedossiers in `.magento` en verwijdert het script de map en de inhoud ervan. Dit heeft geen invloed op uw lokale ontwikkelomgeving.

## Hoofdmap van toepassing

De locatie van de hoofdmap van de toepassing is afhankelijk van de omgeving.

- **Starter en Pro-integratie**: `/app`
- **Startersproductie**: `/<project-ID>`
- **Pro Staging**: `/<project-ID>_stg`
- **Pro Production**: `/<project-ID>`

### Schrijfbare mappen

De externe integratie-, staging- en productieomgevingen zijn alleen-lezen. De volgende mappen zijn de *alleen* beschrijfbare directory&#39;s om beveiligingsredenen:

- `var`
- `pub/static`
- `pub/media`
- `app/etc`
- `/tmp`

>[!NOTE]
>
>In Productie en het Staging milieu&#39;s, heeft elk knooppunt in de drie knoopcluster een `/tmp` map die niet met de andere knooppunten wordt gedeeld.

## Bestanden negeren

Er is een basis `.gitignore` bestand met de Adobe Commerce op de projectopslagplaats voor cloudinfrastructuren. Zie de nieuwste [.gitignore-bestand in de magento-cloud-opslagplaats](https://github.com/magento/magento-cloud/blob/master/.gitignore). Om een dossier toe te voegen dat in `.gitignore` lijst kunt u de `-f` (kracht) optie bij het opslaan van een commit:

```bash
git add <path/filename> -f
```

## Basissjabloon wijzigen

U kunt de volgende stappen gebruiken om de structuur van een bestaand project te veranderen om het recentste basissjabloon voor Adobe Commerce op wolkeninfrastructuur te weerspiegelen.

1. Kloont het project aan een lokaal werkstation.

1. Werk de `composer.json` bestand met de volgende waarden voor het `extra` sectie.

   ```json
   "extra": {
       "magento-force": true
       "magento-deploystrategy": "copy"
   }
   ```

1. Voeg de `.gitignore` voor de basissjabloon ontworpen bestand. Als u bijvoorbeeld de opdracht `.gitignore` bestand voor de sjabloon version 2.2.6 gebruikt u de [.gitignore voor 2.2.6](https://github.com/magento/magento-cloud/blob/2.2.6/.gitignore) bestand als referentie.

1. Wis de git-cache.

   ```bash
   git rm -r --cached .
   ```

1. Wijzigingen toevoegen en doorvoeren.

   ```bash
   git add -A && git commit -m "Update base template"
   ```

{{redeploy-warning}}
