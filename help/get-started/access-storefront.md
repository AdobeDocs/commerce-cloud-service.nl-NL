---
title: Open het deelvenster Commerce Admin
description: Leer hoe u het deelvenster Commerce Admin kunt openen.
recommendations: noDisplay, catalog
exl-id: 9a8a0a49-b108-48bd-b413-ec9431370c06
source-git-commit: 3ca09243dc0a714c1d86cccf9f0620a8a39fd1e1
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Open het deelvenster Commerce Admin

Gebruikers die beheerdersrechten hebben tot het deelvenster Commerce Admin kunnen gebruikers toevoegen, winkelservices configureren, de installatie van de winkel voltooien en aanpassingen uitvoeren, enzovoort.

Voor een nieuw project, is de eerste stap na het ontvangen van welkome e-mail de toegang van Admin tot het project te beveiligen door het wachtwoord op de rekening van de Eigenaar van de Vergunning te veranderen. De standaardgebruikersnaam voor dit account is het e-mailadres van de eigenaar van de licentie.

U kunt een verzoek tot wijziging van het wachtwoord indienen op een van de volgende manieren:

- Zoek de welkomstmail die naar het e-mailadres van de Eigenaar van de licentie is verzonden en volg de koppeling en wijzig uw wachtwoord.

- Kopieer de URL van de winkel vanuit de [[!DNL Cloud Console]](../cloud-guide/project/overview.md) in een browser. Voeg vervolgens toe `/admin` aan het einde van de URL om de aanmeldpagina te openen. Klik op de knop **Wachtwoord vergeten?** koppeling om een verzoek tot wijziging van het wachtwoord naar het e-mailadres van de eigenaar van de licentie te verzenden.

Nadat u het verzoek tot wijziging van het wachtwoord hebt verzonden, controleert u uw e-mail op de melding voor het opnieuw instellen van het wachtwoord. Controleer de spammap als u geen e-mail ontvangt.

>[!TIP]
>
>Als het opnieuw instellen van het wachtwoord mislukt of als u zich niet kunt aanmelden bij het deelvenster Beheer, kan een gebruiker met beheerdersrechten verbinding maken met het project via SSH en een beheergebruiker toevoegen met behulp van het dialoogvenster `admin:user:create` CLI-opdracht. Zie [Een beheerdersaccount maken, bewerken of ontgrendelen](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/admin.html) in de _Installatiehandleiding_.

## Gezondheid van site controleren

De [Analyse voor de hele site](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/intro) is een proactief zelfbedieningshulpmiddel en een centrale gegevensopslagplaats die gedetailleerde systeeminzichten en aanbevelingen omvat om de veiligheid en de operabiliteit van uw installatie van Adobe Commerce te verzekeren. Het biedt 24/7 real-time prestatiescontrole, rapporten, en advies om potentiële kwesties en betere zichtbaarheid in plaatsgezondheid, veiligheid, en toepassingsconfiguraties te identificeren. Het helpt de resolutietijd te verminderen en de stabiliteit en prestaties van de site te verbeteren. U hebt rechtstreeks vanuit het dialoogvenster [Deelvenster Beheer](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/access#option-2-logging-in-to-your-site-wide-analysis-tool-dashboard-from-your-stores-admin-panel) of van de [toegewezen domein](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/access#option-1-logging-in-to-your-site-wide-analysis-tool-dashboard-directly-from-the-site-wide-analysis-tool-domain-for-adobe-commerce-on-cloud-infrastructure-only) (Adobe Commerce alleen voor infrastructuurprojecten in de cloud).
