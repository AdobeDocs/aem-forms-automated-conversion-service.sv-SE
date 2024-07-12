---
title: Nyheter Versionsinformation – konverteringstjänsten för automatiserade formulär
description: Lär dig mer om de senaste funktionerna och åtgärdade fel för konverteringstjänsten för automatiserade formulär
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
exl-id: fccafbc9-28c1-4736-922c-24d675b25213
source-git-commit: e95b4ed35f27f920b26c05f3398529f825948f1f
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 64%

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

## 24 feb 2022 (AFC-2022.02.0) {#feb-2022}

* Funktioner för att [automatiskt konvertera avsnitt till fragment](convert-existing-forms-to-adaptive-forms.md) har lagts till för att förbättra återgivningshastigheten för konverterade formulär och göra det enklare att läsa in stora formulär i en adaptiv formulärredigerare.

## 29 aug 2021 (AFC-2021.08.0) {#aug-2021}

* Förbättrade funktioner för att konvertera PDF forms på italienska och portugisiska till anpassade formulär.

## 29 juli 2021 (AFC-2021.07.2) {#july-2021}

* Möjlighet att konvertera ett PDF-formulär på franska, tyska och spanska till ett adaptivt formulär har lagts till.

## 24 juni 2021 (AFC-2021.06.2) {#june-2021}

### Förbättringar {#june-2021-improvements}

Förbättrad precision för att automatiskt identifiera logiska avsnitt i källformulären och konvertera dem till motsvarande adaptiva formulärpaneler.

## 3 mars 2021 (AFC-2021.02.2) {#mar-2021}

### Förbättringar {#march-2021-improvements}

Förbättrad sortering av formulärinnehåll i urvalsgrupper och fält samtidigt som ett källformulär konverteras till ett anpassat formulär.

## 02 feb 2021 (AFC-2021.01.2) {#feb-2021}

### Förbättringar {#feb-2021-improvements}

Förbättrad organisering av formulärinnehåll i paneler och generering av rubriker för paneler samtidigt som ett källformulär konverteras till ett anpassat formulär.

## 16 juli 2020 (AFC-2020.07.2) {#jul-2020}

### Nyheter {#whats-new-jul-2020-}

Lagt till stöd för att konvertera PDF forms i färg till anpassningsbara formulär.

### Förbättringar {#jul-2020-improvements}

Förbättringar av den automatiserade konverteringen av fält för text, formulär och urvalsgrupper till motsvarande adaptiva formulärkomponenter.

## 20 mars 2020 (AFC-2020.03.1) {#mar-2020}

### Tidig tillgång {#early-access}

**Identifiera automatiskt logiska avsnitt i ett formulär**

Som standard skapar tjänsten en separat toppnivåpanel för varje sida i ett PDF-formulär. Nu kan du använda alternativet **[!UICONTROL Auto-detect logical sections]** för att släppa sidnivåpaneler (sidnummerbaserade paneler) och endast skapa logiska paneler. Det enar också fälten som inte tillhör något avsnitt med föregående logiska avsnitt och fält i ett logisk avsnitt spritt över två angränsande sidor i ett enda logiskt avsnitt. Till exempel, om vissa fält i ett logiskt avsnitt finns i slutet av sidan ett och vissa är i början av sidan två, enas alla sådana fält i ett enda logiskt avsnitt.

### Förbättringar {#mar-2020-improvements}

**Förbättringar i listdetektering**

Tjänsten är nu effektivare när det gäller att upptäcka numrerade och spaltade listor.

### Specialinstruktioner {#special-instructions}

**Installera paketet Automated Forms Conversion Service connector**

Du behöver kopplingspaketet 1.1.38 eller senare för att kunna använda de senaste funktionerna och förbättringarna i version AFC-2020.03.1.

Om du redan har en miljö som är installerad och körs för konvertering av automatiserade formulär kan du använda de senaste funktionerna i konverteringstjänsten genom att installera det senaste Service Pack-paketet, det senaste AEM Forms-tilläggspaketet och det senaste kopplingspaketet, i angiven ordning. För detaljerade instruktioner, se artikel [Konfigurera konverteringstjänsten för automatiserade formulär](configure-service.md).
