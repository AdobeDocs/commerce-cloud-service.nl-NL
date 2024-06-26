---
title: Uitgaande e-mails configureren
description: Leer hoe u uitgaande e-mails voor Adobe Commerce kunt inschakelen voor cloudinfrastructuur.
exl-id: 814fe2a9-15bf-4bcb-a8de-ae288fd7f284
source-git-commit: 59f82d891bb7b1953c1e19b4c1d0a272defb89c1
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Uitgaande e-mails configureren

U kunt uitgaande e-mails voor elke omgeving in- en uitschakelen vanuit de [!DNL Cloud Console] of vanaf de opdrachtregel. U kunt uitgaande e-mails voor integratie- en staging-omgevingen verzenden om dubbele verificatie uit te voeren of wachtwoordgegevens opnieuw in te stellen voor gebruikers van Cloud-projecten.

Standaard zijn uitgaande e-mails ingeschakeld in productie- en staging-omgevingen. Maar [!UICONTROL Enable outgoing emails] kan worden weergegeven als uitgeschakeld in de omgevingsinstellingen totdat u de instelling `enable_smtp` eigenschap via de [opdrachtregel](#enable-emails-in-the-cli) of [Cloud Console](outgoing-emails.md#enable-emails-in-the-cloud-console).

De [!UICONTROL enable_smtp] eigenschapswaarde van [opdrachtregel](#enable-emails-in-the-cli) wijzigt ook de [!UICONTROL Enable outgoing emails] waarde instellen voor deze omgeving in de Cloud Console.

{{redeploy-warning}}

## E-mails inschakelen in de Cloud Console

Gebruik de **[!UICONTROL Outgoing emails]** schakelen in de _Omgeving configureren_ om e-mailondersteuning in of uit te schakelen.

Als uitgaande e-mailberichten moeten worden uitgeschakeld of opnieuw ingeschakeld in een Pro Production- of Staging-omgeving, kunt u een [Adobe Commerce-ondersteuningsticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

>[!TIP]
>
>De status van uitgaande e-mail wordt mogelijk niet weerspiegeld voor Pro-omgevingen in de Cloud Console. Gebruik in plaats daarvan de opdracht [opdrachtregel](#enable-emails-in-the-cli) voor het inschakelen en testen van uitgaande e-mails.

**E-mailondersteuning beheren vanuit de[!DNL Cloud Console]**:

1. Aanmelden bij de [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Selecteer een project in het menu _Alle projecten_ lijst.
1. Voor het dashboard van het Project, klik het configuratiepictogram in het hogere recht.
1. Klikken **[!UICONTROL Environments]** en selecteer een specifieke omgeving in de lijst.
1. Als u uitgaande e-mailberichten wilt in- of uitschakelen, schakelt u _Uitgaande e-mails inschakelen_ **Aan** of **Uit**.

   ![Configuratie uitgaande e-mail inschakelen](../../assets/outgoing-emails.png)

Nadat u het plaatsen verandert, bouwt het milieu en stelt met de nieuwe configuratie op.

## E-mails inschakelen in de CLI

U kunt de e-mailconfiguratie voor een actieve omgeving wijzigen met de opdracht `magento-cloud` CLI `environment:info` om de `enable_smtp` eigenschap. SMTP-updates inschakelen `MAGENTO_CLOUD_SMTP_HOST` omgevingsvariabele met het IP-adres van de SMTP-host voor het verzenden van e-mail.

**E-mailondersteuning beheren via de opdrachtregel**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Controleer de instelling voor de uitgaande e-mail voor de omgeving.

   ```bash
   magento-cloud environment:info -e <environment-id> | grep enable_smtp
   ```

1. Wijzig de configuratie van de e-mailondersteuning door het `enable_smtp` omgevingsvariabele naar `true` of `false`.

   ```bash
   magento-cloud environment:info --refresh -e <environment-id> enable_smtp true
   ```

   Wacht op het milieu om te bouwen en op te stellen.

1. Gebruik SSH aan login het verre milieu.

1. Controleer of het e-mailbericht werkt. Stuur een test-e-mail naar een adres dat u kunt controleren.

   ```bash
   php -r 'mail("mail@example.com", "test message", "just testing", "From: tester@example.com");'
   ```

1. Controleer of het e-mailbericht is opgehaald door SendGrid.

   ```bash
   grep mail@example.com /var/log/mail.log
   ```
