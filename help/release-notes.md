---
title: Nyheter Versionsinformation – konverteringstjänsten för automatiserade formulär
description: 'Lär dig mer om de senaste funktionerna och åtgärdade fel för konverteringstjänsten för automatiserade formulär '
translation-type: tm+mt
source-git-commit: 765f7bd4126fe4b8f4dd92c4b3eb556dae4e9ff0
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 93%

---


# Versionsinformation

Konverteringstjänsten för automatiserade formulär förbättras fortlöpande. Besök sidan regelbundet för att hålla dig uppdaterad om den senaste utvecklingen. Sidan innehåller information om:

* Tidig tillgång
* Senaste versioner
* Nya funktioner
* förbättringar
* Felkorrigeringar
* Inaktuell funktionalitet
* Specialinstruktioner
* Framtida planer för ändringar

## 02 feb 2021 (AFC-2021.01.2)

### Förbättringar

Förbättrad organisering av formulärinnehåll i paneler och generering av rubriker för paneler samtidigt som ett källformulär konverteras till ett anpassat formulär.

## 16 juli 2020 (AFC-2020.07.2)

### Nyheter

Lagt till stöd för att konvertera PDF forms i färg till anpassningsbara formulär.

### Förbättringar

Förbättringar av den automatiserade konverteringen av fält för text, formulär och urvalsgrupper till motsvarande adaptiva formulärkomponenter.


## 20 mars 2020 (AFC-2020.03.1)

### Tidig tillgång

**Identifiera automatiskt logiska avsnitt i ett formulär**

Som standard skapar tjänsten en separat toppnivåpanel för varje sida i ett PDF-formulär. Nu kan du använda alternativet **[!UICONTROL Auto-detect logical sections]** för att släppa sidnivåpaneler (sidnummerbaserade paneler) och endast skapa logiska paneler. Det enar också fälten som inte tillhör något avsnitt med föregående logiska avsnitt och fält i ett logisk avsnitt spritt över två angränsande sidor i ett enda logiskt avsnitt. Till exempel, om vissa fält i ett logiskt avsnitt finns i slutet av sidan ett och vissa är i början av sidan två, enas alla sådana fält i ett enda logiskt avsnitt.

### Förbättringar {#improvements}

**Förbättringar i listdetektering**

Tjänsten är nu effektivare när det gäller att upptäcka numrerade och spaltade listor.

### Specialinstruktioner

**Installera paketet Automated Forms Conversion Service connector**

Du behöver kopplingspaketet 1.1.38 eller senare för att kunna använda de senaste funktionerna och förbättringarna som levererades i version AFC-2020.03.1. Du kan hämta kopplingspaketet från [AEM Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/featurepack/AFCS-Connector-2020.03.1).

Om du redan har en miljö som är installerad och körs för konvertering av automatiserade formulär kan du använda de senaste funktionerna i konverteringstjänsten genom att installera det senaste Service Pack-paketet, det senaste AEM Forms-tilläggspaketet och det senaste kopplingspaketet, i angiven ordning. För detaljerade instruktioner, se artikel [Konfigurera konverteringstjänsten för automatiserade formulär](configure-service.md).