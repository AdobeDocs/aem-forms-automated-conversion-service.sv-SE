---
title: 'Felsöka automatisk formulärkonverteringstjänst '
seo-title: 'Felsöka automatisk formulärkonverteringstjänst (AFCS) '
description: 'Vanliga AFCS-problem och deras lösningar '
seo-description: Vanliga AFCS-problem och deras lösningar
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: aebfde420d02bd4184022ecb42496a379d66a3b5

---


# Felsöka automatisk formulärkonverteringstjänst


Artikeln innehåller information om installations-, konfigurations- och administrationsproblem som kan uppstå i en produktionsmiljö för automatisk formulärkonvertering. Dokumentet innehåller även grundläggande felsökningssteg och förklaringar för vanliga felmeddelanden.

### Vanliga fel {#commonerrors}

| Fel | Exempel |
|--- |--- |
| **Felmeddelande** <br> Åtkomsttokenhuvudet är inte tillgängligt. <br><br>**Orsak **till att<br>en administratör har skapat flera IMS-konfigurationer eller att IMS-konfigurationen inte kan nå AFCS-tjänsten på Adobe Cloud.<br><br>**Upplösning** <br> Om det finns flera konfigurationer tar du bort alla konfigurationer och [skapar en ny konfiguration](configure-service.md#obtainpubliccertificates). <br> Om det finns en enda konfiguration använder du **[!UICONTROL Health Check]** för att [kontrollera anslutningen](configure-service.md#createintegrationoption). | ![Färgat formulär](assets/invalid-ims-configuration.png) |
| **Felmeddelande** <br> Det gick inte att ansluta till tjänsten.  <br><br>**Orsak **<br>till felaktig tjänst-URL eller ingen tjänst-URL anges i molntjänsterna för automatisk formulärkonvertering.<br><br>**URL** för <br> tjänsten [Korrigera upplösning](configure-service.md#configure-the-cloud-service) i molntjänster för automatisk formulärkonvertering. | ![Färgat formulär](assets/wrong-endpoint-configured.png) |
