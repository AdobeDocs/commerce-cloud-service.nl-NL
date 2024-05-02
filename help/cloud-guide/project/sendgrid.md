---
title: E-mailservice SendGrid
description: Leer over de SendGrid e-mailservice voor Adobe Commerce op cloudinfrastructuur en hoe u uw DNS-configuratie kunt testen.
exl-id: 30d3c780-603d-4cde-ab65-44f73c04f34d
source-git-commit: 2b106edcaaacb63c0e785f094b7e1b755885abd0
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 0%

---

# E-mailservice SendGrid

De SendGrid Eenvoudige de volmachtsdienst van de Overdracht van de Post van het Protocol (SMTP) verleent de uitgaande e-mailauthentificatie en reputatie controlediensten, met inbegrip van steun voor:

* Alle uitgaande e-mails over een transactie
* Specifieke IP-adressen
* Domeinregistratie, DomainKeys Identified Mail (DKIM)-handtekeningen voor e-maildomeinvalidatie (alleen voor Pro Staging- en Production-omgevingen)
* Aangepaste domeinregistratie (alleen voor Pro)
* Geautomatiseerde integratie voor Starter- en Pro-integratieomgevingen. Pro-productie- en staging-omgevingen vereisen handmatige provisioning en configuratie tijdens het hardwareinrichtingsproces voor de infrastructuur als service (IaaS)

De SMTP-proxy van SendGrid is niet bedoeld voor gebruik als e-mailserver voor algemene doeleinden voor het ontvangen van binnenkomende e-mail of voor gebruik met e-mailmarketingcampagnes.

