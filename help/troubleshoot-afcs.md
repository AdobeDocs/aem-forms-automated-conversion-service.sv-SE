---
title: 'Felsöka automatisk formulärkonverteringstjänst '
seo-title: 'Felsöka automatisk formulärkonverteringstjänst (AFCS) '
description: 'Vanliga AFCS-problem och deras lösningar '
seo-description: Vanliga AFCS-problem och deras lösningar
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: 535267e20fb8e583e1c01f4160be378ffd31a4a4

---


# Felsöka automatisk formulärkonverteringstjänst


<!--The article provides information on installation, configuration and administration issues that may arise in an Automated Forms Conversion Service production environment. --> The document  provides basic troubleshooting steps for common errors.

## Vanliga fel {#commonerrors}

| Fel | Exempel |
|--- |--- |
| **Felmeddelande** <br> Åtkomsttokenhuvudet är inte tillgängligt. <br><br>**Orsak **till att<br>en administratör har skapat flera IMS-konfigurationer eller att IMS-konfigurationen inte kan nå AFCS-tjänsten på Adobe Cloud.<br><br>**Upplösning** <br> Om det finns flera konfigurationer tar du bort alla konfigurationer och [skapar en ny konfiguration](configure-service.md#obtainpubliccertificates). <br> Om det finns en enda konfiguration använder du **[!UICONTROL Health Check]** för att [kontrollera anslutningen](configure-service.md#createintegrationoption). | ![Åtkomsttokenhuvudet är inte tillgängligt](assets/invalid-ims-configuration.png) |
| **Felmeddelande** <br> Det gick inte att ansluta till tjänsten.  <br><br>**Orsak **<br>till felaktig tjänst-URL eller ingen tjänst-URL anges i molntjänsterna för automatisk formulärkonvertering.<br><br>**URL** för <br> tjänsten [Korrigera upplösning](configure-service.md#configure-the-cloud-service) i molntjänster för automatisk formulärkonvertering. | ![Det går inte att ansluta till tjänsten.](assets/wrong-endpoint-configured.png) |
| **Felmeddelande** <br> Tjänsten kunde inte konvertera formuläret.  <br><br>**Orsak **till att<br>nätverksanslutningsproblem uppstår när du avslutar tjänsten på grund av planerat underhåll eller driftstopp i Adobe Cloud.<br><br>**Upplösning** <br> Lös problem med nätverksanslutningen när du är klar och kontrollera statusen för tjänsten på https://status.adobe.com/ för ett planerat eller oplanerat avbrott. | ![Det går inte att ansluta till tjänsten.](assets/service-failure.png) |
| **Felmeddelande** <br> Antalet sidor är fler än 15.  <br><br>**Orsak **till att<br>källformuläret är längre än 15 sidor.<br><br>**Upplösning** <br> Använd Adobe Acrobat för att dela upp formulär med mer än 15 sidor. Använd färre än 15 sidor i ett formulär. | ![Det går inte att ansluta till tjänsten.](assets/number-of-pages.png) |
| **Felmeddelande** <br> Antalet filer är fler än 15.  <br><br>**Orsak **<br>: Mappen innehåller fler än 15 formulär.<br><br>**Upplösning** Använd <br> 15 för att ställa in antalet formulär i en mapp. Det totala antalet sidor i en mapp är mindre än 50. Minska mappens storlek till mindre än 10 MB. Behåll inte formulär i en undermapp. Organisera källformulären i en batch på 8-15 formulär. | ![Det går inte att ansluta till tjänsten.](assets/number-of-pages.png) |
| **Felmeddelande** <br> Källfilformatet stöds inte.  <br><br>**Orsak **<br>: Mappen som innehåller källformulär har filer som inte stöds.<br><br>**Upplösning** <br> Tjänsten stöder bara .xdp- och .pdf-filer. Ta bort filer med andra tillägg från mappen och kör konverteringen. | ![Det går inte att ansluta till tjänsten.](assets/unsupported-file-formats.png) |
| **Felmeddelande**<br> för skannade formulär stöds inte.  <br><br>**Orsak **<br>: PDF-formuläret innehåller bara skannade bilder av formuläret och innehåller ingen innehållsstruktur.<br><br>**Upplösning** <br> Tjänsten stöder inte konvertering av skannade formulär eller en bild av ett formulär till ett anpassat, körklart formulär. Du kan dock använda Adobe Acrobat för att konvertera bilden av ett formulär till ett PDF-formulär. Använd sedan tjänsten för att konvertera PDF-formuläret till ett anpassat formulär. Använd alltid en högkvalitativ bild av formuläret för konvertering i Acrobat. Det förbättrar kvaliteten på konverteringen. | ![Det går inte att ansluta till tjänsten.](assets/scanned-forms-error.png) |
| **Felmeddelandets** krypterade PDF-formulär <br> stöds inte.  <br><br>**Orsak **:<br>Mappen innehåller krypterade PDF-formulär.<br><br>**Upplösning** <br> Tjänsten stöder inte konvertering av krypterade PDF-formulär till adaptiva formulär. Ta bort krypteringen, ladda upp det okrypterade formuläret och kör konverteringen. | ![Det går inte att ansluta till tjänsten.](assets/secured-pdf-form.png) |
| **Felmeddelande** <br> Det gick inte att parsa JSON-schema av metamodell.  <br><br>**Orsak **<br>till att JSON-schemat som tillhandahålls till tjänsten inte är korrekt formaterat, innehåller ogiltiga tecken eller använder ogiltig syntax för att mappa komponenter.<br><br>**Upplösning** Kontrollera <br> JSON-filens formatering. Du kan använda valfri JSON-validerare online för att kontrollera schemats formatering och struktur. Mer information om metamodellsyntax finns i [Utöka artikeln med metamodellen](extending-the-default-meta-model.md) som standard. | ![Det går inte att ansluta till tjänsten.](assets/invalid-meta-model-schema.png) |
