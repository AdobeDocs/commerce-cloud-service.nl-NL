---
source-git-commit: 2d902a3926c6bbc6a9dc8afcbd667eddeaf3be7e
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---
# Bestand opnemen om aangepaste VCL snel te wijzigen

## Het aangepaste VCL-fragment wijzigen

1. [Aanmelden](/help/get-started/onboarding.md#access-your-admin-panel) aan de beheerder.

1. Klikken **Winkels** > **Instellingen** > **Configuratie** > **Geavanceerd** > **Systeem**.

1. Uitbreiden **Volledige paginacache** > **Snelle configuratie** > **Aangepaste VCL-fragmenten**.

   ![Aangepaste VCL-fragmenten beheren](/help/assets/cdn/fastly-manage-snippets.png)

1. In de _Handeling_ klikt u op het instellingenpictogram naast het fragment dat u wilt bewerken.

1. Klik op **VCL snel uploaden naar** in de _Snelle configuratie_ sectie.

1. Nadat het uploaden is voltooid, vernieuwt u de cache volgens het bericht boven aan de pagina.

>[!WARNING]
>
>De _Aangepaste VCL-fragmenten_ Met de optie UI worden alleen de fragmenten weergegeven die via Adobe Commerce Admin zijn toegevoegd. Als u fragmenten toevoegt met de snelheids-API, gebruikt u de API voor [beheren](/help/cloud-guide/cdn/fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api).
