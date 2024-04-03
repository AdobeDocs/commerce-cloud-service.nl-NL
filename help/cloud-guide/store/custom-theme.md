---
title: Aangepast thema
description: Leer hoe u een aangepast thema met Adobe Commerce installeert op cloudinfrastructuur.
feature: Cloud, Themes
exl-id: f08134ab-daea-471d-a927-02531d36a809
source-git-commit: bb7a866b1896a8a43d01ad3f83dc655bcf383374
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Aangepast thema

U kunt een of meerdere thema&#39;s installeren en gebruiken voor een of alle winkels en sites in uw project. Thema&#39;s bevatten meerdere statische bestanden, waaronder afbeeldingen, lettertypen, CSS, JavaScript, PHP en meer om uw winkels volledig te ontwerpen. U kunt het thema toevoegen door de code ervan naar het bestandssysteem te extraheren of door Composer te gebruiken.

## Een thema handmatig installeren

Als u een thema handmatig wilt installeren, moet u de themacode in een gecomprimeerd archief of in een directorystructuur hebben die lijkt op het volgende:

```text
<VendorName>
  ├── composer.json
      ├── etc
      │   └── view.xml
      ├── media
      ├── registration.php
      ├── theme.xml
      └── web
          ├── css
          │   └── source
          ├── fonts
          ├── images
          └── js
```

**Een thema handmatig installeren**:

1. De themacode kopiëren onder `<Project root dir>/app/design/frontend` voor een winkelthema of `<Project root dir>/app/design/adminhtml` voor een thema Admin. Controleren of de map op het hoogste niveau `<VendorName>`anders wordt het thema niet correct geïnstalleerd.

   ```bash
   cp -r ExampleTheme <project-root>/app/design/frontend
   ```

1. Bevestig het thema dat naar de juiste plaats is gekopieerd.

   * Winefront-thema: `ls <project-root>/app/design/frontend`
   * Thema beheerder: `ls <project-root>/app/design/adminhtml`

   Hieronder volgt een monster:

   ExampleTheme Adobe Commerce

1. Bestanden toevoegen en toewijzen.

   ```bash
   git add -A && git commit -m "Add theme"
   ```

1. Verplaats de bestanden naar de vertakking.

   ```bash
   git push origin <branch name>
   ```

1. Wacht tot de implementatie is voltooid.
1. Meld u aan bij de beheerder.
1. Klikken **Inhoud** > Ontwerp > **Thema&#39;s**.

   Het thema wordt weergegeven in het rechterdeelvenster.

## Een thema installeren met Composer

Het installeren van een thema met Composer is hetzelfde als het installeren van een andere extensie met Composer. Zie [Modules installeren, beheren en upgraden](extensions.md) voor meer informatie.

Een thema installeren met Composer:

1. Koop het thema uit Commerce Marketplace.
1. Haal de naam van de componist van het thema op.
1. Wijzig de hoofdmap van de Adobe Commerce en voer de opdracht in:

   ```bash
   composer require <vendor>/<name>:<version>
   ```

   Bijvoorbeeld:

   ```bash
   composer require zero1/theme-fashionista-theme:1.0.0
   ```

1. Wacht op gebiedsdelen om bij te werken.
1. Voer de volgende opdrachten in:

   ```bash
   git add -A && git commit -m "Add theme"
   ```

   ```bash
   git push origin <branch name>
   ```

1. Meld u aan bij de beheerder.
1. Klikken **Inhoud** > Ontwerp > **Thema&#39;s**.

   Het thema wordt weergegeven in het rechterdeelvenster.

## Meerdere thema&#39;s

Als u meerdere thema&#39;s gebruikt, zoals verschillende thema&#39;s per landinstelling, kunt u de opties `SCD_MATRIX` omgevingsvariabele voor het aanpassen van de themaimplementatie. Zie de [build](../environment/variables-build.md#scd_matrix) of [inzetten](../environment/variables-deploy.md#scd_matrix) in de [omgevingsconfiguratie](../environment/configure-env-yaml.md).
