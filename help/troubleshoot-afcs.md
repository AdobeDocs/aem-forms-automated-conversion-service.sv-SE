---
title: 'Felsöka automatisk formulärkonverteringstjänst '
seo-title: 'Felsöka automatisk formulärkonverteringstjänst (AFCS) '
description: 'Vanliga AFCS-problem och deras lösningar '
seo-description: Vanliga AFCS-problem och deras lösningar
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: 4b9f3f4fe3b3901cb99c9374ff40e8f49855237f

---


# Felsöka automatisk formulärkonverteringstjänst


Artikeln innehåller information om installations-, konfigurations- och administrationsproblem som kan uppstå i en produktionsmiljö för automatisk formulärkonvertering. Dokumentet innehåller även grundläggande felsökningssteg och förklaringar för vanliga felmeddelanden.

## Vanliga fel {#commonerrors}

| Fel | Exempel |
|--- |--- |
| **Felmeddelande** <br> Åtkomsttokenhuvudet är inte tillgängligt. <br><br>**Orsak **till att<br>en administratör har skapat flera IMS-konfigurationer eller att IMS-konfigurationen inte kan nå AFCS-tjänsten på Adobe Cloud.<br><br>**Upplösning** <br> Om det finns flera konfigurationer tar du bort alla konfigurationer och [skapar en ny konfiguration](configure-service.md#obtainpubliccertificates). <br> Om det finns en enda konfiguration använder du **[!UICONTROL Health Check]** för att [kontrollera anslutningen](configure-service.md#createintegrationoption). | ![Åtkomsttokenhuvudet är inte tillgängligt](assets/invalid-ims-configuration.png) |
| **Felmeddelande** <br> Det gick inte att ansluta till tjänsten.  <br><br>**Orsak **<br>till felaktig tjänst-URL eller ingen tjänst-URL anges i molntjänsterna för automatisk formulärkonvertering.<br><br>**URL** för <br> tjänsten [Korrigera upplösning](configure-service.md#configure-the-cloud-service) i molntjänster för automatisk formulärkonvertering. | ![Det går inte att ansluta till tjänsten.](assets/wrong-endpoint-configured.png) |
| **Felmeddelande** <br> Tjänsten kunde inte konvertera formuläret.  <br><br>**Orsak **<br>till nätverksanslutningsproblem eller till att tjänsten inte är tillgänglig på grund av planerat underhåll eller driftstopp i Adobe Cloud.<br><br>**Upplösning** <br> Lös problem med nätverksanslutningen när du är klar och kontrollera statusen för tjänsten på https://status.adobe.com/ för planerade eller oplanerade driftavbrott. | ![Det går inte att ansluta till tjänsten.](assets/service-failure.png) |
| **Felmeddelande** <br> Antalet sidor är fler än 15.  <br><br>**Orsak **<br>: Mappen som innehåller käll-XDP- och PDF-formulär har fler än 15 filer.<br><br>**Upplösning** Använd <br> 15 för att ställa in antalet formulär i en mapp. Det totala antalet sidor i en mapp är mindre än 50. Minska mappens storlek till mindre än 10 MB. Behåll inte formulär i en undermapp. Ordna källdokumenten i en grupp om 8-15 dokument. | ![Det går inte att ansluta till tjänsten.](assets/number-of-pages.png) |
| **Felmeddelande** <br> Källfilformatet stöds inte.  <br><br>**Orsak **<br>: Mappen som innehåller källformulär har filer som inte stöds.<br><br>**Upplösning** <br> Tjänsten stöder bara .xdp- och .pdf-filer. Ta bort filer med andra tillägg från mappen och kör konverteringen. | ![Det går inte att ansluta till tjänsten.](assets/unsupported-file-formats.png) |
| **Felmeddelande**<br> för skannade formulär stöds inte.  <br><br>**Orsak **<br>: PDF-formuläret innehåller bara skannad bild av formuläret och innehåller ingen innehållsstruktur.<br><br>**Upplösning** <br> Tjänsten stöder inte konvertering av skannade formulär eller en bild av ett formulär till ett anpassat, körklart formulär. Du kan dock använda Adobe Acrobat för att konvertera bilden av ett formulär till ett PDF-formulär. Använd sedan tjänsten för att konvertera PDF-formuläret till ett anpassat formulär. Använd alltid en högkvalitativ bild av formuläret för konvertering i Acrobat. Det förbättrar kvaliteten på konverteringen. | ![Det går inte att ansluta till tjänsten.](assets/scanned-forms-error.png) |