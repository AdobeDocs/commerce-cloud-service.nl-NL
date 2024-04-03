---
title: Het pakket ECE-gereedschappen bijwerken
description: Leer hoe u het pakket ECE-Tools kunt upgraden om te profiteren van de nieuwste oplossingen en functies die op Adobe Commerce op cloudinfrastructuur zijn toegepast.
feature: Cloud, Upgrade
exl-id: 7cce45eb-ae53-4468-b16d-4f4d3422ac52
source-git-commit: 513bc5b52f046ffd98005d80f34725b7f60b38bd
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# Het pakket ECE-gereedschappen bijwerken

Een update van de `ece-tools` pakket werkt ook het andere [Cloud Tools Suite voor handelspakketten](../release-notes/cloud-tools-suite.md), waarvoor `ece-tools`. Daarom moet u een versie van Adobe Commerce op wolkeninfrastructuur gebruiken die de `ece-tools` pakket.

{{ece-tools-package}}

**Vereisten**:

- Voordat u gaat bijwerken `ece-tools`, de [Opmerkingen bij de release Cloud Tools Suite voor handel](../release-notes/cloud-tools-suite.md).
- Als u bijwerkt vanuit `ece-tools` 2002.0.22 of eerder tot en met 2002.1.0 [Achterwaartse incompatibele wijzigingen](../release-notes/backward-incompatible-changes.md) en breng de vereiste wijzigingen aan in uw Adobe Commerce-infrastructuurproject voor de cloud.
- Controleren [Upgrades en patches](../development/commerce-version.md#upgrade-from-older-versions) om te bepalen welke versies van ECE-Tools compatibel zijn met uw Adobe Commerce voor het infrastructuurproject in de cloud.

{{upgrade-tip}}

**Als u het dialoogvenster `ece-tools` package**:

1. Voer op uw lokale werkstation een update uit met Composer.

   ```bash
   composer update magento/ece-tools --with-dependencies
   ```

   >[!NOTE]
   >
   >Als u niet verder kunt bijwerken `ece-tools` versie 2002.0.8, zie [Upgradeproject voor gebruik van het pakket ECE-Tools](install-package.md).

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Update magento/ece-tools"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Voeg deze vertakking na testvalidatie samen met de integratievertakking.
