---
title: Technologiestapel
description: Bekijk de technologiestapel die de Handel op de infrastructuur van de Wolk vormt.
feature: Cloud, Iaas, Paas
exl-id: e456db25-c44b-4053-b96d-517d3d1606d0
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# Technologiestapel

U kunt de Adobe Commerce op cloudinfrastructuur beschouwen als vijf functionele lagen, zoals hieronder wordt getoond:

![Stapel met wolken](../../assets/CloudStack.svg)

1. [**Cloud-infrastructuur**](pro-architecture.md): Kies Amazon Web Services (AWS) of Microsoft Azure als uw IaaS-stichting (Infrastructure as a Service) voor uw Adobe Commerce op cloudinfrasinfrastructuurPro-projecten.

   Adobe analyseert het gebruik van uw virtuele computerbron (vCPU) routinematig en wijst automatisch bronnen toe om uw langetermijngebruik te optimaliseren en het risico te beperken dat uw maximale jaarlijkse vCPU-daglimiet wordt overschreden. Als u verhoogd plaatsverkeer voor specifieke tijdsperioden verwacht, moet u een kaartje van de Steun blijven openen aan [een tijdelijke upgrade aanvragen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-request-temporary-magento-upsize.html).

1. [**Platform als service**](cloud-architecture.md): Elk Adobe Commerce-project voor cloudinfrastructuur biedt een Platform as a Service (PaaS) Integration-omgeving voor het ontwikkelen, testen en integreren van services.
1. [**Adobe Commerce**](../project/overview.md): Adobe Commerce on cloud Infrastructure biedt een vooraf ingerichte infrastructuur, waaronder PHP, MySQL (MariaDB), Redis, [!DNL RabbitMQ]en ondersteunde zoekmachinetechnologieën.
1. [**Prestatiegereedschappen**](../monitor/new-relic-service.md): Met de New Relic-prestatieprogramma&#39;s kunt u fouten in uw toepassingen en infrastructuur opsporen, controleren en beheren door gegevens van uw Adobe Commerce te verzamelen, te analyseren en weer te geven voor cloud-infrastructuurprojecten.
1. [**Inhoudsleveringsnetwerk (CDN), Webtoepassingsfirewall ([!DNL WAF]) en Image Optimization (IO)**](../cdn/fastly.md):

   * [Fastly CDN](../cdn/fastly.md#ddos-protection)—Verleent de veilige diensten CDN met ingebouwde bescherming tegen Verdeelde Ontkenning van de aanvallen van de Dienst (DDoS) zoals [!DNL Ping of Death], [!DNL Smurf] aanvallen, en andere Internet Control Message Protocol (ICMP) gebaseerde overstromingsaanvallen.
   * [Web Application Firewall (WAF)](../cdn/fastly-waf-service.md)—De diensten van WAF verzekeren naleving PCI voor Adobe Commerce storefronts in productiemilieu&#39;s en beleid van WAF dat uw het Webtoepassingen van Adobe Commerce tegen injectieaanvallen, kwaadwillige input, dwars-plaats scripting, gegevensexfiltratie, het protocolschendingen van HTTP, en andere beschermt [[!DNL OWASP] De tien belangrijkste beveiligingsbedreigingen](https://owasp.org/www-project-top-ten/).
   * [Optimalisatie van afbeeldingen (IO)](../cdn/fastly-image-optimization.md)—Biedt realtime beeldbewerking en optimalisatie om de levering van images te versnellen en het onderhoud van sets met afbeeldingsbronnen voor responsieve webtoepassingen te vereenvoudigen. Met de snelste IO wordt het laden van images geoffload en de grootte van de images aangepast, zodat servers bestellingen en conversies efficiënt kunnen verwerken.

Monolithische toepassingen zijn hulpbronnenintensief en moeilijk te schalen en snel te gebruiken. Met de infrastructuur van de Wolk, krijgen de klanten van de Handel ongeëvenaarde toegang tot op SaaS-Gebaseerde microdiensten die rijk, intelligent, en prestatiesrijk zijn. Zie [Ondersteunde software en services](cloud-architecture.md#supported-software-and-services).

Gebruik de [Handleiding Aan de slag voor handel](../../get-started/overview.md) om uw nieuwe Cloud-programma in te stellen en uw [!DNL Commerce] in een cloud-native omgeving.
