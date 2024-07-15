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
>U kunt details SendGrid voor uw rekening in [ op het instappen UI ](https://cloud.magento.com) vinden en de **Details van het Project** selecteren > **het ontvangen Info** tabel.

## E-mail in- of uitschakelen

U kunt uitgaande e-mailberichten voor elke omgeving in- of uitschakelen via de cloudconsole of de opdrachtregel.

Standaard zijn uitgaande e-mails ingeschakeld in Pro Production- en Staging-omgevingen. Nochtans, [!UICONTROL Outgoing emails] kan gehandicapt in de milieu montages verschijnen tot u het `enable_smtp` bezit door de [ bevellijn ](outgoing-emails.md#enable-emails-in-the-cli) of [ Console van de Wolk ](outgoing-emails.md#enable-emails-in-the-cloud-console) plaatst. U kunt uitgaande e-mails voor integratie- en staging-omgevingen inschakelen om tweefasenverificatie te verzenden of wachtwoorde-mails voor gebruikers van Cloud-projecten opnieuw in te stellen. Zie [ e-mails voor het testen ](outgoing-emails.md) vormen.

Als de uitgaande e-mails moeten worden onbruikbaar gemaakt of op ProProductie of het Opvoeren milieu&#39;s opnieuw worden toegelaten, kunt u een [ kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) voorleggen.

>[!TIP]
>
>Het bijwerken van de [!UICONTROL enable_smtp] bezitswaarde door [ bevellijn ](outgoing-emails.md#enable-emails-in-the-cli) verandert ook de [!UICONTROL Enable outgoing emails] plaatsende waarde voor dit milieu op de [ Console van de Wolk ](outgoing-emails.md#enable-emails-in-the-cloud-console).

## SendGrid-dashboard

Alle Cloud-projecten worden beheerd onder een centraal account, zodat alleen Support toegang heeft tot het SendGrid-dashboard. SendGrid biedt geen beperkingen voor subaccounts.

Om de logboeken van de Activiteit voor leveringsstatus of een lijst van teruggestuurde, verworpen of geblokkeerde e-mailadressen te herzien, [ een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) voorleggen. Het team van de Steun **kan** activiteitenlogboeken niet terugwinnen ouder dan 30 dagen.

Indien mogelijk, neem de volgende informatie met uw verzoek op:

* het desbetreffende e-mailadres of -adres
* het betrokken tijdschema (alleen binnen de afgelopen 30 dagen)
* het onderwerp van de e-mail

## DomainKeys Identified Mail (DKIM)

DKIM is een technologie van de e-mailauthentificatie die de Dienstverleners van Internet (ISPs) toelaat om zowel wettige als nep afzenderadressen, een techniek te identificeren die algemeen in phishing en e-mailzwendel wordt gebruikt. DKIM is afhankelijk van een domeineigenaar die de DNS-records beheert. Wanneer u DKIM gebruikt, gebruikt de server van de afzender een persoonlijke sleutel om de berichten te ondertekenen. Bovendien voegt de eigenaar van het domein een DKIM-record (een gewijzigde `TXT` -record) toe aan de DNS-records van het afzender-domein. Deze `TXT` -record bevat een openbare sleutel die door e-mailservers van ontvangers wordt gebruikt om de handtekening van een bericht te controleren. De DKIM-cryptografie met openbare sleutels stelt ontvangers in staat de authenticiteit van een afzender te verifiëren. Zie ](https://docs.sendgrid.com/ui/account-and-settings/dkim-records) Verklaarde Verslagen DKIM [.

>[!WARNING]
>
>De handtekeningen SendGrid DKIM en de steun van de domeinauthentificatie zijn slechts beschikbaar voor Pro projecten en niet de projecten van de Aanzet. Als gevolg hiervan worden uitgaande e-mailberichten over transacties waarschijnlijk gemarkeerd door spamfilters. Het gebruik van DKIM verbetert de leveringssnelheid als een geverifieerde e-mailafzender. Om de snelheid van de berichtlevering te verbeteren, kunt u van Starter aan Pro bevorderen of uw eigen server SMTP of dienstverlener van de e-maillevering gebruiken. Zie [ E-mailverbindingen ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/communications/email-communications) in de _gids van Systemen Admin_ vormen.

### Afzender en domeinverificatie

Voor SendGrid om transactie-e-mails namens u van de milieu&#39;s van de Proproductie of van het Staging te verzenden, moet u uw DNS montages vormen om de drie subdomeinDNS ingangen te omvatten SendGrid. Aan elke SendGrid-account wordt een unieke `TXT` -record toegewezen waarmee uitgaande e-mailberichten worden geverifieerd.

**om domeinauthentificatie** toe te laten:

1. Verzend a [ steunkaartje ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) om het toelaten van DKIM voor een specifiek domein (**Pro het Opvoeren en de milieu&#39;s van de Productie slechts**) te verzoeken.
1. Werk uw DNS-configuratie bij met de `TXT` - en `CNAME` -records die in het ondersteuningsticket aan u worden geleverd.

**Voorbeeld `TXT` verslag met rekeningsidentiteitskaart**:

```text
v=spf1 include:u17504801.wl.sendgrid.net -all
```

**Voorbeeld `CNAME` verslagen**:

| Domein | Punten naar | Recordtype |
| ---------- | ---------- | ------------- |
| em.emaildomain.com | uxxxxxx.wl.sendgrid.net | CNAME |
| s1._domainkey.emaildomain.com | s1.domainkey.uxxxxxx.wl.sendgrid.net | CNAME |
| s2._domainkey.emaildomain.com | s2.domainkey.uxxxxxx.wl.sendgrid.net | CNAME |

### DKIM-handtekeningen en geautomatiseerde beveiliging

U kunt kiezen tussen geautomatiseerde en handmatige beveiliging wanneer u een geverifieerd domein instelt. Als u geautomatiseerde veiligheid kiest, beheert SendGrid automatisch uw DKIM en SPF verslagen. Wanneer u een nieuw specifiek verzendend IP adres aan uw rekening toevoegt, werkt SendGrid uw DNS montages en handtekening DKIM onmiddellijk bij. Als u automatische beveiliging uitschakelt, bent u verantwoordelijk voor het bijwerken van uw DKIM-handtekening wanneer u uw verzendend domein wijzigt.

**Geautomatiseerde toegelaten veiligheid van het Voorbeeld**:

```text
subdomain.mydomain.com. | CNAME | uxxxxxx.wl.sendgrid.net
s1._domainkey.mydomain.com. | CNAME | s1.domainkey.uxxxxxx.wl.sendgrid.net
s2._domainkey.mydomain.com. | CNAME | s2.domainkey.uxxxxxx.wl.sendgrid.net
```

**Geautomatiseerde van het Voorbeeld gehandicapte veiligheid**:

```text
me12345.mydomain.com | MX | mx.sendgrid.net
me12345.mydomain.com | TXT | v=spf1 include:sendgrid.net ~all
m1._mydomain.com | TXT | k=rsa; t=s; p=<public-key>
```

Nadat de domeinauthentificatie opstelling is, behandelt SendGrid automatisch het Kader van het Beleid van de Veiligheid (SPF) en DKIM verslagen voor u. Nadat SendGrid de `CNAME` verslagen verstrekt om aan uw DNS verslagen toe te voegen, kunt u specifieke IP adressen toevoegen en andere rekeningsupdates maken zonder het moeten uw SPF verslagen manueel beheren. Zie [ Geautomatiseerde Veiligheid en Uw Ondertekening DKIM ](https://docs.sendgrid.com/ui/account-and-settings/dkim-records#automated-security-and-your-dkim-signature).

Om uw DNS configuratie te testen:

```terminal
dig CNAME em.domain_name
dig CNAME s1._domainkey.domain_name
dig CNAME s2._domainkey.domain_name
```

## Drempel voor Transactionele e-mail

De drempel voor transactie-e-mail verwijst naar het aantal transactie-e-mailberichten dat u vanuit Pro-omgevingen binnen een specifieke periode kunt verzenden, zoals 12.000 e-mailberichten per maand vanuit niet-productieomgevingen. De drempel is ontworpen om te beschermen tegen het verzenden van spam en mogelijk uw e-mailreputatie te beschadigen.

Er zijn geen harde grenzen aan het aantal e-mails dat kan worden verzonden in de Productieomgeving, zolang de score voor de reproductie van de afzender meer dan 95% bedraagt. De reputatie wordt beïnvloed door het aantal gebrande of verworpen e-mails en of op DNS-Gebaseerde spamregisters uw domein als potentiële spambron hebben gemarkeerd. Zie [ E-mails niet verzonden wanneer de credits SendGrid op Adobe Commerce ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/emails-not-being-sent-sendgrid-credits-exceeded) in de _Kennisbank van de Steun van Commerce_ werden overschreden.

**om te controleren als de maximumkredieten** worden overschreden:

1. Wijzig op uw lokale werkstation de projectmap.

1. Gebruik SSH om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Controleer de `/var/log/mail.log` op `authentication failed : Maxium credits exceeded` -items.

   Als u om het even welke `authentication failed` logboekingangen ziet en **E-mail verzendende reputatie** is bij een minimum van 95, kunt u [ een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) voorleggen om een verhoging van de krediettoewijzing te verzoeken.

### E-mailverzendingsreputatie

Een e-mailverzendende reputatie is een score die door een Internet Service Provider (ISP) wordt toegewezen aan een bedrijf dat e-mailberichten verzendt. Hoe hoger de score, des te waarschijnlijker is ISP berichten aan inbox van een ontvanger moet leveren. Als de score onder een bepaald niveau valt, kan ISP berichten aan de spamomslag van ontvangers leiden, of zelfs berichten volledig verwerpen. De reputatie score wordt bepaald door verscheidene factoren zoals een 30 daggemiddelde van uw IP adressen rangschikt tegen andere IP adressen en het tarief van de spamklacht. Zie [ 8 Manieren om Uw E-mail te controleren die Reputatie ](https://sendgrid.com/en-us/blog/5-ways-check-sending-reputation) verzendt.
