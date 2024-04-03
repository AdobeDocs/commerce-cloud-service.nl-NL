---
title: Variables, eigenschap
description: Gebruik het bezit van variabelen om opslagconfiguratieopties voor aan te passen [!DNL Commerce] toepassing.
feature: Cloud, Configuration
exl-id: 5cd92fbb-8bff-48b1-9658-500140591344
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# Variables, eigenschap

U kunt op toepassing-gebaseerde omgevingsvariabelen gebruiken om opslagconfiguraties aan te passen. Deze variabelen gebruiken een specifieke syntaxis. Zie [Configuratie-instellingen overschrijven](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/override-config-settings.html) in de _Configuratiegids_.

In de `.magento.app.yaml` bestand is vereist voor specifieke versies van het [!DNL Commerce] toepassing.

Vereist voor Adobe Commerce 2.2.x tot 2.3.x:

```yaml
variables:
    env:
        CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
        CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL: 'Magento_Enterprise_Cloud_BT'
        CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
```

Stel voor Adobe Commerce 2.4.x de volgende variabelen in:

```yaml
variables:
    env:
        CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
        CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
```
