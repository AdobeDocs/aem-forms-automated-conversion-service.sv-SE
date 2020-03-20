---
title: Vad är nytt? Versionsinformation - automatisk formulärkonverteringstjänst
description: 'Läs om de senaste funktionerna och felen som har åtgärdats för tjänsten Automated Forms Conversion '
translation-type: tm+mt
source-git-commit: 01dfd20951314017d47713bfb1a2a5f2d563f434

---


# Tjänsten Automated Forms Conversion: Versionsinformation

Automated Forms Conversion Service får kontinuerliga förbättringar. Om du vill hålla dig uppdaterad med den senaste utvecklingen går du regelbundet till den här sidan. Den här sidan innehåller information om:

* Senaste releaser
* Nya funktioner
* Felkorrigeringar
* Föråldrade funktioner
* Specialinstruktioner
* Framtida planer för ändringar

Den här sidan uppdateras varje månad, så gå tillbaka dit regelbundet.

## 20 mars 2020 (AFC-2020.03.1)

### Nyheter

**Identifiera logiska avsnitt i ett formulär automatiskt**

Som standard skapar tjänsten en separat panel på den översta nivån för varje sida i ett PDF-indataformulär. Nu kan du välja alternativet att ta bort **[!UICONTROL Auto-detect logical sections]** begreppet att skapa en separat panel på den översta nivån för varje PDF-sida och automatiskt identifiera logiska avsnitt. Tjänstklubbarna kopplade fält i ett formulär till en logisk sektion. Alla fält som är relaterade till faktureringsadressen är t.ex. grupperade i ett avsnitt och alla fält som är kopplade till leveransadressen är grupperade i ett annat avsnitt. Tjänsten skapar också en separat panel på den översta nivån för varje automatiskt identifierat logiskt avsnitt.

### Förbättringar

**Förbättringar i listidentifiering**

Tjänsten är nu mer effektiv när det gäller att identifiera punktlistor och numrerade listor. Det är nu enkelt att identifiera flernivålistor.

### Specialinstruktioner

**Installera paketet Automated Forms Conversion Service Connector**

Du behöver kopplingspaketet 1.1.38 eller senare för att kunna använda de senaste funktionerna och förbättringarna som levererades i version AFC-2020.03.1. Du kan hämta kopplingspaketet från [AEM Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/fd/AEM-Forms-6.5.4.0-WIN).

Om du redan har en installerad och igång miljö för automatisk formulärkonvertering kan du använda de senaste funktionerna i konverteringstjänsten genom att installera det senaste Service Pack-paketet, det senaste AEM Forms-tilläggspaketet och det senaste kopplingspaketet i den angivna ordningen. Detaljerade instruktioner finns i artikeln [Konfigurera tjänsten](configure-service.md) Automated Forms Conversion.
