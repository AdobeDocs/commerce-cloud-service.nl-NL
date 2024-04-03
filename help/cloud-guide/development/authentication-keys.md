---
title: Verificatietoetsen
description: Leer hoe u verificatietoetsen toepast op een ontwikkelingsproject in Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Security
topic: Security
exl-id: b05cd4c2-0804-49c8-980a-4c7b6932082b
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Verificatietoetsen

U moet een verificatietoets hebben om toegang te krijgen tot de Adobe Commerce-opslagplaats en om installatie- en updateopdrachten voor uw Adobe Commerce in te schakelen voor het infrastructuurproject in de cloud. Er zijn twee methoden om de autorisatiegegevens van de Composer op te geven.

- **verificatiebestand**—Een bestand dat uw Adobe Commerce bevat [autorisatiegegevens](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/authentication-keys.html) in uw Adobe Commerce op de hoofdmap van de cloud-infrastructuur.
- **omgevingsvariabele**—Een omgevingsvariabele voor het instellen van verificatietoetsen in uw Adobe Commerce op een cloudinfragment om blootstelling door een ongeluk te voorkomen.

>[!BEGINSHADEBOX]

**Beveiligingsnotitie**

Adobe raadt u aan de [omgevingsvariabele](#composer-auth-environment-variable) met uw cloud-project om te voorkomen dat uw autorisatiegegevens per ongeluk worden weergegeven.

De methode van het authentificatiedossier is ideaal wanneer het gebruiken van Docker van de Wolk voor Handel als lokaal ontwikkelingshulpmiddel, maar ben zorgvuldig niet uploadt `auth.json` bestand naar een openbare Git-opslagplaats. U kunt de `auth.json` aan de [`.gitignore` file](../project/file-structure.md#ignoring-files).

>[!ENDSHADEBOX]

## Verificatiebestand

**Om een `auth.json` file**:

1. Als u geen `auth.json` in uw hoofdmap van het project, maakt u er een.

   - Maak met een teksteditor een `auth.json` in uw hoofdmap van het project.
   - Kopieer de inhoud van het dialoogvenster [monster `auth.json`](https://github.com/magento/magento2/blob/2.3/auth.json.sample) in de nieuwe `auth.json` bestand.

1. Vervangen `<public-key>` en `<private-key>` met uw Adobe Commerce-verificatiegegevens.

   ```json
   {
       "http-basic": {
           "repo.magento.com": {
               "username": "<public-key>",
               "password": "<private-key>"
           }
       }
   }
   ```

1. Sla de wijzigingen op en sluit de teksteditor af.

## Omgevingsvariabele van composer

De volgende methode is de beste manier om onbedoelde blootstelling van gevoelige gegevens in een openbare Git-opslagplaats te voorkomen.

**Verificatietoetsen toevoegen met behulp van een omgevingsvariabele**:

1. In de _[!DNL Cloud Console]_klikt u op het configuratiepictogram rechts van de projectnavigatie.

   ![Project configureren](../../assets/icon-configure.png){width="36"}

1. In de _Projectinstellingen_ lijst, klik **[!UICONTROL Variables]**.

1. Klik op **[!UICONTROL Create variable]**.

1. In de **[!UICONTROL Variable name]** veld, Enter `env:COMPOSER_AUTH`.

1. In de _Waarde_ veld, voeg het volgende toe en vervang `<public-key>` en `<private-key>` met uw Adobe Commerce-verificatiegegevens:

   ```json
   {
       "http-basic": {
           "repo.magento.com": {
               "username": "<public-key>",
               "password": "<private-key>"
           }
       }
   }
   ```

1. Selecteren **[!UICONTROL Available during buildtime]** en deselecteren **[!UICONTROL Available during runtime]**.

1. Klik op **[!UICONTROL Create variable]**.

1. Verwijder de `auth.json` bestand uit elke omgeving.