>[!TIP]
>
>U kunt SendGrid-details voor uw account vinden in het dialoogvenster [UI Onboarding](https://cloud.magento.com) en selecteert u de **Projectdetails** > **Hostgegevens** tab.

## E-mail in- of uitschakelen

U kunt uitgaande e-mailberichten voor elke omgeving in- of uitschakelen via de cloudconsole of de opdrachtregel.

Standaard zijn uitgaande e-mails ingeschakeld in Pro Production- en Staging-omgevingen. Maar [!UICONTROL Outgoing emails] kan worden weergegeven als uitgeschakeld in de omgevingsinstellingen totdat u de instelling `enable_smtp` eigenschap via de [opdrachtregel](outgoing-emails.md#enable-emails-in-the-cli) of [Cloud Console](outgoing-emails.md#enable-emails-in-the-cloud-console). U kunt uitgaande e-mails voor integratie- en staging-omgevingen inschakelen om tweefasenverificatie te verzenden of wachtwoorde-mails voor gebruikers van Cloud-projecten opnieuw in te stellen. Zie [E-mails configureren voor testen](outgoing-emails.md).

Als uitgaande e-mailberichten moeten worden uitgeschakeld of opnieuw ingeschakeld in een Pro Production- of Staging-omgeving, kunt u een [Adobe Commerce-ondersteuningsticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

>[!TIP]
>
>De [!UICONTROL enable_smtp] eigenschapswaarde van [opdrachtregel](outgoing-emails.md#enable-emails-in-the-cli) wijzigt ook de [!UICONTROL Enable outgoing emails] waarde instellen voor deze omgeving op de [Cloud Console](outgoing-emails.md#enable-emails-in-the-cloud-console).

## SendGrid-dashboard

Alle Cloud-projecten worden beheerd onder een centraal account, zodat alleen Support toegang heeft tot het SendGrid-dashboard. SendGrid biedt geen beperkingen voor subaccounts.

U kunt als volgt de activiteitenlogboeken controleren op de leveringsstatus of op een lijst met teruggestuurde, geweigerde of geblokkeerde e-mailadressen: [een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket). Het ondersteuningsteam **kan** activiteitslogboeken ophalen die ouder zijn dan 30 dagen.

Indien mogelijk, neem de volgende informatie met uw verzoek op:

* het desbetreffende e-mailadres of -adres
* het betrokken tijdschema (alleen binnen de afgelopen 30 dagen)
* het onderwerp van de e-mail

## DomainKeys Identified Mail (DKIM)

DKIM is een technologie van de e-mailauthentificatie die de Dienstverleners van Internet (ISPs) toelaat om zowel wettige als nep afzenderadressen, een techniek te identificeren die algemeen in phishing en e-mailzwendel wordt gebruikt. DKIM is afhankelijk van een domeineigenaar die de DNS-records beheert. Wanneer u DKIM gebruikt, gebruikt de server van de afzender een persoonlijke sleutel om de berichten te ondertekenen. De eigenaar van het domein voegt ook een DKIM-record toe. Dit is een gewijzigd bestand `TXT` record, naar de DNS-records van het zender-domein. Dit `TXT` het verslag bevat een openbare sleutel die de ontvankelijke postservers gebruiken om de handtekening van een bericht te verifiëren. De DKIM-cryptografie met openbare sleutels stelt ontvangers in staat de authenticiteit van een afzender te verifiëren. Zie [DKIM-records uitleg](https://docs.sendgrid.com/ui/account-and-settings/dkim-records).

>[!WARNING]
>
>De handtekeningen SendGrid DKIM en de steun van de domeinauthentificatie zijn slechts beschikbaar voor Pro projecten en niet de projecten van de Aanzet. Als gevolg hiervan worden uitgaande e-mailberichten over transacties waarschijnlijk gemarkeerd door spamfilters. Het gebruik van DKIM verbetert de leveringssnelheid als een geverifieerde e-mailafzender. Om de snelheid van de berichtlevering te verbeteren, kunt u van Starter aan Pro bevorderen of uw eigen server SMTP of dienstverlener van de e-maillevering gebruiken. Zie [E-mailverbindingen configureren](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/communications/email-communications) in de _Handleiding Admin Systems_.

### Afzender en domeinverificatie

Voor SendGrid om transactie-e-mails namens u van de milieu&#39;s van de Proproductie of van het Staging te verzenden, moet u uw DNS montages vormen om de drie subdomeinDNS ingangen te omvatten SendGrid. Aan elke SendGrid-account is een unieke waarde toegewezen `TXT` record waarmee uitgaande e-mailberichten worden geverifieerd.

**Domeinverificatie inschakelen**:

1. Een [ondersteuningsticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) om het toelaten van DKIM voor een specifiek domein (**Pro Staging- en productieomgevingen**).
1. Werk uw DNS configuratie met de `TXT` en `CNAME` dossiers die aan u in het steunkaartje worden verstrekt.

**Voorbeeld `TXT` opnemen met account-id**:

```text
v=spf1 include:u17504801.wl.sendgrid.net -all
```

**Voorbeeld `CNAME` records**:

| Domein | Punten naar | Recordtype |
| ---------- | ---------- | ------------- |
| em.emaildomain.com | uxxxxxx.wl.sendgrid.net | CNAME |
| s1._domainkey.emaildomain.com | s1.domainkey.uxxxxxx.wl.sendgrid.net | CNAME |
| s2._domainkey.emaildomain.com | s2.domainkey.uxxxxxx.wl.sendgrid.net | CNAME |

### DKIM-handtekeningen en geautomatiseerde beveiliging

U kunt kiezen tussen geautomatiseerde en handmatige beveiliging wanneer u een geverifieerd domein instelt. Als u geautomatiseerde veiligheid kiest, beheert SendGrid automatisch uw DKIM en SPF verslagen. Wanneer u een nieuw specifiek verzendend IP adres aan uw rekening toevoegt, werkt SendGrid uw DNS montages en handtekening DKIM onmiddellijk bij. Als u automatische beveiliging uitschakelt, bent u verantwoordelijk voor het bijwerken van uw DKIM-handtekening wanneer u uw verzendend domein wijzigt.

**Voorbeeld van geautomatiseerde beveiliging ingeschakeld**:

```text
subdomain.mydomain.com. | CNAME | uxxxxxx.wl.sendgrid.net
s1._domainkey.mydomain.com. | CNAME | s1.domainkey.uxxxxxx.wl.sendgrid.net
s2._domainkey.mydomain.com. | CNAME | s2.domainkey.uxxxxxx.wl.sendgrid.net
```

**Voorbeeld van automatische beveiliging uitgeschakeld**:

```text
me12345.mydomain.com | MX | mx.sendgrid.net
me12345.mydomain.com | TXT | v=spf1 include:sendgrid.net ~all
m1._mydomain.com | TXT | k=rsa; t=s; p=<public-key>
```

Nadat de domeinauthentificatie opstelling is, behandelt SendGrid automatisch het Kader van het Beleid van de Veiligheid (SPF) en DKIM verslagen voor u. Nadat SendGrid de `CNAME` de verslagen aan uw DNS verslagen toe te voegen, kunt u specifieke IP adressen toevoegen en andere rekeningsupdates maken zonder het moeten uw verslagen van SPF manueel beheren. Zie [Automatische beveiliging en uw DKIM-handtekening](https://docs.sendgrid.com/ui/account-and-settings/dkim-records#automated-security-and-your-dkim-signature).

Om uw DNS configuratie te testen:

```terminal
dig CNAME em.domain_name
dig CNAME s1._domainkey.domain_name
dig CNAME s2._domainkey.domain_name
```

## Drempel voor Transactionele e-mail

De drempel voor transactie-e-mail verwijst naar het aantal transactie-e-mailberichten dat u vanuit Pro-omgevingen binnen een specifieke periode kunt verzenden, zoals 12.000 e-mailberichten per maand vanuit niet-productieomgevingen. De drempel is ontworpen om te beschermen tegen het verzenden van spam en mogelijk uw e-mailreputatie te beschadigen.

Er zijn geen harde grenzen aan het aantal e-mails dat kan worden verzonden in de Productieomgeving, zolang de score voor de reproductie van de afzender meer dan 95% bedraagt. De reputatie wordt beïnvloed door het aantal gebrande of verworpen e-mails en of op DNS-Gebaseerde spamregisters uw domein als potentiële spambron hebben gemarkeerd. Zie [E-mails niet verzonden wanneer SendGrid-credits op Adobe Commerce worden overschreden](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/emails-not-being-sent-sendgrid-credits-exceeded) in de _Kennisbank handelsondersteuning_.

**Controleren of de maximale credits worden overschreden**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Gebruik SSH om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Controleer de `/var/log/mail.log` for `authentication failed : Maxium credits exceeded` vermeldingen.

   Als u een `authentication failed` logbestandvermeldingen en de **E-mailverzendingsreputatie** minimaal 95 is, kunt u [Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) om een verhoging van de krediettoewijzing aan te vragen.

### E-mailverzendingsreputatie

Een e-mailverzendende reputatie is een score die door een Internet Service Provider (ISP) wordt toegewezen aan een bedrijf dat e-mailberichten verzendt. Hoe hoger de score, des te waarschijnlijker is ISP berichten aan inbox van een ontvanger moet leveren. Als de score onder een bepaald niveau valt, kan ISP berichten aan de spamomslag van ontvangers leiden, of zelfs berichten volledig verwerpen. De reputatie score wordt bepaald door verscheidene factoren zoals een 30 daggemiddelde van uw IP adressen rangschikt tegen andere IP adressen en het tarief van de spamklacht. Zie [8 manieren om te controleren hoe je e-mailbericht wordt verzonden](https://sendgrid.com/en-us/blog/5-ways-check-sending-reputation).
