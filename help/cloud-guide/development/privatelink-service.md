---
title: PrivateLink-service
description: Leer hoe u de PrivateLink-service gebruikt om een veilige verbinding tot stand te brengen tussen een privécloud en een Adobe Commerce-cloudplatform in dezelfde regio.
feature: Cloud, Iaas, Security
exl-id: b25548b8-312b-4a74-b242-f4e2ac6cf945
source-git-commit: 5b52157c6c623bb4c765a2d545919df79d81f1da
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 0%

---

# PrivateLink-service

Adobe Commerce over cloud-infrastructuur ondersteunt integratie met de [AWS PrivateLink](https://aws.amazon.com/privatelink/) of [Azure Private Link](https://learn.microsoft.com/en-us/azure/private-link/) service. U kunt PrivateLink gebruiken om veilige, persoonlijke communicatie tot stand te brengen tussen Adobe Commerce in omgevingen met cloudinfrastructuren met services en toepassingen die worden gehost op externe systemen. Zowel de Adobe Commerce-toepassing als externe systemen moeten toegankelijk zijn via Virtual Private Cloud (VPC)-eindpunten die zijn geconfigureerd op hetzelfde cloud-platform (AWS of Azure) in dezelfde cloud-regio.

>[!TIP]
>
>PrivateLink kan het best worden gebruikt voor het beveiligen van verbindingen voor niet-HTTP(S)-integratie, zoals database- of bestandsoverdrachten. Als u van plan bent uw toepassing te integreren met Adobe Commerce API&#39;s, raadpleegt u hoe u een [Adobe-API-net](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/) in _API-net voor Adobe Developer App Builder_.

## Functies en ondersteuning

De PrivateLink-service-integratie voor Adobe Commerce op cloud-infrastructuurprojecten omvat de volgende functies en ondersteuning:

- Een veilige verbinding tussen een klant Virtual Private Cloud (VPC) en de Adobe VPC op hetzelfde cloudplatform (AWS of Azure) binnen dezelfde Cloud-regio.
- Steun voor unidirectionele of bidirectionele communicatie tussen eindpuntdiensten beschikbaar bij Adobe en Klant VPCs.
- Inschakelen van service:

   - Open vereiste poorten in de Adobe Commerce in de cloud-infrastructuuromgeving
   - De eerste verbinding tussen de klant en Adobe-VPC&#39;s tot stand brengen
   - Verbindingsproblemen oplossen tijdens inschakelen

## Beperkingen

- Ondersteuning voor PrivateLink is alleen beschikbaar in Pro Production- en Staging-omgevingen. Het is niet beschikbaar op lokale of integratieomgevingen, of op Starter-projecten.
- U kunt geen verbindingen tot stand brengen SSH gebruikend PrivateLink. Zie [SSH-toetsen inschakelen](secure-connections.md).
- Adobe Commerce-ondersteuning biedt geen ondersteuning voor het oplossen van problemen met AWS PrivateLink buiten initiële activering.
- Klanten zijn verantwoordelijk voor de kosten die gepaard gaan met het beheer van hun eigen VPC.
- U kunt het HTTPS-protocol (poort 443) niet gebruiken om via Azure Private Link verbinding verbinding te maken met Adobe Commerce op cloudinfrastructuur [Camoufleren met een snelle oorsprong](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/faq/fastly-origin-cloaking-enablement-faq.html). Deze beperking geldt niet voor AWS PrivateLink.
- PrivateDNS is niet beschikbaar.

## Verbindingstypen van PrivateLink

Er zijn twee PrivateLink verbindingstypes beschikbaar-getoond in het volgende netwerkdiagram-om veilige communicatie tussen uw opslag en externe systemen te vestigen die buiten het milieu van de Wolk worden ontvangen.

![Het netwerkdiagram van PrivateLink](../../assets/privatelink-architecture-diagram.png)

Kies een van de verbindingstypen voor PrivateLink die het meest geschikt zijn voor uw Adobe Commerce in omgevingen met cloudinfrastructuren:

- **Unidirectionele PrivateLink**-Kies deze configuratie om gegevens veilig op te halen uit een Adobe Commerce in de cloud Infrastructure Store.
- **Bidirectionele PrivateLink**-Kies deze configuratie om veilige verbindingen tot stand te brengen met en van systemen buiten de Adobe Commerce op de omgeving van de cloudinfrastructuur. De bidirectionele optie vereist twee verbindingen:

   - Een verbinding tussen de klant VPC en de Adobe VPC
   - Een verbinding tussen de Adobe VPC en de klant VPC

>[!TIP]
>
>Werk met uw netwerkbeheerder of leverancier van het platform van de Wolk voor hulp met het selecteren van het PrivateLink verbindingstype, of hulp met opstelling en beleid VPC. Zie de documentatie van PrivateLink voor het Cloud-platform: [AWS PrivateLink](https://aws.amazon.com/privatelink/) of [Azure Private Link](https://learn.microsoft.com/en-us/azure/private-link/).

## Enable PrivateLink aanvragen

>[!WARNING]
>
>Als u PrivateLink inschakelt, kan dit maximaal _vijf_ werkdagen. Het verstrekken van onvolledige of onjuiste informatie kan het proces vertragen.

### Vereisten

![controleren](../../assets/fix.svg) Een Cloud-account (AWS of Azure) in dezelfde regio als de Adobe Commerce op een cloudinfragment.

![controleren](../../assets/fix.svg) Een VPC in het klantenmilieu dat gastheren de diensten om door PrivateLink te verbinden. Raadpleeg de documentatie bij AWS of Azure voor hulp bij de installatie van VPC of neem contact op met uw netwerkbeheerder.

![controleren](../../assets/fix.svg) Voor bidirectionele verbindingen PrivateLink, moet u de configuratie van de eindpuntdienst voor uw toepassing of dienst tot stand brengen, en een eindpunt in uw milieu creëren VPC alvorens om PrivateLink te verzoeken enablement. Zie [Instellen voor bidirectionele Private Link-verbindingen](#set-up-for-bidirectional-privatelink-connections).

Verzamel de volgende gegevens die voor PrivateLink worden vereist toelaat:

- **Customer Cloud-accountnummer** (AWS of Azure)—Moet zich in dezelfde regio bevinden als de Adobe Commerce op de instantie van de cloud-infrastructuur
- **Cloud-gebied**—Geef het Cloud-gebied op waar het account wordt gehost voor verificatiedoeleinden
- **Diensten- en communicatiepoorten**—Adobe moet havens openen om de dienstmededeling tussen VPCs, bijvoorbeeld SQL haven 3306, haven 2222 van SFTP toe te laten
- **Project-id**—Geef de Adobe Commerce op voor het project-id van de cloud-infrastructuur Pro. U kunt project identiteitskaart en andere projectinformatie krijgen gebruikend het volgende [Cloud CLI](../dev-tools/cloud-cli-overview.md) opdracht: `magento-cloud project:info`
- **Verbindingstype**—Unidirectioneel of bidirectioneel opgeven voor verbindingstype
- **Endpoint-service**—Voor bidirectionele verbindingen PrivateLink, verstrek DNS URL voor de VPC eindpuntdienst die de Adobe met moet verbinden, bijvoorbeeld: `com.amazonaws.vpce.<cloud-region>.vpce-svc-<service-id>`
- **Toegang tot eindpuntservice verleend**—Om met de externe dienst te verbinden, sta de eindpuntdienst toegang tot het volgende de rekeningshoofd van AWS toe: `arn:aws:iam::402592597372:root`

  >[!WARNING]
  >
  >Als de toegang tot de eindpuntdienst niet wordt verleend, dan is de bidirectionele verbinding PrivateLink aan de dienst in uw VPC **niet** toegevoegd, waardoor de installatie wordt vertraagd.

#### Aanvullende voorwaarden specifiek voor Azure Private Link-activering

- Geef de cluster-id op; gebruik SSH, meld u aan bij de externe server en gebruik de opdracht: `cat /etc/platform_cluster`
- Een externe service kan alleen verbinding maken met uw Adobe Commerce Pro-cluster als u:

   - Een lijst van havens op uw Pro cluster om aan het nieuwe externe Privé Eindpunt bloot te stellen
   - Een lijst van Azure abonnement IDs voor de verbindingen van het Privé Eindpunt

- Als u uw Adobe Commerce Pro-cluster wilt verbinden met een externe service, hebt u het volgende nodig:

   - Een lijst van middel IDs voor de doeldiensten. De externe Privé dienst IDs van de Verbinding kijken gelijkaardig aan het volgende:

  ```text
  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/privateLinkServices/{svcNameID}
  ```

### Workflow Enablement

In de volgende workflow wordt beschreven hoe u PrivateLink-integratie met Adobe Commerce kunt inschakelen voor cloudinfrastructuur.

1. **Klant** legt een steunkaartje voor die om PrivateLink toelaat met de onderwerpregel verzoekt `PrivateLink support for <company>`. Inclusief de [voor activering vereiste gegevens](#prerequisites) in het ticket. De Adobe gebruikt het kaartje van de Steun om mededeling tijdens het enablement proces te coördineren.

1. **Adobe** laat de toegang van de klantenrekening tot de eindpuntdienst in de Adobe VPC toe.

   - Werk de de dienstconfiguratie van het eindpunt van de Adobe bij om verzoeken goed te keuren die van de klantAWS of de Azure rekening in werking worden gesteld.
   - Werk het kaartje van de Steun bij om de de dienstnaam voor het eindpunt van Adobe VPC te verstrekken om te verbinden met, bijvoorbeeld `com.amazonaws.vpce.<cloud-region>.vpce-svc-<service-id>`.

1. **Klant** voegt de dienst van het eindpunt van de Adobe aan hun rekening van de Wolk (AWS of Azure) toe, die een verbindingsverzoek aan Adobe teweegbrengt. Raadpleeg de documentatie bij het Cloud-platform voor instructies:

   - Voor AWS, zie [Accepterend en verwerpend de verbindingsverzoeken van het interfaceeindpunt].
   - Voor Azure raadpleegt u [Verbindingsverzoeken beheren].

1. **Adobe** keurt het verbindingsverzoek goed.

1. Na goedkeuring van verbindingsaanvraag **de klant** [verifieert de verbinding](#test-vpc-endpoint-service-connection) tussen hun VPC en de Adobe VPC.

1. Aanvullende stappen om tweerichtingsverbindingen in te schakelen:

   - **Adobe** Levert het belangrijkste van de rekening van de Adobe (wortelgebruiker voor AWS of Azure rekening) en vraagt toegang tot de klantVPC eindpuntdienst.
   - **Klant** laat Adobe toegang tot de eindpuntdienst in klant VPC toe. Hierbij wordt ervan uitgegaan dat de opdrachtgever van de Adobe toegang heeft tot `arn:aws:iam::402592597372:root`, zoals eerder beschreven in het **Toegang tot eindpuntservice verleend** voorwaarde.

      - Werk de de dienstconfiguratie van het klanteneindpunt bij om verzoeken goed te keuren die van de rekening van de Adobe in werking worden gesteld. Raadpleeg de documentatie bij het Cloud-platform voor instructies:

         - Voor AWS, zie [Het toevoegen van en het verwijderen van toestemmingen voor uw eindpuntdienst].
         - Voor Azure raadpleegt u [Een verbinding met een privé-eindpunt beheren]

      - Verstrek Adobe van de eindpuntdienstnaam voor de klant VPC.

   - **Adobe** voegt de dienst van het klanteneindpunt aan de rekening van het Adobe platform (AWS of Azure) toe, die een verbindingsverzoek aan klant VPC teweegbrengt.
   - **Klant** keurt het verbindingsverzoek van Adobe goed om de opstelling te voltooien.
   - **Klant** [verifieert de verbinding](#test-vpc-endpoint-service-connection) van de Adobe VPC.

## VPC-eindpuntserviceverbinding testen

U kunt de toepassing van Telnet gebruiken om de verbinding aan de VPC eindpuntdienst te testen.

**Om de verbinding aan de VPC eindpuntdienst te testen**:

1. Van de folder van de projectwortel, **uitchecken** het milieu van het Staging of van de Productie dat wordt gevormd om tot de PrivateLink eindpuntdienst toegang te hebben.

   ```bash
   magento-cloud environment:checkout <environment-id>
   ```

1. Voer de volgende CURL-opdracht uit:

   ```bash
   curl -v telnet://<endpoint-service-dns-url>:<port>/
   ```

   Voorbeeld:

   ```terminal
   $ curl -v telnet://vpce-007ffnb9qkcnjgult-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.us-east-1.vpce.amazonaws.com:80 -vvv
   ```

   Voorbeeld van succesvolle reactie:

   ```terminal
   * Rebuilt URL to: telnet://vpce-007ffnb9qkcnjgult-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.us-east-1.vpce.amazonaws.com:80
   * Connected to vpce-0088d56482571241d-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.us-east-1.vpce. amazonaws.com (191.210.82.246) port 80 (#0)
   ```

   Monster is mislukt antwoord:

   ```terminal
   Failed to connect to vpce-007ffnb9qkcnjgult-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.ap-southeast-1.vpce.amazonaws.com port 80: Connection timed out
   * Closing connection 0
   ```

1. Controleer of de service luistert op de VM.

   ```bash
   netstat -na | grep <port>
   ```

1. Controleer de pakketstroom.

   ```bash
   tcpdump -i <ethernet-interface> -tt -nn port <destination-port> and host <source-host>
   ```

   Controleer de volgende interne instellingen om te controleren of de configuratie geldig is:

   - Instellingen voor eindpunten- en eindpuntservices
   - NLB-instellingen (Network Load Balancer)
   - De doelgroepen in NLB en controleren of zij gezond zijn
   - De URL voor het netwerkpunt/curl-eindpunt van elke VM (hierboven vermeld)

   Raadpleeg de volgende artikelen voor hulp bij het oplossen van problemen met verbindingen:

   - [AWS: Problemen oplossen, eindpuntserviceverbindingen]
   - [Amazon: Problemen met de Azure Private Link-connectiviteit oplossen]

   Als u de fouten niet kunt oplossen, werkt u het Adobe Commerce Support-ticket bij om hulp te vragen bij het vaststellen van de verbinding.

## De configuratie van PrivateLink wijzigen

[Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om een bestaande configuratie te veranderen PrivateLink. U kunt bijvoorbeeld de volgende wijzigingen aanvragen:

- Verwijder de PrivateLink-verbinding van de Adobe Commerce op de Pro-productie- of Staging-omgeving van de cloudinfrastructuur.
- Wijzig het accountnummer van het Cloud-platform van de klant voor toegang tot de eindpuntservice van de Adobe.
- Voeg of verwijder verbindingen PrivateLink van de Adobe VPC aan andere eindpuntdiensten toe beschikbaar in het milieu van klantVPC.

## Instellen voor bidirectionele Private Link-verbindingen

De klant VPC moet de volgende middelen beschikbaar hebben om bidirectionele verbindingen te steunen PrivateLink:

- Een netwerktaakverdeler (NLB)
- Een configuratie van de eindpuntdienst die toegang tot een toepassing of de dienst van klant VPC toelaat
- An [interface-eindpunt] (AWS) of [privé-eindpunt] (Azure) die Adobe toestaat om met eindpuntdiensten te verbinden die in uw VPC worden ontvangen

Als deze bronnen niet beschikbaar zijn in de VPC van de klant, moet u zich aanmelden bij uw Cloud-platformaccount om de configuratie toe te voegen.

- Amazon VPC-console- `https://console.aws.amazon.com/vpc/`
- Azure-portal `https://portal.azure.com`

Raadpleeg de documentatie bij het Cloud-platform voor instructies voor het instellen van Private Link:

- **AWS Private Link-documentatie**
   - [Creeer een Balans van de Lading van het Netwerk]
   - [Creeer een configuratie van de eindpuntdienst]
   - [Creeer een interfaceeindpunt]
   - [Levenscyclus interfaceeindpunt]

- **Azure Private Link-documentatie**
   - [Een taakverdeling maken]
   - [Azure Private Link-workflow]

<!--Link definitions-->

[Accepterend en verwerpend de verbindingsverzoeken van het interfaceeindpunt]: https://docs.aws.amazon.com/vpc/latest/userguide/accept-reject-endpoint-requests.html
[Het toevoegen van en het verwijderen van toestemmingen voor uw eindpuntdienst]: https://docs.aws.amazon.com/vpc/latest/userguide/add-endpoint-service-permissions.html
[Amazon: Problemen met de Azure Private Link-connectiviteit oplossen]: https://docs.microsoft.com/en-us/azure/private-link/troubleshoot-private-link-connectivity
[AWS: Problemen oplossen, eindpuntserviceverbindingen]: https://aws.amazon.com/premiumsupport/knowledge-center/connect-endpoint-service-vpc/
[Azure Private Link-workflow]: https://docs.microsoft.com/en-us/azure/private-link/private-link-service-overview#workflow
[Een taakverdeling maken]: https://docs.microsoft.com/en-us/azure/load-balancer/quickstart-load-balancer-standard-public-portal
[Creeer een Balans van de Lading van het Netwerk]: https://docs.aws.amazon.com/elasticloadbalancing/latest/network/create-network-load-balancer.html
[Creeer een configuratie van de eindpuntdienst]: https://docs.aws.amazon.com/vpc/latest/userguide/create-endpoint-service.html
[Creeer een interfaceeindpunt]: https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#create-interface-endpoint
[interface endpoint lifecycle]: https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#vpce-interface-lifecycle
[interface-eindpunt]: https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html
[Een verbinding met een privé-eindpunt beheren]: https://docs.microsoft.com/en-us/azure/private-link/manage-private-endpoint
[Verbindingsverzoeken beheren]: https://docs.microsoft.com/en-us/azure/private-link/private-link-service-overview#manage-your-connection-requests
[privé-eindpunt]: https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview
