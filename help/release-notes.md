---
title: Vad är nytt? Versionsinformation - automatisk formulärkonverteringstjänst
description: 'Läs om de senaste funktionerna och felen som har åtgärdats för tjänsten Automated Forms Conversion '
translation-type: tm+mt
source-git-commit: 6d658dbb181c09e42073e328e0232e40d4fb6b58

---


# Tjänsten Automated Forms Conversion: Versionsinformation

Automated Forms Conversion Service får kontinuerliga förbättringar. Om du vill hålla dig uppdaterad med den senaste utvecklingen går du regelbundet till den här sidan. Den här sidan innehåller information om:

* Senaste releaser
* Nya funktioner
* Felkorrigeringar
* Föråldrade funktioner
* Specialinstruktioner
* Framtida planer för ändringar

## 20 mars 2020 (AFC-2020.03.1)

### Nyheter

**Identifiera logiska avsnitt i ett formulär automatiskt**

Som standard skapar tjänsten en separat panel på den översta nivån för varje sida i ett PDF-formulär. Nu kan du använda alternativet för **[!UICONTROL Auto-detect logical sections]** att släppa paneler på sidnivå (sidnummerbaserade paneler) och endast skapa logiska paneler.  Det klär också de fält som inte hör till något avsnitt med föregående logiska avsnitt. Det förenar även fält i ett logiskt avsnitt som sprids över två intilliggande sidor till ett enda logiskt avsnitt. Om t.ex. vissa fält i ett logiskt avsnitt finns i slutet av sida ett och vissa finns i början av sida två, klubbar alla sådana fält in i ett enda logiskt avsnitt.

### Förbättringar

**Förbättringar i listidentifiering**

Tjänsten är nu mer effektiv när det gäller att identifiera punktlistor och numrerade listor. Det är nu enkelt att identifiera flernivålistor.

### Specialinstruktioner

**Installera paketet Automated Forms Conversion Service Connector**

Du behöver kopplingspaketet 1.1.38 eller senare för att kunna använda de senaste funktionerna och förbättringarna som levererades i version AFC-2020.03.1. Du kan hämta kopplingspaketet från [AEM Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/fd/AEM-Forms-6.5.4.0-WIN).

Om du redan har en installerad och igång miljö för automatisk formulärkonvertering kan du använda de senaste funktionerna i konverteringstjänsten genom att installera det senaste Service Pack-paketet, det senaste AEM Forms-tilläggspaketet och det senaste kopplingspaketet i den angivna ordningen. Detaljerade instruktioner finns i artikeln [Konfigurera tjänsten](configure-service.md) Automated Forms Conversion.
