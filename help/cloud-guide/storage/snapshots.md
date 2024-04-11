---
title: Back-upbeheer
description: Leer hoe u handmatig een back-up voor uw Adobe Commerce-infrastructuurproject in de cloud kunt maken en herstellen.
feature: Cloud, Paas, Snapshots, Storage
exl-id: 1cb00db7-2375-4761-9c07-1e20a74859e0
source-git-commit: 069cbc233492d22932e8dce5bf0426dce8459727
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# Back-upbeheer

U kunt een handmatige back-up van actieve Starter-omgevingen op elk gewenst moment uitvoeren met de **[!UICONTROL Backup]** in de [!DNL Cloud Console] of door `magento-cloud snapshot:create` gebruiken.

Een back-up of _opname_ is een volledige back-up van omgevingsgegevens met alle permanente gegevens van actieve services (MySQL-database) en alle bestanden die zijn opgeslagen op de gekoppelde volumes (var, pub/media, app/etc). De opname doet dit _niet_ code opnemen, aangezien de code al is opgeslagen in de op Git gebaseerde gegevensopslagruimte. U kunt geen kopie van een opname downloaden.

De functie voor back-up/momentopname doet dit **niet** van toepassing zijn op de Pro Staging and Production-omgevingen, die standaard regelmatige back-ups ontvangen voor noodhersteldoeleinden. Zie [Pro-back-up en noodherstel](../architecture/pro-architecture.md#backup-and-disaster-recovery) voor meer informatie . In tegenstelling tot de automatische live back-ups in de Pro Staging and Production-omgeving, zijn back-ups **niet** automatisch. Het is _uw_ verantwoordelijkheid om handmatig een back-up te maken of een uitsnijdtaak in te stellen om periodiek een back-up van uw Starter- of Pro-integratieomgevingen te maken.

## Een handmatige back-up maken

U kunt een handmatige back-up maken van elke actieve Starter-omgeving en integratie Pro-omgeving vanuit de [!DNL Cloud Console] of maak een opname via de Cloud CLI. U moet een [Beheerdersrol](../project/user-access.md) voor het milieu

**Om een steun van om het even welke milieu van de Aanzet tot stand te brengen gebruikend[!DNL Cloud Console]**:

1. Aanmelden bij de [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Selecteer een omgeving in de projectnavigatiebalk. De omgeving moet actief zijn.
1. In de _Back-ups_ weergeven, klikken **[!UICONTROL Backup]**. Deze optie is niet beschikbaar voor een Pro-omgeving.

   ![Back-up](../../assets/button-backup.png){width="150"}

**Een back-up maken van een integratieomgeving met behulp van de[!DNL Cloud Console]**:

1. Aanmelden bij de [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Selecteer een integratie-/ontwikkelomgeving in de projectnavigatiebalk. De omgeving moet actief zijn.
1. Selecteer de **[!UICONTROL Backup]** in het menu rechtsboven. Deze optie is beschikbaar voor zowel Starter- als Pro-omgevingen.
1. Klik op de knop **[!UICONTROL Yes]** knop.

**Een opname maken met de opdracht `magento-cloud` CLI**:

1. Wijzig op uw lokale werkstation de projectmap.
1. Bekijk de omgevingsvertakking voor opname.
1. Maak de opname.

   ```bash
   magento-cloud snapshot:create --live
   ```

   U kunt ook de opdracht `magento-cloud backup` korte opdracht. De `--live` blijft de omgeving actief om downtime te voorkomen. Voor een volledige lijst met opties voert u `magento-cloud snapshot:create --help`.

   Monsterrespons:

   ```terminal
   Creating a snapshot of develop-branch
   Waiting for the activity ID (User created a backup of develop-branch):
   
   Creating backup of develop-branch
   Created backup my-snapshot
   [============================] 45 secs (complete)
   Activity ID succeeded
   Snapshot name: my-snapshot
   ```

1. Controleer de meest recente momentopnamen.

   ```bash
   magento-cloud snapshot:list
   ```

   De lijst retourneert informatie over de status van de momentopname:

   ```terminal
   Snapshots on the project (project-id), environment develop-branch (type: development):
   +---------------------------+----------------------+------------+
   | Created                   | Snapshot ID          | Restorable |
   +---------------------------+----------------------+------------+
   | 2023-03-08T17:07:01+00:00 | my-snapshot          | true       |
   +---------------------------+----------------------+------------+
   ```

## Een handmatige back-up herstellen

U moet [Toegang voor beheerders](../project/user-access.md) aan het milieu. U hebt maximaal **zeven dagen** tot _terugzetten_ een handmatige back-up. Bij het herstellen van een back-up wordt de code van de huidige git-vertakking niet gewijzigd. Een back-up op deze manier herstellen is niet van toepassing op Pro-testomgevingen en productieomgevingen. Zie [Pro-back-up en noodherstel](../architecture/pro-architecture.md#backup-and-disaster-recovery).

De hersteltijden variëren afhankelijk van de grootte van de database:

- grote database (200+ GB) kan 5 uur in beslag nemen
- middelgrote database (150 GB) kan 2 1/2 uur in beslag nemen
- kleine database (60 GB) kan 1 uur duren

>[!TIP]
>
>Herstellen zonder back-up:
>
>- Ga als volgt te werk om terug te gaan naar vorige code of toegevoegde extensies te verwijderen uit een omgeving: [Code terugdraaien](#roll-back-code).
>- Om een instabiele omgeving te herstellen die _niet_ een back-up maken, zie [Omgeving herstellen](../development/restore-environment.md).

**Als u een back-up wilt herstellen met de[!DNL Cloud Console]**:

1. Aanmelden bij de [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Selecteer een omgeving in de projectnavigatiebalk.
1. In de _Back-ups_ kies een back-up in het menu _Opgeslagen_ lijst. De back-upfunctie doet dit **niet** van toepassing zijn op de Pro-omgevingen.
1. In de ![Meer](../../assets/icon-more.png){width="32"} (_meer_), klikt u **Herstellen**.
1. Controleer de herstelgegevens op basis van back-upgegevens en klik op **Ja, herstellen**.

**Een opname herstellen met de Cloud CLI**:

1. Wijzig op uw lokale werkstation de projectmap.
1. Bekijk de omgevingsvertakking die u wilt herstellen.
1. Alle beschikbare momentopnamen weergeven.

   ```bash
   magento-cloud snapshot:list
   ```

   De lijst retourneert informatie over de beschikbare momentopnamen:

   ```terminal
   Snapshots on the project (project-id), environment develop-branch (type: development):
   +---------------------------+----------------------+------------+
   | Created                   | Snapshot ID          | Restorable |
   +---------------------------+----------------------+------------+
   | 2023-03-08T17:07:01+00:00 | my-snapshot          | true       |
   +---------------------------+----------------------+------------+
   ```

1. Herstel een momentopname gebruikend momentopname identiteitskaart van de lijst.

   ```bash
   magento-cloud snapshot:restore <snapshot-id>
   ```

## Code terugdraaien

Back-ups en momentopnamen doen _niet_ neem een kopie van de code op. Uw code is al opgeslagen in de op Git gebaseerde gegevensopslagruimte, zodat u Git-gebaseerde opdrachten kunt gebruiken om code terug te draaien (of terug te draaien). Gebruik bijvoorbeeld `git log --oneline` om door vorige verplichtingen te scrollen; dan gebruik [`git revert`](https://git-scm.com/docs/git-revert) om code van specifiek te herstellen begaat.

U kunt er ook voor kiezen om code op te slaan in een _inactief_ vertakking. Gebruik de opdrachten voor afsluiten om een vertakking te maken in plaats van deze te gebruiken `magento-cloud` opdrachten. Zie over [Opdrachten Git](../dev-tools/cloud-cli-overview.md#git-commands) in het Cloud CLI-onderwerp.
