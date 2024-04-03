---
title: Werknemers
description: Leer hoe u de eigenschap workers in de [!DNL Commerce] toepassingsconfiguratiebestand.
feature: Cloud, Configuration
exl-id: d6816925-5912-45ca-8255-6c307e58542d
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Workers, eigenschap

U kunt een worker definiëren die onafhankelijk van de webinstantie moet worden uitgevoerd zonder een actieve Nginx-instantie. De worker gebruikt echter dezelfde netwerkopslag als de worker [!DNL Commerce] toepassing. U te hoeven niet aan opstelling een Webserver op de arbeidersinstantie (het gebruiken Node.js of Go) omdat de router openbare verzoeken aan de worker niet kan richten. Dit maakt de arbeidersinstantie ideaal voor achtergrondtaken of voortdurend lopende taken die een plaatsing dreigen te blokkeren.

## Een worker configureren

Workers zijn alleen beschikbaar voor gebruik met Pro Staging- en Productomgevingen. Pro-integratie en Starter-omgevingen kunnen ervoor kiezen de [CRON_CONSUMERS_RUNNER](../environment/variables-deploy.md#cron_consumers_runner) variabele.

Een worker configureren in Pro Staging of Production [Een Adobe Commerce-ondersteuningsticket verzenden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) en bevat de volgende informatie:

- Project-id
- Milieu-id
- Naam van worker
- Opdrachten starten

U kunt één proces per worker configureren. Een eenvoudige, algemene arbeidersconfiguratie in de `.magento.app.yaml` kan er als volgt uitzien:

```yaml
workers:
    queue:
        commands:
            start: |
                php ./bin/magento queue:consumers:start commerce.eventing.event.publish
```

In dit voorbeeld wordt één worker gedefinieerd met de naam `queue`, met een klein (grootte S) niveau van middeltoewijzing, en stelt `php ./bin/magento` gebruiken bij het opstarten. De worker `queue` dan loopt op elke knoop als arbeidersproces. Als de opdracht wordt afgesloten, wordt deze automatisch opnieuw gestart.

## Opdrachten en overschrijvingen

De `commands.start` toets is vereist om opdrachten met de arbeiderstoepassing te starten. U kunt elke geldige shell-opdracht gebruiken, hoewel deze ideaal is voor het gebruik van de taal van uw toepassing. Als de opdracht `start` key eindigt, hij start automatisch opnieuw.

>[!IMPORTANT]
>
>De `deploy` en `post_deploy` haken en `crons` opdrachten alleen uitvoeren in de webcontainer, niet in instanties van workers.

### Overerving

Definities voor de `size`, `relationships`, `access`, `disk` en `mount`, en `variables` eigenschappen worden door een worker overgeërfd, tenzij deze expliciet worden genegeerd.

De volgende eigenschappen worden het meest gebruikt om te overschrijven [instellingen op hoofdniveau](properties.md):

- `size`—minder middelen toewijzen aan één achtergrondproces
- `variables`—instrueer de toepassing om verschillend te lopen

### Timing en wachtstand

Hoewel elke worker een rij achter een andere worker plaatst, produceert de volgende configuratie een consistente scheiding van twee seconden in tijdstempels in de `var/time.txt` bestand, ongeacht de 8 seconden slaap binnen de PHP code:

```yaml
workers:
    time1:
        commands:
            start: 'php -r "sleep(8); echo time() . PHP_EOL;" >> var/time.txt& sleep 2'
```
