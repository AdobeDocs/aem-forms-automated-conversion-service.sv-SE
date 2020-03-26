---
title: Vad är nytt? Versionsinformation - automatisk formulärkonverteringstjänst
description: 'Läs om de senaste funktionerna och felen som har åtgärdats för tjänsten Automated Forms Conversion '
translation-type: tm+mt
source-git-commit: dc17dfcb331df6144b8a7ce3c9c9d840b1182a95

---


# Tjänsten Automated Forms Conversion: Versionsinformation

Automated Forms Conversion Service får kontinuerliga förbättringar. Om du vill hålla dig uppdaterad med den senaste utvecklingen går du regelbundet till den här sidan. Den här sidan innehåller information om:

* Tidig åtkomst
* Senaste releaser
* Nya funktioner
* förbättringar
* Felkorrigeringar
* Föråldrade funktioner
* Specialinstruktioner
* Framtida planer för ändringar

## 20 mars 2020 (AFC-2020.03.1)

### Tidig åtkomst

**Identifiera logiska avsnitt i ett formulär automatiskt**

AFC-2020.03.1 ger tidig åtkomst till **[!UICONTROL Auto-detect logical sections]** funktionen.

Som standard skapar tjänsten en separat panel på den översta nivån för varje sida i ett PDF-formulär. Nu kan du använda alternativet för **[!UICONTROL Auto-detect logical sections]** att släppa paneler på sidnivå (sidnummerbaserade paneler) och endast skapa logiska paneler.  Det klär också de fält som inte hör till något avsnitt med föregående logiska avsnitt och fält i ett logiskt avsnitt som sprids över två intilliggande sidor till ett enda logiskt avsnitt. Om t.ex. vissa fält i ett logiskt avsnitt finns i slutet av sida ett och vissa finns i början av sida två, klubbar alla sådana fält in i ett enda logiskt avsnitt.

Du behöver kopplingspaketet 1.1.38 eller senare för att kunna använda **[!UICONTROL Auto-detect logical sections]** funktionen. Du kan hämta kopplingspaketet från [AEM Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/featurepack/AFCS-Connector-2020.03.1).

### Förbättringar

**Förbättringar i listidentifiering**

Tjänsten är nu mer effektiv när det gäller att identifiera punktlistor och numrerade listor.